---
title: "Didacticiel : intégration d’Azure Active Directory dans HappyFox | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et HappyFox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 8b5ad750d7849e4037ed7ee93c48b5645c68e799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="ecfca-103">Didacticiel : intégration d’Azure Active Directory dans HappyFox</span><span class="sxs-lookup"><span data-stu-id="ecfca-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="ecfca-104">Dans ce didacticiel, vous allez apprendre à intégrer HappyFox dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ecfca-104">In this tutorial, you learn how to integrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ecfca-105">L’intégration de HappyFox dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ecfca-105">Integrating HappyFox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ecfca-106">Dans Azure AD, vous pouvez contrôler qui a accès à HappyFox</span><span class="sxs-lookup"><span data-stu-id="ecfca-106">You can control in Azure AD who has access to HappyFox</span></span>
- <span data-ttu-id="ecfca-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à HappyFox (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecfca-107">You can enable your users to automatically get signed-on to HappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ecfca-108">Vous pouvez gérer vos comptes depuis un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="ecfca-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ecfca-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ecfca-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ecfca-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ecfca-110">Prerequisites</span></span>

<span data-ttu-id="ecfca-111">Pour configurer l’intégration d’Azure AD avec HappyFox, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ecfca-111">To configure Azure AD integration with HappyFox, you need the following items:</span></span>

- <span data-ttu-id="ecfca-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecfca-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ecfca-113">Un abonnement HappyFox pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ecfca-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ecfca-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ecfca-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ecfca-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ecfca-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ecfca-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ecfca-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ecfca-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ecfca-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ecfca-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ecfca-118">Scenario description</span></span>
<span data-ttu-id="ecfca-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ecfca-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ecfca-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="ecfca-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ecfca-121">Ajout de HappyFox à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ecfca-121">Adding HappyFox from the gallery</span></span>
2. <span data-ttu-id="ecfca-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecfca-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-the-gallery"></a><span data-ttu-id="ecfca-123">Ajout de HappyFox à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ecfca-123">Adding HappyFox from the gallery</span></span>
<span data-ttu-id="ecfca-124">Pour configurer l’intégration de HappyFox dans Azure AD, vous devez ajouter HappyFox à partir de la galerie dans votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ecfca-124">To configure the integration of HappyFox into Azure AD, you need to add HappyFox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ecfca-125">**Pour ajouter HappyFox à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ecfca-125">**To add HappyFox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ecfca-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ecfca-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ecfca-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ecfca-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ecfca-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ecfca-133">Dans la zone de recherche, tapez **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-133">In the search box, type **HappyFox**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_search.png)

5. <span data-ttu-id="ecfca-135">Dans le volet de résultats, sélectionnez **HappyFox**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="ecfca-135">In the results panel, select **HappyFox**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ecfca-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecfca-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ecfca-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec HappyFox, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ecfca-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ecfca-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur HappyFox équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecfca-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HappyFox is to a user in Azure AD.</span></span> <span data-ttu-id="ecfca-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur HappyFox associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="ecfca-140">In other words, a link relationship between an Azure AD user and the related user in HappyFox needs to be established.</span></span>

