---
title: "Didacticiel : Intégration d’Azure Active Directory avec Thirdlight | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Thirdlight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ee7710cfea3a13907c0cc940a98c875bf83607a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="5e77a-103">Didacticiel : Intégration d’Azure Active Directory avec Thirdlight</span><span class="sxs-lookup"><span data-stu-id="5e77a-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="5e77a-104">L’objectif de ce didacticiel est de vous apprendre à intégrer Thirdlight avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5e77a-104">In this tutorial, you learn how to integrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5e77a-105">Intégrer Thirdlight avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5e77a-105">Integrating ThirdLight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5e77a-106">Dans Azure AD, vous pouvez contrôler l’accès à Thirdlight</span><span class="sxs-lookup"><span data-stu-id="5e77a-106">You can control in Azure AD who has access to ThirdLight</span></span>
- <span data-ttu-id="5e77a-107">Vous pouvez autoriser la connexion automatique à Thirdlight (via l’authentification unique) pour vos utilisateurs avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e77a-107">You can enable your users to automatically get signed-on to ThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5e77a-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="5e77a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5e77a-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5e77a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e77a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5e77a-110">Prerequisites</span></span>

<span data-ttu-id="5e77a-111">Pour configurer l’intégration d’Azure AD avec Thirdlight, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5e77a-111">To configure Azure AD integration with ThirdLight, you need the following items:</span></span>

- <span data-ttu-id="5e77a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e77a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5e77a-113">Un abonnement Thirdlight pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5e77a-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5e77a-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5e77a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5e77a-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5e77a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5e77a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5e77a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5e77a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5e77a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5e77a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5e77a-118">Scenario description</span></span>
<span data-ttu-id="5e77a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5e77a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5e77a-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="5e77a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5e77a-121">Ajouter Thirdlight à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5e77a-121">Adding ThirdLight from the gallery</span></span>
2. <span data-ttu-id="5e77a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e77a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-the-gallery"></a><span data-ttu-id="5e77a-123">Ajouter Thirdlight à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5e77a-123">Adding ThirdLight from the gallery</span></span>
<span data-ttu-id="5e77a-124">Pour configurer l’intégration de Thirdlight avec Azure AD, vous devez ajouter Thirdlight, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5e77a-124">To configure the integration of ThirdLight into Azure AD, you need to add ThirdLight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5e77a-125">**Pour ajouter Thirdlight à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5e77a-125">**To add ThirdLight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5e77a-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5e77a-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5e77a-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5e77a-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5e77a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5e77a-133">Dans la zone de recherche, entrez **Thirdlight**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-133">In the search box, type **ThirdLight**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. <span data-ttu-id="5e77a-135">Dans le panneau de résultats, sélectionnez **Thirdlight**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="5e77a-135">In the results panel, select **ThirdLight**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5e77a-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e77a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5e77a-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Thirdlight grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5e77a-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5e77a-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Thirdlight équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e77a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThirdLight is to a user in Azure AD.</span></span> <span data-ttu-id="5e77a-140">En d’autres termes, il faut établir une relation entre l’utilisateur Azure AD et l’utilisateur Thirdlight associé.</span><span class="sxs-lookup"><span data-stu-id="5e77a-140">In other words, a link relationship between an Azure AD user and the related user in ThirdLight needs to be established.</span></span>

<span data-ttu-id="5e77a-141">Pour cela, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Nom d’utilisateur** dans Thirdlight.</span><span class="sxs-lookup"><span data-stu-id="5e77a-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ThirdLight.</span></span>

