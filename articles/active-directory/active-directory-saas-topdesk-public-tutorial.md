---
title: "Didacticiel : Intégration d’Azure Active Directory avec TOPdesk - Public | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et TOPdesk - Public."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: f21fe0b363776974108ff460060e4c15a51a58a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="2b759-103">Didacticiel : Intégration d’Azure Active Directory à TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="2b759-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="2b759-104">Dans ce didacticiel, vous allez apprendre à intégrer TOPdesk - Public à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2b759-104">In this tutorial, you learn how to integrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2b759-105">L’intégration de TOPdesk - Public dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2b759-105">Integrating TOPdesk - Public with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2b759-106">Dans Azure AD, vous pouvez contrôler qui a accès à TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="2b759-106">You can control in Azure AD who has access to TOPdesk - Public.</span></span>
- <span data-ttu-id="2b759-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à TOPdesk - Public (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b759-107">You can enable your users to automatically get signed-on to TOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="2b759-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2b759-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="2b759-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2b759-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b759-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2b759-110">Prerequisites</span></span>

<span data-ttu-id="2b759-111">Pour configurer l’intégration d’Azure AD à TOPdesk - Public, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2b759-111">To configure Azure AD integration with TOPdesk - Public, you need the following items:</span></span>

- <span data-ttu-id="2b759-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b759-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2b759-113">Un abonnement TOPdesk - Public pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2b759-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2b759-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2b759-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2b759-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2b759-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2b759-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2b759-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2b759-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b759-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2b759-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2b759-118">Scenario description</span></span>
<span data-ttu-id="2b759-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2b759-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2b759-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="2b759-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2b759-121">Ajout de TOPdesk - Public à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2b759-121">Adding TOPdesk - Public from the gallery</span></span>
2. <span data-ttu-id="2b759-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b759-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-the-gallery"></a><span data-ttu-id="2b759-123">Ajout de TOPdesk - Public à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2b759-123">Adding TOPdesk - Public from the gallery</span></span>
<span data-ttu-id="2b759-124">Pour configurer l’intégration de TOPdesk - Public à Azure AD, vous devez ajouter TOPdesk - Public à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2b759-124">To configure the integration of TOPdesk - Public into Azure AD, you need to add TOPdesk - Public from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2b759-125">**Pour ajouter TOPdesk - Public à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2b759-125">**To add TOPdesk - Public from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2b759-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2b759-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="2b759-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2b759-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2b759-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2b759-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="2b759-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2b759-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="2b759-133">Dans la zone de recherche, tapez **TOPdesk - Public**, sélectionnez **TOPdesk - Public** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="2b759-133">In the search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button to add the application.</span></span>

    ![TOPdesk - Public dans la liste des résultats](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2b759-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b759-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="2b759-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec TOPdesk - Public avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2b759-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2b759-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur TOPdesk - Public équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b759-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TOPdesk - Public is to a user in Azure AD.</span></span> <span data-ttu-id="2b759-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur TOPdesk - Public associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="2b759-138">In other words, a link relationship between an Azure AD user and the related user in TOPdesk - Public needs to be established.</span></span>

<span data-ttu-id="2b759-139">Dans TOPdesk - Public, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="2b759-139">In TOPdesk - Public, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2b759-140">Pour configurer et tester l’authentification unique Azure AD avec TOPdesk - Public, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="2b759-140">To configure and test Azure AD single sign-on with TOPdesk - Public, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2b759-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2b759-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2b759-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2b759-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2b759-143">**[Créer un utilisateur de test TOPdesk - Public](#create-a-topdesk---public-test-user)** pour avoir un équivalent de Britta Simon dans TOPdesk - Public lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="2b759-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - to have a counterpart of Britta Simon in TOPdesk - Public that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2b759-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b759-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2b759-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="2b759-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2b759-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b759-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2b759-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="2b759-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="2b759-148">**Pour configurer l’authentification unique Azure AD avec TOPdesk - Public, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2b759-148">**To configure Azure AD single sign-on with TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="2b759-149">Dans le portail Azure, dans la page d’intégration de l’application **TOPdesk - Public**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2b759-149">In the Azure portal, on the **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="2b759-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2b759-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="2b759-153">Dans la section **Domaine et URL TOPdesk - Public**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b759-153">On the **TOPdesk - Public Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="2b759-155">a.</span><span class="sxs-lookup"><span data-stu-id="2b759-155">a.</span></span> <span data-ttu-id="2b759-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="2b759-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="2b759-157">b.</span><span class="sxs-lookup"><span data-stu-id="2b759-157">b.</span></span> <span data-ttu-id="2b759-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="2b759-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="2b759-159">c.</span><span class="sxs-lookup"><span data-stu-id="2b759-159">c.</span></span> <span data-ttu-id="2b759-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="2b759-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2b759-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="2b759-161">These values are not real.</span></span> <span data-ttu-id="2b759-162">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="2b759-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2b759-163">L’URL de réponse est expliquée plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2b759-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="2b759-164">Contactez l’[équipe de support technique TOPdesk - Public](https://help.topdesk.com/saas/enterprise/user/) pour obtenir ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="2b759-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) to get these values.</span></span>  

4. <span data-ttu-id="2b759-165">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2b759-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="2b759-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="2b759-167">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="2b759-169">Dans la section **Configuration de TOPdesk - Public**, cliquez sur **Configurer TOPdesk - Public** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="2b759-169">On the **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2b759-170">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="2b759-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration de TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="2b759-172">Connectez-vous à votre site d’entreprise **TOPdesk - Public** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2b759-172">Sign on to your **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="2b759-173">Dans le menu **TOPdesk**, cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="2b759-173">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="2b759-174">![Paramètres](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="2b759-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="2b759-175">Cliquez sur **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="2b759-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="2b759-176">![Paramètres de connexion](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Paramètres de connexion")</span><span class="sxs-lookup"><span data-stu-id="2b759-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="2b759-177">Développez le menu **Login Settings**, puis cliquez sur **General**.</span><span class="sxs-lookup"><span data-stu-id="2b759-177">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="2b759-178">![Général](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "Général")</span><span class="sxs-lookup"><span data-stu-id="2b759-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="2b759-179">Dans la section **Public** de la section de configuration **SAML login**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b759-179">In the **Public** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="2b759-180">![Paramètres techniques](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Paramètres techniques")</span><span class="sxs-lookup"><span data-stu-id="2b759-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="2b759-181">a.</span><span class="sxs-lookup"><span data-stu-id="2b759-181">a.</span></span> <span data-ttu-id="2b759-182">Cliquez sur **Download** pour télécharger le fichier de métadonnées public et enregistrez-le en local sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2b759-182">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="2b759-183">b.</span><span class="sxs-lookup"><span data-stu-id="2b759-183">b.</span></span> <span data-ttu-id="2b759-184">Ouvrez le fichier de métadonnées téléchargé et recherchez le nœud **AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="2b759-184">Open the downloaded metadata file, and then locate the **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="2b759-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="2b759-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="2b759-186">c.</span><span class="sxs-lookup"><span data-stu-id="2b759-186">c.</span></span> <span data-ttu-id="2b759-187">Copiez la valeur **AssertionConsumerService**, collez-la dans la zone de texte **URL de réponse** dans la section **Domaine et URL TOPdesk - Public**.</span><span class="sxs-lookup"><span data-stu-id="2b759-187">Copy the **AssertionConsumerService** value, paste this value in the **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="2b759-188">Pour créer un fichier de certificat, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b759-188">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="2b759-189">![Certificat](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificat")</span><span class="sxs-lookup"><span data-stu-id="2b759-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="2b759-190">a.</span><span class="sxs-lookup"><span data-stu-id="2b759-190">a.</span></span> <span data-ttu-id="2b759-191">Ouvrez le fichier de métadonnées téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2b759-191">Open the downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="2b759-192">b.</span><span class="sxs-lookup"><span data-stu-id="2b759-192">b.</span></span> <span data-ttu-id="2b759-193">Développez le nœud **RoleDescriptor** dont le **xsi:type** est **fed:ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="2b759-193">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="2b759-194">c.</span><span class="sxs-lookup"><span data-stu-id="2b759-194">c.</span></span> <span data-ttu-id="2b759-195">Copiez la valeur du nœud **X509Certificate** .</span><span class="sxs-lookup"><span data-stu-id="2b759-195">Copy the value of the **X509Certificate** node.</span></span>
    
    <span data-ttu-id="2b759-196">d.</span><span class="sxs-lookup"><span data-stu-id="2b759-196">d.</span></span> <span data-ttu-id="2b759-197">Enregistrez la valeur de **X509Certificate** copiée, dans un fichier local sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2b759-197">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="2b759-198">Dans la section **Public**, cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="2b759-198">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="2b759-199">![Connexion SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "Connexion SAML")</span><span class="sxs-lookup"><span data-stu-id="2b759-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="2b759-200">Dans la boîte de dialogue **SAML configuration assistant** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b759-200">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="2b759-201">![Assistant de configuration SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "Assistant de configuration SAML")</span><span class="sxs-lookup"><span data-stu-id="2b759-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="2b759-202">a.</span><span class="sxs-lookup"><span data-stu-id="2b759-202">a.</span></span> <span data-ttu-id="2b759-203">Pour charger votre fichier de métadonnées téléchargé à partir du portail Azure, dans **Métadonnées de fédération**, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="2b759-203">To upload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="2b759-204">b.</span><span class="sxs-lookup"><span data-stu-id="2b759-204">b.</span></span> <span data-ttu-id="2b759-205">Pour charger votre fichier de certificat, sous **Certificate (RSA)**, cliquez sur **Browse**.</span><span class="sxs-lookup"><span data-stu-id="2b759-205">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="2b759-206">c.</span><span class="sxs-lookup"><span data-stu-id="2b759-206">c.</span></span> <span data-ttu-id="2b759-207">Pour charger le fichier de logo que vous avez obtenu de l’équipe de support TOPdesk, sous **Logo icon**, cliquez sur **Browse**.</span><span class="sxs-lookup"><span data-stu-id="2b759-207">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="2b759-208">d.</span><span class="sxs-lookup"><span data-stu-id="2b759-208">d.</span></span> <span data-ttu-id="2b759-209">Dans la zone de texte **User name attribute** (Attribut de nom d’utilisateur), entrez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="2b759-209">In the **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="2b759-210">e.</span><span class="sxs-lookup"><span data-stu-id="2b759-210">e.</span></span> <span data-ttu-id="2b759-211">Dans la zone de texte **Display name** , indiquez le nom de votre configuration.</span><span class="sxs-lookup"><span data-stu-id="2b759-211">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="2b759-212">f.</span><span class="sxs-lookup"><span data-stu-id="2b759-212">f.</span></span> <span data-ttu-id="2b759-213">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="2b759-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2b759-214">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="2b759-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2b759-215">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="2b759-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2b759-216">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2b759-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2b759-217">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b759-217">Create an Azure AD test user</span></span>

<span data-ttu-id="2b759-218">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2b759-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="2b759-220">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2b759-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2b759-221">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2b759-221">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="2b759-223">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2b759-223">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="2b759-225">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2b759-225">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="2b759-227">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b759-227">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="2b759-229">a.</span><span class="sxs-lookup"><span data-stu-id="2b759-229">a.</span></span> <span data-ttu-id="2b759-230">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2b759-230">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2b759-231">b.</span><span class="sxs-lookup"><span data-stu-id="2b759-231">b.</span></span> <span data-ttu-id="2b759-232">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2b759-232">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="2b759-233">c.</span><span class="sxs-lookup"><span data-stu-id="2b759-233">c.</span></span> <span data-ttu-id="2b759-234">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2b759-234">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="2b759-235">d.</span><span class="sxs-lookup"><span data-stu-id="2b759-235">d.</span></span> <span data-ttu-id="2b759-236">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2b759-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="2b759-237">Créer un utilisateur de test TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="2b759-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="2b759-238">Pour se connecter à TOPdesk - Public, les utilisateurs d’Azure AD doivent être approvisionnés dans TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="2b759-238">In order to enable Azure AD users to log into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="2b759-239">Dans le cas de TOPdesk - Public, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="2b759-239">In the case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="2b759-240">Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b759-240">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="2b759-241">Connectez-vous à votre site d’entreprise **TOPdesk - Public** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2b759-241">Sign on to your **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="2b759-242">Dans le menu en haut, cliquez sur **TOPdesk \> New \> Support Files \> Person**.</span><span class="sxs-lookup"><span data-stu-id="2b759-242">In the menu on the top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="2b759-243">![Personne](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Personne")</span><span class="sxs-lookup"><span data-stu-id="2b759-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="2b759-244">Dans la boîte de dialogue New User, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2b759-244">On the New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="2b759-245">![Nouvelle personne](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "Nouvelle personne")</span><span class="sxs-lookup"><span data-stu-id="2b759-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="2b759-246">a.</span><span class="sxs-lookup"><span data-stu-id="2b759-246">a.</span></span> <span data-ttu-id="2b759-247">Cliquez sur l’onglet General.</span><span class="sxs-lookup"><span data-stu-id="2b759-247">Click the General tab.</span></span>

    <span data-ttu-id="2b759-248">b.</span><span class="sxs-lookup"><span data-stu-id="2b759-248">b.</span></span> <span data-ttu-id="2b759-249">Dans la zone de texte **Surname**, tapez le nom de l’utilisateur, par exemple Simon.</span><span class="sxs-lookup"><span data-stu-id="2b759-249">In the **Surname** textbox, type Surname of the user like Simon</span></span>
 
    <span data-ttu-id="2b759-250">c.</span><span class="sxs-lookup"><span data-stu-id="2b759-250">c.</span></span> <span data-ttu-id="2b759-251">Sélectionnez un **Site** pour le compte.</span><span class="sxs-lookup"><span data-stu-id="2b759-251">Select a **Site** for the account.</span></span>
 
    <span data-ttu-id="2b759-252">d.</span><span class="sxs-lookup"><span data-stu-id="2b759-252">d.</span></span> <span data-ttu-id="2b759-253">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2b759-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="2b759-254">Vous pouvez utiliser n’importe quel outil ou API de création de compte d’utilisateur, fourni par TOPdesk - Public, pour approvisionner des comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b759-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2b759-255">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b759-255">Assign the Azure AD test user</span></span>

<span data-ttu-id="2b759-256">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="2b759-256">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TOPdesk - Public.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="2b759-258">**Pour affecter Britta Simon à TOPdesk - Public, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2b759-258">**To assign Britta Simon to TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="2b759-259">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2b759-259">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2b759-261">Dans la liste des applications, sélectionnez **TOPdesk - Public**.</span><span class="sxs-lookup"><span data-stu-id="2b759-261">In the applications list, select **TOPdesk - Public**.</span></span>

    ![Lien TOPdesk - Public dans la liste des applications](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="2b759-263">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2b759-263">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="2b759-265">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2b759-265">Click **Add** button.</span></span> <span data-ttu-id="2b759-266">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2b759-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="2b759-268">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2b759-268">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2b759-269">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2b759-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2b759-270">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2b759-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2b759-271">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2b759-271">Test single sign-on</span></span>

<span data-ttu-id="2b759-272">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="2b759-272">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2b759-273">Lorsque vous cliquez sur la vignette TOPdesk - Public dans le volet d’accès, vous devez être connecté automatiquement à votre application TOPdesk - Public.</span><span class="sxs-lookup"><span data-stu-id="2b759-273">When you click the TOPdesk - Public tile in the Access Panel, you should get automatically signed-on to your TOPdesk - Public application.</span></span>
<span data-ttu-id="2b759-274">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2b759-274">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2b759-275">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2b759-275">Additional resources</span></span>

* [<span data-ttu-id="2b759-276">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b759-276">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2b759-277">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2b759-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