<span data-ttu-id="ecfca-141">Dans HappyFox, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="ecfca-141">In HappyFox, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ecfca-142">Pour configurer et tester l’authentification unique Azure AD avec HappyFox, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="ecfca-142">To configure and test Azure AD single sign-on with HappyFox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ecfca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ecfca-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ecfca-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ecfca-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ecfca-145">**[Création d’un utilisateur de test HappyFox](#creating-a-happyfox-test-user)** pour avoir un équivalent de Britta Simon dans HappyFox lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ecfca-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - to have a counterpart of Britta Simon in HappyFox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ecfca-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecfca-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ecfca-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ecfca-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ecfca-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecfca-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ecfca-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application HappyFox.</span><span class="sxs-lookup"><span data-stu-id="ecfca-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="ecfca-150">**Pour configurer l’authentification unique Azure AD avec HappyFox, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ecfca-150">**To configure Azure AD single sign-on with HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="ecfca-151">Dans le portail Azure, sur la page d’intégration de l’application **HappyFox**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-151">In the Azure portal, on the **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ecfca-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ecfca-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_samlbase.png)

3. <span data-ttu-id="ecfca-155">Dans la section **Domaine et URL HappyFox**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ecfca-155">On the **HappyFox Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="ecfca-157">a.</span><span class="sxs-lookup"><span data-stu-id="ecfca-157">a.</span></span> <span data-ttu-id="ecfca-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.happyfox.com/`</span><span class="sxs-lookup"><span data-stu-id="ecfca-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="ecfca-159">b.</span><span class="sxs-lookup"><span data-stu-id="ecfca-159">b.</span></span> <span data-ttu-id="ecfca-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="ecfca-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ecfca-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="ecfca-161">These values are not real.</span></span> <span data-ttu-id="ecfca-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="ecfca-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ecfca-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique HappyFox](https://support.happyfox.com/home).</span><span class="sxs-lookup"><span data-stu-id="ecfca-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) to get these values.</span></span> 
 
4. <span data-ttu-id="ecfca-164">Dans la section **Certificat de signature SAML**, cliquez sur **Certificat (Base64)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ecfca-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_certificate.png) 

5. <span data-ttu-id="ecfca-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ecfca-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ecfca-168">Dans la section **Configuration de HappyFox** , cliquez sur **Configurer HappyFox** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-168">On the **HappyFox Configuration** section, click **Configure HappyFox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ecfca-169">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_configure.png) 

7. <span data-ttu-id="ecfca-171">Connectez-vous au portail du personnel HappyFox et accédez à **Manage** (Gérer), puis cliquez sur l’onglet **Integrations** (Intégrations).</span><span class="sxs-lookup"><span data-stu-id="ecfca-171">Sign on to your HappyFox staff portal and navigate to **Manage**, Click on **Integrations** tab.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/header.png) 

8. <span data-ttu-id="ecfca-173">Dans l’onglet Integrations (Intégrations), cliquez sur **Configure** (Configurer) sous **SAML Integration** (Intégration SAML) pour ouvrir les paramètres d’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ecfca-173">In the Integrations tab, Click **Configure** under **SAML Integration** to open the Single Sign On Settings.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/configure.png) 

9. <span data-ttu-id="ecfca-175">Dans la section de configuration SAML, collez l’**URL d’authentification unique SAML** que vous avez copiée à partir du portail Azure dans la zone de texte **URL cible d’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-175">Inside SAML configuration section, paste the **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/targeturl.png)

10. <span data-ttu-id="ecfca-177">Ouvrez le certificat téléchargé à partir du portail Azure dans le Bloc-notes et collez son contenu dans la section **IdP Signature** (Signature IdP).</span><span class="sxs-lookup"><span data-stu-id="ecfca-177">Open the certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/cert.png)

11. <span data-ttu-id="ecfca-179">Cliquez sur le bouton **Enregistrer les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-179">Click **Save Settings** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="ecfca-181">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="ecfca-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ecfca-182">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="ecfca-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ecfca-183">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ecfca-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ecfca-184">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecfca-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="ecfca-185">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ecfca-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ecfca-187">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ecfca-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ecfca-188">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ecfca-190">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ecfca-192">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ecfca-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ecfca-194">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ecfca-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ecfca-196">a.</span><span class="sxs-lookup"><span data-stu-id="ecfca-196">a.</span></span> <span data-ttu-id="ecfca-197">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ecfca-198">b.</span><span class="sxs-lookup"><span data-stu-id="ecfca-198">b.</span></span> <span data-ttu-id="ecfca-199">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ecfca-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ecfca-200">c.</span><span class="sxs-lookup"><span data-stu-id="ecfca-200">c.</span></span> <span data-ttu-id="ecfca-201">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ecfca-202">d.</span><span class="sxs-lookup"><span data-stu-id="ecfca-202">d.</span></span> <span data-ttu-id="ecfca-203">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="ecfca-204">Création d’un utilisateur de test HappyFox</span><span class="sxs-lookup"><span data-stu-id="ecfca-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="ecfca-205">L’application prend en charge la configuration d’utilisateur juste-à-temps, et après authentification, les utilisateurs sont créés automatiquement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="ecfca-205">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ecfca-206">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ecfca-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ecfca-207">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à HappyFox.</span><span class="sxs-lookup"><span data-stu-id="ecfca-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HappyFox.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ecfca-209">**Pour assigner Britta Simon à HappyFox, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ecfca-209">**To assign Britta Simon to HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="ecfca-210">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ecfca-212">Dans la liste des applications, sélectionnez **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-212">In the applications list, select **HappyFox**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_app.png) 

3. <span data-ttu-id="ecfca-214">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ecfca-216">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-216">Click **Add** button.</span></span> <span data-ttu-id="ecfca-217">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ecfca-219">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ecfca-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ecfca-220">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ecfca-221">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ecfca-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ecfca-222">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ecfca-222">Testing single sign-on</span></span>

<span data-ttu-id="ecfca-223">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="ecfca-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="ecfca-224">Lorsque vous cliquez sur la mosaïque HappyFox dans le panneau d’accès, la page de connexion de l’application HappyFox devrait apparaître.</span><span class="sxs-lookup"><span data-stu-id="ecfca-224">When you click the HappyFox tile in the Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="ecfca-225">Vous devriez voir le bouton **SAML** sur la page de connexion.</span><span class="sxs-lookup"><span data-stu-id="ecfca-225">You should see the **‘SAML’** button on the sign-in page.</span></span>

    ![Plug-in](./media/active-directory-saas-happyfox-tutorial/saml.png) 

2. <span data-ttu-id="ecfca-227">Cliquez sur le bouton **SAML** pour vous connecter à HappyFox à l’aide de votre compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ecfca-227">Click the **‘SAML’** button to log in to HappyFox using your Azure AD account.</span></span>

<span data-ttu-id="ecfca-228">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ecfca-228">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ecfca-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ecfca-229">Additional resources</span></span>

* [<span data-ttu-id="ecfca-230">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ecfca-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ecfca-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ecfca-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_203.png

