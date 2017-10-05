---
title: "Didacticiel : Intégration d’Azure Active Directory à Directions on Microsoft | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Directions on Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e0c8986f-2acd-418d-a306-437abc44b640
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f9c068c71eb00a4c779c91c8ee0f0dc9d6ba85ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-directions-on-microsoft"></a><span data-ttu-id="04a9d-103">Didacticiel : Intégration d’Azure Active Directory à Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="04a9d-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span></span>

<span data-ttu-id="04a9d-104">Dans ce didacticiel, vous allez apprendre à intégrer Directions on Microsoft à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="04a9d-104">In this tutorial, you learn how to integrate Directions on Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="04a9d-105">L’intégration de Directions on Microsoft à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="04a9d-105">Integrating Directions on Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="04a9d-106">Dans Azure AD, vous pouvez contrôler qui a accès à Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="04a9d-106">You can control in Azure AD who has access to Directions on Microsoft</span></span>
- <span data-ttu-id="04a9d-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Directions on Microsoft (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04a9d-107">You can enable your users to automatically get signed-on to Directions on Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="04a9d-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="04a9d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="04a9d-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="04a9d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04a9d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="04a9d-110">Prerequisites</span></span>

<span data-ttu-id="04a9d-111">Pour configurer l’intégration d’Azure AD à Directions on Microsoft, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="04a9d-111">To configure Azure AD integration with Directions on Microsoft, you need the following items:</span></span>

- <span data-ttu-id="04a9d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="04a9d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="04a9d-113">Abonnement Directions on Microsoft pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="04a9d-113">A Directions on Microsoft single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="04a9d-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="04a9d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="04a9d-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="04a9d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="04a9d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="04a9d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="04a9d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="04a9d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="04a9d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="04a9d-118">Scenario description</span></span>
<span data-ttu-id="04a9d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="04a9d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="04a9d-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="04a9d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="04a9d-121">Ajout de Directions on Microsoft à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="04a9d-121">Adding Directions on Microsoft from the gallery</span></span>
2. <span data-ttu-id="04a9d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="04a9d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-directions-on-microsoft-from-the-gallery"></a><span data-ttu-id="04a9d-123">Ajout de Directions on Microsoft à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="04a9d-123">Adding Directions on Microsoft from the gallery</span></span>
<span data-ttu-id="04a9d-124">Pour configurer l’intégration de Directions on Microsoft à Azure AD, vous devez ajouter Directions on Microsoft disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="04a9d-124">To configure the integration of Directions on Microsoft into Azure AD, you need to add Directions on Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="04a9d-125">**Pour ajouter Directions on Microsoft à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="04a9d-125">**To add Directions on Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="04a9d-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="04a9d-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="04a9d-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="04a9d-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="04a9d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="04a9d-133">Dans la zone de recherche, tapez **Directions on Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-133">In the search box, type **Directions on Microsoft**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_search.png)

5. <span data-ttu-id="04a9d-135">Dans le volet de résultats, sélectionnez **Directions on Microsoft**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="04a9d-135">In the results panel, select **Directions on Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="04a9d-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="04a9d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="04a9d-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Directions on Microsoft, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="04a9d-138">In this section, you configure and test Azure AD single sign-on with Directions on Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="04a9d-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Directions on Microsoft équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04a9d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Directions on Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="04a9d-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Directions on Microsoft associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="04a9d-140">In other words, a link relationship between an Azure AD user and the related user in Directions on Microsoft needs to be established.</span></span>

<span data-ttu-id="04a9d-141">Dans Directions on Microsoft, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="04a9d-141">In Directions on Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="04a9d-142">Pour configurer et tester l’authentification unique Azure AD avec Directions on Microsoft, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="04a9d-142">To configure and test Azure AD single sign-on with Directions on Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="04a9d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="04a9d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="04a9d-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="04a9d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="04a9d-145">**[Création d’un utilisateur de test Directions on Microsoft](#creating-a-directions-on-microsoft-test-user)** pour avoir un équivalent de Britta Simon dans Directions on Microsoft lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="04a9d-145">**[Creating a Directions on Microsoft test user](#creating-a-directions-on-microsoft-test-user)** - to have a counterpart of Britta Simon in Directions on Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="04a9d-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04a9d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="04a9d-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="04a9d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="04a9d-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="04a9d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="04a9d-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="04a9d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Directions on Microsoft application.</span></span>

<span data-ttu-id="04a9d-150">**Pour configurer l’authentification unique Azure AD avec Directions on Microsoft, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="04a9d-150">**To configure Azure AD single sign-on with Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="04a9d-151">Dans le portail Azure, dans la page d’intégration de l’application **Directions on Microsoft**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-151">In the Azure portal, on the **Directions on Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="04a9d-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="04a9d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_samlbase.png)

3. <span data-ttu-id="04a9d-155">Dans la section **Domaine et URL Directions on Microsoft**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="04a9d-155">On the **Directions on Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_url.png)

    <span data-ttu-id="04a9d-157">a.</span><span class="sxs-lookup"><span data-stu-id="04a9d-157">a.</span></span> <span data-ttu-id="04a9d-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="04a9d-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://www.directionsonmicrosoft.com/user/login` |
    | `https://<subdomain>.devcloud.acquia-sites.com/<companyname>` |

    <span data-ttu-id="04a9d-159">b.</span><span class="sxs-lookup"><span data-stu-id="04a9d-159">b.</span></span> <span data-ttu-id="04a9d-160">Dans la zone de texte **Identificateur**, entrez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="04a9d-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://rhelmdirectionsonmicrosoftcomtest.devcloud.acquia-sites.com/simplesaml/<companyname>` |
    | `https://www.directionsonmicrosoft.com/simplesaml/<companyname>` |

    > [!NOTE] 
    > <span data-ttu-id="04a9d-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="04a9d-161">These values are not real.</span></span> <span data-ttu-id="04a9d-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="04a9d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="04a9d-163">Pour obtenir ces valeurs, contactez [l’équipe du support client Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="04a9d-163">Contact [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com) to get these values.</span></span> 
 
