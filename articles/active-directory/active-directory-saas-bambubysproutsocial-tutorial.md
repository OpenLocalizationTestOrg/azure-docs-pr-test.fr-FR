---
title: "Didacticiel : Intégration d’Azure Active Directory à Bambu by Sprout Social | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Bambu by Sprout Social."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 985966d26f6ed0dcd4db47589abf94260ce62bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="1f9ba-103">Didacticiel : Intégration d’Azure Active Directory à Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="1f9ba-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="1f9ba-104">Dans ce didacticiel, vous allez apprendre à intégrer Bambu by Sprout Social à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f9ba-104">In this tutorial, you learn how to integrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1f9ba-105">L’intégration de Bambu by Sprout Social à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1f9ba-105">Integrating Bambu by Sprout Social with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1f9ba-106">Dans Azure AD, vous pouvez contrôler qui a accès à Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="1f9ba-106">You can control in Azure AD who has access to Bambu by Sprout Social</span></span>
- <span data-ttu-id="1f9ba-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Bambu by Sprout Social (via l’authentification unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f9ba-107">You can enable your users to automatically get signed-on to Bambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1f9ba-108">Vous pouvez gérer vos comptes depuis un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1f9ba-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1f9ba-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1f9ba-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with Bambu by Sprout Social, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="1f9ba-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1f9ba-110">Prerequisites</span></span>

<span data-ttu-id="1f9ba-111">Pour configurer l’intégration d’Azure AD à Bambu by Sprout Social, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1f9ba-111">To configure Azure AD integration with Bambu by Sprout Social, you need the following items:</span></span>