<span data-ttu-id="5e77a-142">Pour configurer et tester l’authentification unique Azure AD avec Thirdlight, vous devez compléter les blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="5e77a-142">To configure and test Azure AD single sign-on with ThirdLight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5e77a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5e77a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5e77a-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5e77a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5e77a-145">**[Création d’un utilisateur de test Thirdlight](#creating-a-thirdlight-test-user)** pour avoir un équivalent de Britta Simon dans Thirdlight qui est lié à la représentation d’un utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e77a-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - to have a counterpart of Britta Simon in ThirdLight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5e77a-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e77a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5e77a-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="5e77a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5e77a-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e77a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5e77a-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Thirdlight.</span><span class="sxs-lookup"><span data-stu-id="5e77a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="5e77a-150">**Pour configurer l’authentification unique Azure AD avec Thirdlight, réalisez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="5e77a-150">**To configure Azure AD single sign-on with ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="5e77a-151">Dans le portail Azure, sur la page d’intégration de l’application **Thirdlight**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-151">In the Azure portal, on the **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5e77a-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5e77a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. <span data-ttu-id="5e77a-155">Dans la section **Domaine et URL Thirdlight**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5e77a-155">On the **ThirdLight Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="5e77a-157">a.</span><span class="sxs-lookup"><span data-stu-id="5e77a-157">a.</span></span> <span data-ttu-id="5e77a-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.thirdlight.com/`</span><span class="sxs-lookup"><span data-stu-id="5e77a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="5e77a-159">b.</span><span class="sxs-lookup"><span data-stu-id="5e77a-159">b.</span></span> <span data-ttu-id="5e77a-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="5e77a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5e77a-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5e77a-161">These values are not real.</span></span> <span data-ttu-id="5e77a-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="5e77a-162">Update these values with the actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="5e77a-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique Thirdlight](https://www.thirdlight.com/support).</span><span class="sxs-lookup"><span data-stu-id="5e77a-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="5e77a-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5e77a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. <span data-ttu-id="5e77a-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5e77a-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5e77a-168">Dans une autre fenêtre de navigateur web, ouvrez une session sur votre site d’entreprise Thirdlight en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5e77a-168">In a different web browser window, log in to your ThirdLight company site as an administrator.</span></span>

7. <span data-ttu-id="5e77a-169">Accédez à **Configuration \> System Administration**, puis cliquez sur **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-169">Go to **Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="5e77a-170">![Administration système](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "Administration système")</span><span class="sxs-lookup"><span data-stu-id="5e77a-170">![System Administration](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "System Administration")</span></span>

8. <span data-ttu-id="5e77a-171">Dans la section de configuration de SAML2, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5e77a-171">In the SAML2 configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="5e77a-172">![Authentification unique SAML](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "Authentification unique SAML")</span><span class="sxs-lookup"><span data-stu-id="5e77a-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="5e77a-173">a.</span><span class="sxs-lookup"><span data-stu-id="5e77a-173">a.</span></span> <span data-ttu-id="5e77a-174">Sélectionnez **Enable SAML2 Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="5e77a-175">b.</span><span class="sxs-lookup"><span data-stu-id="5e77a-175">b.</span></span> <span data-ttu-id="5e77a-176">Dans **Source for IdP Metadata**, sélectionnez **Load IdP Metadata from XML**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="5e77a-177">c.</span><span class="sxs-lookup"><span data-stu-id="5e77a-177">c.</span></span> <span data-ttu-id="5e77a-178">Ouvrez le fichier de métadonnées téléchargé, copiez son contenu, puis collez-le dans la zone de texte **Idp Metadata XML** .</span><span class="sxs-lookup"><span data-stu-id="5e77a-178">Open the downloaded metadata file, copy the content, and then paste it into the **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="5e77a-179">d.</span><span class="sxs-lookup"><span data-stu-id="5e77a-179">d.</span></span> <span data-ttu-id="5e77a-180">Cliquez sur **Save SAML2 settings**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="5e77a-181">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="5e77a-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5e77a-182">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="5e77a-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5e77a-183">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5e77a-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5e77a-184">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e77a-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="5e77a-185">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5e77a-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5e77a-187">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5e77a-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5e77a-188">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5e77a-190">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5e77a-192">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5e77a-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5e77a-194">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5e77a-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5e77a-196">a.</span><span class="sxs-lookup"><span data-stu-id="5e77a-196">a.</span></span> <span data-ttu-id="5e77a-197">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5e77a-198">b.</span><span class="sxs-lookup"><span data-stu-id="5e77a-198">b.</span></span> <span data-ttu-id="5e77a-199">Dans la zone de texte **Nom d’utilisateur** , tapez l’**adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5e77a-199">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="5e77a-200">c.</span><span class="sxs-lookup"><span data-stu-id="5e77a-200">c.</span></span> <span data-ttu-id="5e77a-201">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5e77a-202">d.</span><span class="sxs-lookup"><span data-stu-id="5e77a-202">d.</span></span> <span data-ttu-id="5e77a-203">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="5e77a-204">Création d’un utilisateur de test Thirdlight</span><span class="sxs-lookup"><span data-stu-id="5e77a-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="5e77a-205">Pour se connecter à Thirdlight, les utilisateurs d’Azure AD doivent être approvisionnés dans Thirdlight.</span><span class="sxs-lookup"><span data-stu-id="5e77a-205">To enable Azure AD users to log in to ThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="5e77a-206">Dans le cas de Thirdlight, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="5e77a-206">In the case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="5e77a-207">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5e77a-207">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="5e77a-208">Ouvrez une session en tant qu’administrateur sur le site **Thirdlight** de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="5e77a-208">Log in to your **ThirdLight** company site as an administrator.</span></span>

2. <span data-ttu-id="5e77a-209">Cliquez sur l’onglet **Users** .</span><span class="sxs-lookup"><span data-stu-id="5e77a-209">Go to **Users** tab.</span></span>

3. <span data-ttu-id="5e77a-210">Sélectionnez **Users and Groups**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-210">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="5e77a-211">Cliquez sur le bouton **Add new User** .</span><span class="sxs-lookup"><span data-stu-id="5e77a-211">Click **Add new User** button.</span></span>

5. <span data-ttu-id="5e77a-212">Renseignez les zones de texte **Username, Name or Description, Email, Choose a Preset or Group of New Members** du compte AAD valide que vous souhaitez approvisionner.</span><span class="sxs-lookup"><span data-stu-id="5e77a-212">Enter **the Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want to provision.</span></span>

6. <span data-ttu-id="5e77a-213">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="5e77a-214">Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur, fourni par Thirdlight, pour approvisionner des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="5e77a-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5e77a-215">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e77a-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5e77a-216">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Thirdlight.</span><span class="sxs-lookup"><span data-stu-id="5e77a-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThirdLight.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5e77a-218">**Pour assigner Britta Simon à Thirdlight, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5e77a-218">**To assign Britta Simon to ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="5e77a-219">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5e77a-221">Dans la liste des applications, sélectionnez **Thirdlight**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-221">In the applications list, select **ThirdLight**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. <span data-ttu-id="5e77a-223">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5e77a-225">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-225">Click **Add** button.</span></span> <span data-ttu-id="5e77a-226">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5e77a-228">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5e77a-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5e77a-229">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5e77a-230">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5e77a-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5e77a-231">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5e77a-231">Testing single sign-on</span></span>

<span data-ttu-id="5e77a-232">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="5e77a-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5e77a-233">En cliquant sur la vignette Thirdlight dans le Panneau d’accès, vous allez en principe être connecté automatiquement à votre application Thirdlight.</span><span class="sxs-lookup"><span data-stu-id="5e77a-233">When you click the ThirdLight tile in the Access Panel, you should get automatically signed-on to your ThirdLight application.</span></span>
<span data-ttu-id="5e77a-234">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5e77a-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5e77a-235">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5e77a-235">Additional resources</span></span>

* [<span data-ttu-id="5e77a-236">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e77a-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5e77a-237">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5e77a-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png