4. <span data-ttu-id="04a9d-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="04a9d-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_certificate.png) 

5. <span data-ttu-id="04a9d-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="04a9d-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="04a9d-168">Pour configurer l’authentification unique côté **Directions on Microsoft**, vous devez envoyer les **métadonnées XML** téléchargées à [l’équipe du support technique Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="04a9d-168">To configure single sign-on on **Directions on Microsoft** side, you need to send the downloaded **Metadata XML** to [Directions on Microsoft support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="04a9d-169">Pour permettre à l’équipe du support technique Directions on Microsoft de trouver votre adhésion au site fédéré, indiquez les informations de votre entreprise dans votre e-mail.</span><span class="sxs-lookup"><span data-stu-id="04a9d-169">To enable the Directions on Microsoft support team to locate your federated site membership, include your company information in your email.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="04a9d-170">L’authentification unique pour Directions on Microsoft doit être activée par [l’équipe du support client Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="04a9d-170">Single sign-on for Directions on Microsoft needs to be enabled by the [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="04a9d-171">Vous recevrez une notification une fois l’authentification unique activée.</span><span class="sxs-lookup"><span data-stu-id="04a9d-171">You will receive a notification when single sign-on has been enabled.</span></span>

> [!TIP]
> <span data-ttu-id="04a9d-172">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="04a9d-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="04a9d-173">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="04a9d-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="04a9d-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="04a9d-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="04a9d-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="04a9d-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="04a9d-176">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="04a9d-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="04a9d-178">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="04a9d-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="04a9d-179">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="04a9d-181">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="04a9d-183">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="04a9d-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="04a9d-185">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="04a9d-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="04a9d-187">a.</span><span class="sxs-lookup"><span data-stu-id="04a9d-187">a.</span></span> <span data-ttu-id="04a9d-188">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="04a9d-189">b.</span><span class="sxs-lookup"><span data-stu-id="04a9d-189">b.</span></span> <span data-ttu-id="04a9d-190">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="04a9d-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="04a9d-191">c.</span><span class="sxs-lookup"><span data-stu-id="04a9d-191">c.</span></span> <span data-ttu-id="04a9d-192">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="04a9d-193">d.</span><span class="sxs-lookup"><span data-stu-id="04a9d-193">d.</span></span> <span data-ttu-id="04a9d-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-194">Click **Create**.</span></span>
 
### <a name="creating-a-directions-on-microsoft-test-user"></a><span data-ttu-id="04a9d-195">Création d’un utilisateur de test Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="04a9d-195">Creating a Directions on Microsoft test user</span></span>

<span data-ttu-id="04a9d-196">Aucun élément d’action ne vous permet de configurer l’approvisionnement des utilisateurs dans Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="04a9d-196">There is no action item for you to configure user provisioning to Directions on Microsoft.</span></span>  

<span data-ttu-id="04a9d-197">Quand un utilisateur affecté tente de se connecter à Directions on Microsoft à l’aide du volet d’accès, Directions on Microsoft vérifie l’existence de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="04a9d-197">When an assigned user tries to log in to Directions on Microsoft using the access panel, Directions on Microsoft checks whether the user exists.</span></span> <span data-ttu-id="04a9d-198">Si aucun compte d’utilisateur n’est disponible, Directions on Microsoft le crée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="04a9d-198">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="04a9d-199">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="04a9d-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="04a9d-200">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="04a9d-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Directions on Microsoft.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="04a9d-202">**Pour affecter Britta Simon à Directions on Microsoft, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="04a9d-202">**To assign Britta Simon to Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="04a9d-203">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="04a9d-205">Dans la liste des applications, sélectionnez **Directions on Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-205">In the applications list, select **Directions on Microsoft**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_app.png) 

3. <span data-ttu-id="04a9d-207">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="04a9d-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-209">Click **Add** button.</span></span> <span data-ttu-id="04a9d-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="04a9d-212">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="04a9d-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="04a9d-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="04a9d-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="04a9d-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="04a9d-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="04a9d-215">Testing single sign-on</span></span>

<span data-ttu-id="04a9d-216">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="04a9d-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="04a9d-217">Lorsque vous cliquez sur la vignette Directions on Microsoft dans le volet d’accès, vous devez être connecté automatiquement à votre application Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="04a9d-217">When you click the Directions on Microsoft tile in the Access Panel, you should get automatically signed-on to your Directions on Microsoft application.</span></span>

<span data-ttu-id="04a9d-218">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="04a9d-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="04a9d-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="04a9d-219">Additional resources</span></span>

* [<span data-ttu-id="04a9d-220">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="04a9d-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="04a9d-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="04a9d-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_203.png

