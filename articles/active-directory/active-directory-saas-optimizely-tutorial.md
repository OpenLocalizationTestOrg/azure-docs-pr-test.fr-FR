---
title: "Didacticiel : Intégration d’Azure Active Directory à Optimizely |Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Optimizely."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 4d6f6da6bace09fbd6ab105530a1162653675c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="42b0f-103">Didacticiel : Intégration d’Azure Active Directory avec Optimizely</span><span class="sxs-lookup"><span data-stu-id="42b0f-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="42b0f-104">Dans ce didacticiel, vous allez apprendre à intégrer Optimizely avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42b0f-104">In this tutorial, you learn how to integrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="42b0f-105">L’intégration d’Optimizely à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="42b0f-105">Integrating Optimizely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="42b0f-106">Dans Azure AD, vous pouvez contrôler qui a accès à Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42b0f-106">You can control in Azure AD who has access to Optimizely</span></span>
- <span data-ttu-id="42b0f-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Optimizely (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42b0f-107">You can enable your users to automatically get signed-on to Optimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="42b0f-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="42b0f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="42b0f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="42b0f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42b0f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="42b0f-110">Prerequisites</span></span>

<span data-ttu-id="42b0f-111">Pour configurer l’intégration d’Azure AD avec Optimizely, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="42b0f-111">To configure Azure AD integration with Optimizely, you need the following items:</span></span>

- <span data-ttu-id="42b0f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="42b0f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="42b0f-113">Un abonnement Optimizely pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="42b0f-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="42b0f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="42b0f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="42b0f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="42b0f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="42b0f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="42b0f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="42b0f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="42b0f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="42b0f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="42b0f-118">Scenario description</span></span>
<span data-ttu-id="42b0f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="42b0f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="42b0f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="42b0f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="42b0f-121">Ajout d’Optimizely à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="42b0f-121">Adding Optimizely from the gallery</span></span>
2. <span data-ttu-id="42b0f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="42b0f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-the-gallery"></a><span data-ttu-id="42b0f-123">Ajout d’Optimizely à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="42b0f-123">Adding Optimizely from the gallery</span></span>
<span data-ttu-id="42b0f-124">Pour configurer l’intégration d’Optimizely avec Azure AD, vous devez ajouter Optimizely à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="42b0f-124">To configure the integration of Optimizely into Azure AD, you need to add Optimizely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="42b0f-125">**Pour ajouter Optimizely à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42b0f-125">**To add Optimizely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="42b0f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="42b0f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="42b0f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="42b0f-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="42b0f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="42b0f-133">Dans la zone de recherche, tapez **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-133">In the search box, type **Optimizely**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="42b0f-135">Dans le volet de résultats, sélectionnez **Optimizely**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="42b0f-135">In the results panel, select **Optimizely**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="42b0f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="42b0f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="42b0f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Optimizely avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="42b0f-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="42b0f-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Optimizely équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42b0f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Optimizely is to a user in Azure AD.</span></span> <span data-ttu-id="42b0f-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Optimizely associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="42b0f-140">In other words, a link relationship between an Azure AD user and the related user in Optimizely needs to be established.</span></span>

<span data-ttu-id="42b0f-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42b0f-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Optimizely.</span></span>

<span data-ttu-id="42b0f-142">Pour configurer et tester l’authentification unique Azure AD avec Optimizely, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="42b0f-142">To configure and test Azure AD single sign-on with Optimizely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="42b0f-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="42b0f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="42b0f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42b0f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="42b0f-145">**[Création d’un utilisateur de test Optimizely](#creating-an-optimizely-test-user)** pour avoir un équivalent de Britta Simon dans Optimizely lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="42b0f-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - to have a counterpart of Britta Simon in Optimizely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="42b0f-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="42b0f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="42b0f-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="42b0f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="42b0f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="42b0f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="42b0f-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42b0f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="42b0f-150">**Pour configurer l’authentification unique Azure AD avec Optimizely, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42b0f-150">**To configure Azure AD single sign-on with Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="42b0f-151">Dans le portail Azure, sur la page d’intégration de l’application **Optimizely**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-151">In the Azure portal, on the **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="42b0f-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="42b0f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="42b0f-155">Dans la section **Domaine et URL Optimizely**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="42b0f-155">On the **Optimizely Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="42b0f-157">a.</span><span class="sxs-lookup"><span data-stu-id="42b0f-157">a.</span></span> <span data-ttu-id="42b0f-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="42b0f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="42b0f-159">b.</span><span class="sxs-lookup"><span data-stu-id="42b0f-159">b.</span></span> <span data-ttu-id="42b0f-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="42b0f-160">In the **Identifier** textbox, type a URL using the following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="42b0f-161">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="42b0f-161">These values are not the real.</span></span> <span data-ttu-id="42b0f-162">Vous mettrez à jour la valeur avec l’URL de connexion et l’identificateur réels. La procédure est expliquée plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="42b0f-162">You will update the value with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="42b0f-163">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="42b0f-163">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="42b0f-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="42b0f-165">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="42b0f-167">Dans la section **Configuration d’Optimizely**, cliquez sur **Configurer Optimizely** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-167">On the **Optimizely Configuration** section, click **Configure Optimizely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="42b0f-168">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="42b0f-168">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="42b0f-170">Pour configurer l’authentification unique côté **Optimizely**, contactez votre responsable de compte Optimizely et fournissez-lui le **certificat (Base64)** téléchargé et **l’URL du service d’authentification unique SAML**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-170">To configure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide the downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="42b0f-171">En réponse à votre e-mail, Optimizely vous fournit l’URL de connexion (authentification unique initiée par le fournisseur de service) et l’identificateur (ID d’entité du fournisseur de service).</span><span class="sxs-lookup"><span data-stu-id="42b0f-171">In response to your email, Optimizely provides you with the Sign On URL (SP-initiated SSO) and the Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="42b0f-172">a.</span><span class="sxs-lookup"><span data-stu-id="42b0f-172">a.</span></span> <span data-ttu-id="42b0f-173">Copiez **l’URL d’authentification unique initiée par SP** fournie par Optimizely, puis collez-la dans la zone de texte **URL de connexion** de la section **Domaine et URL Optimizely** sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="42b0f-173">Copy the **SP-initiated SSO URL** provided by Optimizely, and paste into the **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="42b0f-174">b.</span><span class="sxs-lookup"><span data-stu-id="42b0f-174">b.</span></span> <span data-ttu-id="42b0f-175">Copiez **l’ID d’entité du fournisseur d’identité** fourni par Optimizely, puis collez-le dans la zone de texte **Identificateur** de la section **Domaine et URL Optimizely** sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="42b0f-175">Copy the **Service Provider Entity ID** provided by Optimizely, and paste into the **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="42b0f-176">Dans une autre fenêtre de navigateur, connectez-vous à votre application Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42b0f-176">In a different browser window, sign-on to your Optimizely application.</span></span>