- <span data-ttu-id="1f9ba-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f9ba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1f9ba-113">Un abonnement Bambu by Sprout Social pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1f9ba-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1f9ba-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1f9ba-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1f9ba-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1f9ba-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="1f9ba-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f9ba-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1f9ba-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1f9ba-118">Scenario description</span></span>
<span data-ttu-id="1f9ba-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1f9ba-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1f9ba-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1f9ba-121">Ajout de Bambu by Sprout Social à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1f9ba-121">Adding Bambu by Sprout Social from the gallery</span></span>
2. <span data-ttu-id="1f9ba-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f9ba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-the-gallery"></a><span data-ttu-id="1f9ba-123">Ajout de Bambu by Sprout Social à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1f9ba-123">Adding Bambu by Sprout Social from the gallery</span></span>
<span data-ttu-id="1f9ba-124">Pour configurer l’intégration de Bambu by Sprout Social à Azure AD, vous devez ajouter Bambu by Sprout Social depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-124">To configure the integration of Bambu by Sprout Social into Azure AD, you need to add Bambu by Sprout Social from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1f9ba-125">**Pour ajouter Bambu by Sprout Social à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1f9ba-125">**To add Bambu by Sprout Social from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1f9ba-126">Dans le volet de navigation gauche du **[Portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1f9ba-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1f9ba-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1f9ba-131">Pour ajouter la nouvelle application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1f9ba-133">Dans la zone de recherche, tapez **Bambu by Sprout Social**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-133">In the search box, type **Bambu by Sprout Social**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="1f9ba-135">Dans le volet de résultats, sélectionnez **Bambu by Sprout Social**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-135">In the results panel, select **Bambu by Sprout Social**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1f9ba-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f9ba-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1f9ba-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Bambu by Sprout Social sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1f9ba-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1f9ba-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Bambu by Sprout Social équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bambu by Sprout Social is to a user in Azure AD.</span></span> <span data-ttu-id="1f9ba-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur de Bambu by Sprout Social associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-140">In other words, a link relationship between an Azure AD user and the related user in Bambu by Sprout Social needs to be established.</span></span>

<span data-ttu-id="1f9ba-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="1f9ba-142">Pour configurer et tester l’authentification unique Azure AD avec Bambu by Sprout Social, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1f9ba-142">To configure and test Azure AD single sign-on with Bambu by Sprout Social, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1f9ba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1f9ba-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l'authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1f9ba-145">**[Création d’un utilisateur de test Bambu by Sprout Social](#creating-a-bambu-by-sprout-social-test-user)** : pour avoir un équivalent de Britta Simon dans Bambu by Sprout Social lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - to have a counterpart of Britta Simon in Bambu by Sprout Social that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="1f9ba-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1f9ba-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1f9ba-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f9ba-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1f9ba-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="1f9ba-150">**Pour configurer l’authentification unique Azure AD avec Bambu by Sprout Social, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1f9ba-150">**To configure Azure AD single sign-on with Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="1f9ba-151">Dans le Portail Azure, sur la page d’intégration de l’application **Bambu by Sprout Social**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-151">In the Azure portal, on the **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1f9ba-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="1f9ba-155">Dans la section **Domaine et URL de Bambu by Sprout Social**, l’utilisateur n’aura pas à effectuer les étapes que l’application a déjà intégrées préalablement avec Azure.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-155">On the **Bambu by Sprout Social Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="1f9ba-157">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="1f9ba-159">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1f9ba-159">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="1f9ba-161">Dans la section **Configuration de Bambu by Sprout Social**, cliquez sur **Configurer Bambu by Sprout Social** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-161">On the **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1f9ba-162">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="1f9ba-162">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="1f9ba-164">Pour configurer l’authentification unique côté **Bambu by Sprout Social**, vous devez envoyer le **XML de métadonnées** et l’**URL du service d’authentification unique SAML** téléchargés à l’équipe de support [Bambu by Sprout Social](mailto:support@getbambu.com).</span><span class="sxs-lookup"><span data-stu-id="1f9ba-164">To configure single sign-on on **Bambu by Sprout Social** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="1f9ba-165">Ils effectueront les réglages nécessaires pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-165">They will set this up in order to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1f9ba-166">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1f9ba-167">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Single Sign-On** (Authentification unique) et accédez à la documentation incorporée via la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click on the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1f9ba-168">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1f9ba-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

To ensure users can sign-in to Bambu by Sprout Social after it has been configured to use Azure Active Directory, review the following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior to sign-in. To set this up, see Provisioning.
 
- Users must be assigned access to Bambu by Sprout Social in Azure AD to sign-in. To assign users, see Users.
 
- To configure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on to users, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1f9ba-169">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f9ba-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="1f9ba-170">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1f9ba-172">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1f9ba-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1f9ba-173">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1f9ba-175">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-175">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1f9ba-177">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-177">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1f9ba-179">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1f9ba-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1f9ba-181">a.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-181">a.</span></span> <span data-ttu-id="1f9ba-182">Dans la zone de texte **Name**, entrez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-182">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="1f9ba-183">b.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-183">b.</span></span> <span data-ttu-id="1f9ba-184">Dans la zone de texte **Nom d’utilisateur** , tapez l’**adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-184">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="1f9ba-185">c.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-185">c.</span></span> <span data-ttu-id="1f9ba-186">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1f9ba-187">d.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-187">d.</span></span> <span data-ttu-id="1f9ba-188">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="1f9ba-189">Création d’un utilisateur de test Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="1f9ba-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="1f9ba-190">L’application prend en charge la configuration d’utilisateur juste-à-temps, et après authentification, les utilisateurs sont créés automatiquement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-190">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1f9ba-191">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1f9ba-191">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1f9ba-192">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-192">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bambu by Sprout Social.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1f9ba-194">**Pour affecter Britta Simon à Bambu by Sprout Social, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1f9ba-194">**To assign Britta Simon to Bambu by Sprout Social, perform the following steps:**</span></span>

1. <span data-ttu-id="1f9ba-195">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-195">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1f9ba-197">Dans la liste des applications, sélectionnez **Bambu by Sprout Social**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-197">In the applications list, select **Bambu by Sprout Social**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="1f9ba-199">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-199">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1f9ba-201">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-201">Click **Add** button.</span></span> <span data-ttu-id="1f9ba-202">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1f9ba-204">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-204">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1f9ba-205">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1f9ba-206">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1f9ba-207">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1f9ba-207">Testing single sign-on</span></span>

<span data-ttu-id="1f9ba-208">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-208">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1f9ba-209">Lorsque vous cliquez sur la vignette Bambu by Sprout Social dans le volet d’accès, vous devez être connecté automatiquement à votre application Bambu by Sprout Social.</span><span class="sxs-lookup"><span data-stu-id="1f9ba-209">When you click the Bambu by Sprout Social tile in the Access Panel, you should get automatically signed-on to your Bambu by Sprout Social application.</span></span> <span data-ttu-id="1f9ba-210">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="1f9ba-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1f9ba-211">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1f9ba-211">Additional resources</span></span>

* [<span data-ttu-id="1f9ba-212">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f9ba-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1f9ba-213">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1f9ba-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