10. <span data-ttu-id="42b0f-177">Cliquez sur le nom de votre compte dans l’angle supérieur droit, puis sur **Paramètres du compte**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-177">Click you account name in the top right corner and then **Account Settings**.</span></span>
   
    ![Authentification unique Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="42b0f-179">Sous l’onglet Compte, cochez la case **Activer l’authentification unique** sous Authentification unique dans la section **Vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-179">In the Account tab, check the box **Enable SSO** under Single Sign On in the **Overview** section.</span></span>
   
    ![Authentification unique Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="42b0f-181">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="42b0f-182">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="42b0f-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="42b0f-183">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="42b0f-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="42b0f-184">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="42b0f-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="42b0f-185">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="42b0f-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="42b0f-186">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="42b0f-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="42b0f-188">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42b0f-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="42b0f-189">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="42b0f-191">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="42b0f-193">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="42b0f-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="42b0f-195">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="42b0f-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="42b0f-197">a.</span><span class="sxs-lookup"><span data-stu-id="42b0f-197">a.</span></span> <span data-ttu-id="42b0f-198">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="42b0f-199">b.</span><span class="sxs-lookup"><span data-stu-id="42b0f-199">b.</span></span> <span data-ttu-id="42b0f-200">Dans la zone de texte **Nom d’utilisateur** , tapez l’**adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="42b0f-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="42b0f-201">c.</span><span class="sxs-lookup"><span data-stu-id="42b0f-201">c.</span></span> <span data-ttu-id="42b0f-202">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="42b0f-203">d.</span><span class="sxs-lookup"><span data-stu-id="42b0f-203">d.</span></span> <span data-ttu-id="42b0f-204">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="42b0f-205">Création d’un utilisateur de test Optimizely</span><span class="sxs-lookup"><span data-stu-id="42b0f-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="42b0f-206">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42b0f-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="42b0f-207">Sur la page d’accueil, sélectionnez l’onglet **Collaborateurs**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-207">On the home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="42b0f-208">Pour ajouter un nouveau collaborateur au projet, cliquez sur **Nouveau collaborateur**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-208">To add new collaborator to the project, click **New Collaborator**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="42b0f-210">Renseignez l’adresse de messagerie et assignez un rôle au nouveau collaborateur.</span><span class="sxs-lookup"><span data-stu-id="42b0f-210">Fill in the email address and assign them a role.</span></span> <span data-ttu-id="42b0f-211">Cliquez sur **Inviter**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-211">Click **Invite**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="42b0f-213">Il reçoit une invitation par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="42b0f-213">They receive an email invite.</span></span> <span data-ttu-id="42b0f-214">À l’aide de l’adresse de messagerie, il doit se connecter à Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42b0f-214">Using the email address, they have to log in to Optimizely.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="42b0f-215">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="42b0f-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="42b0f-216">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42b0f-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Optimizely.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="42b0f-218">**Pour affecter Britta Simon à Optimizely, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="42b0f-218">**To assign Britta Simon to Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="42b0f-219">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="42b0f-221">Dans la liste des applications, sélectionnez **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-221">In the applications list, select **Optimizely**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="42b0f-223">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="42b0f-225">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-225">Click **Add** button.</span></span> <span data-ttu-id="42b0f-226">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="42b0f-228">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="42b0f-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="42b0f-229">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="42b0f-230">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="42b0f-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="42b0f-231">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="42b0f-231">Testing single sign-on</span></span>

<span data-ttu-id="42b0f-232">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="42b0f-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="42b0f-233">Lorsque vous cliquez sur la vignette Optimizely dans le volet d’accès, vous devez être connecté automatiquement à votre application Optimizely.</span><span class="sxs-lookup"><span data-stu-id="42b0f-233">When you click the Optimizely tile in the Access Panel, you should get automatically signed-on to your Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="42b0f-234">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="42b0f-234">Additional resources</span></span>

* [<span data-ttu-id="42b0f-235">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="42b0f-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="42b0f-236">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="42b0f-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

