---
title: "Didacticiel : Intégration d’Azure Active Directory à Abintegro | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Abintegro."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99287e1f-4189-494a-97c8-e1c03d047fd3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: a2a3c1a7a338ee1cb35dd08176ad3bb5f3cdc319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-abintegro"></a><span data-ttu-id="c3165-103">Didacticiel : Intégration d’Azure Active Directory à Abintegro</span><span class="sxs-lookup"><span data-stu-id="c3165-103">Tutorial: Azure Active Directory integration with Abintegro</span></span>

<span data-ttu-id="c3165-104">Dans ce didacticiel, vous allez apprendre à intégrer Abintegro dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c3165-104">In this tutorial, you learn how to integrate Abintegro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c3165-105">L’intégration d’Abintegro dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c3165-105">Integrating Abintegro with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c3165-106">Dans Azure AD, vous pouvez contrôler qui a accès à Abintegro</span><span class="sxs-lookup"><span data-stu-id="c3165-106">You can control in Azure AD who has access to Abintegro</span></span>
- <span data-ttu-id="c3165-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Abintegro (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3165-107">You can enable your users to automatically get signed-on to Abintegro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c3165-108">Vous pouvez gérer vos comptes depuis un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="c3165-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c3165-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c3165-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3165-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c3165-110">Prerequisites</span></span>

<span data-ttu-id="c3165-111">Pour configurer l’intégration d’Azure AD avec Abintegro, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c3165-111">To configure Azure AD integration with Abintegro, you need the following items:</span></span>

- <span data-ttu-id="c3165-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3165-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c3165-113">Un abonnement Abintegro pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c3165-113">An Abintegro single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c3165-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c3165-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c3165-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c3165-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c3165-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c3165-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c3165-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c3165-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c3165-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c3165-118">Scenario description</span></span>
<span data-ttu-id="c3165-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c3165-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c3165-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="c3165-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c3165-121">Ajout d’Abintegro à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c3165-121">Adding Abintegro from the gallery</span></span>
2. <span data-ttu-id="c3165-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3165-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-abintegro-from-the-gallery"></a><span data-ttu-id="c3165-123">Ajout d’Abintegro à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c3165-123">Adding Abintegro from the gallery</span></span>
<span data-ttu-id="c3165-124">Pour configurer l’intégration d’Abintegro dans Azure AD, vous devez ajouter Abintegro à partir de la galerie dans votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c3165-124">To configure the integration of Abintegro into Azure AD, you need to add Abintegro from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c3165-125">**Pour ajouter Abintegro à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c3165-125">**To add Abintegro from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c3165-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c3165-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c3165-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c3165-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c3165-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c3165-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c3165-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c3165-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c3165-133">Dans la zone de recherche, tapez **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="c3165-133">In the search box, type **Abintegro**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_search.png)

5. <span data-ttu-id="c3165-135">Dans le volet de résultats, sélectionnez **Abintegro**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="c3165-135">In the results panel, select **Abintegro**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c3165-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3165-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c3165-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Abintegro, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c3165-138">In this section, you configure and test Azure AD single sign-on with Abintegro based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c3165-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Abintegro équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3165-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Abintegro is to a user in Azure AD.</span></span> <span data-ttu-id="c3165-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Abintegro associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="c3165-140">In other words, a link relationship between an Azure AD user and the related user in Abintegro needs to be established.</span></span>

<span data-ttu-id="c3165-141">Dans Abintegro, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="c3165-141">In Abintegro, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c3165-142">Pour configurer et tester l’authentification unique Azure AD avec Abintegro, vous devez vous conformer aux indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="c3165-142">To configure and test Azure AD single sign-on with Abintegro, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c3165-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c3165-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c3165-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3165-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c3165-145">**[Création d’un utilisateur de test Abintegro](#creating-an-abintegro-test-user)** pour avoir un équivalent de Britta Simon dans Abintegro lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c3165-145">**[Creating an Abintegro test user](#creating-an-abintegro-test-user)** - to have a counterpart of Britta Simon in Abintegro that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c3165-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3165-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c3165-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="c3165-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c3165-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3165-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c3165-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Abintegro.</span><span class="sxs-lookup"><span data-stu-id="c3165-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Abintegro application.</span></span>

<span data-ttu-id="c3165-150">**Pour configurer l’authentification unique Azure AD avec Abintegro, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c3165-150">**To configure Azure AD single sign-on with Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="c3165-151">Dans le portail Azure, sur la page d’intégration de l’application **Abintegro**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c3165-151">In the Azure portal, on the **Abintegro** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="c3165-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c3165-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_samlbase.png)

3. <span data-ttu-id="c3165-155">Dans la section **Domaine et URL Abintegro**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c3165-155">On the **Abintegro Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_url.png)

    <span data-ttu-id="c3165-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span><span class="sxs-lookup"><span data-stu-id="c3165-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c3165-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="c3165-158">This value is not real.</span></span> <span data-ttu-id="c3165-159">Mettez à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="c3165-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="c3165-160">Contactez [l’équipe de support technique Abintegro](mailto:support@abintegro.com) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="c3165-160">Contact [Abintegro Client support team](mailto:support@abintegro.com) to get this value.</span></span> 
 
4. <span data-ttu-id="c3165-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c3165-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_certificate.png) 

5. <span data-ttu-id="c3165-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c3165-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-abintegro-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c3165-165">Pour configurer l’authentification unique côté **Abintegro**, vous devez envoyer le fichier **XML des métadonnées** téléchargé à l’[équipe de support technique Abintegro](mailto:support@abintegro.com).</span><span class="sxs-lookup"><span data-stu-id="c3165-165">To configure single sign-on on **Abintegro** side, you need to send the downloaded **Metadata XML** to [Abintegro support team](mailto:support@abintegro.com).</span></span> <span data-ttu-id="c3165-166">Elle configure ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="c3165-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c3165-167">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="c3165-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c3165-168">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="c3165-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c3165-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c3165-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c3165-170">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3165-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="c3165-171">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c3165-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="c3165-173">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c3165-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c3165-174">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c3165-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c3165-176">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c3165-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c3165-178">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c3165-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c3165-180">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c3165-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c3165-182">a.</span><span class="sxs-lookup"><span data-stu-id="c3165-182">a.</span></span> <span data-ttu-id="c3165-183">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c3165-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c3165-184">b.</span><span class="sxs-lookup"><span data-stu-id="c3165-184">b.</span></span> <span data-ttu-id="c3165-185">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c3165-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c3165-186">c.</span><span class="sxs-lookup"><span data-stu-id="c3165-186">c.</span></span> <span data-ttu-id="c3165-187">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c3165-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c3165-188">d.</span><span class="sxs-lookup"><span data-stu-id="c3165-188">d.</span></span> <span data-ttu-id="c3165-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c3165-189">Click **Create**.</span></span>
 
### <a name="creating-an-abintegro-test-user"></a><span data-ttu-id="c3165-190">Création d’un utilisateur de test Abintegro</span><span class="sxs-lookup"><span data-stu-id="c3165-190">Creating an Abintegro test user</span></span>

<span data-ttu-id="c3165-191">Aucun élément d’action ne vous permet de configurer l’approvisionnement des utilisateurs dans Abintegro.</span><span class="sxs-lookup"><span data-stu-id="c3165-191">There is no action item for you to configure user provisioning to Abintegro.</span></span> <span data-ttu-id="c3165-192">Quand un utilisateur affecté tente de se connecter à Abintegro via le volet d’accès, Abintegro vérifie si cet utilisateur existe.</span><span class="sxs-lookup"><span data-stu-id="c3165-192">When an assigned user tries to log into Abintegro using the access panel, Abintegro checks whether the user exists.</span></span>
  
<span data-ttu-id="c3165-193">Si aucun compte d’utilisateur n’est encore disponible, Abintegro le crée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="c3165-193">If there is no user account available yet, it is automatically created by Abintegro.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c3165-194">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c3165-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c3165-195">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Abintegro.</span><span class="sxs-lookup"><span data-stu-id="c3165-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Abintegro.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="c3165-197">**Pour assigner Britta Simon à Abintegro, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c3165-197">**To assign Britta Simon to Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="c3165-198">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c3165-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c3165-200">Dans la liste des applications, sélectionnez **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="c3165-200">In the applications list, select **Abintegro**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_app.png) 

3. <span data-ttu-id="c3165-202">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c3165-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="c3165-204">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c3165-204">Click **Add** button.</span></span> <span data-ttu-id="c3165-205">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c3165-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="c3165-207">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c3165-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c3165-208">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c3165-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c3165-209">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c3165-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c3165-210">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c3165-210">Testing single sign-on</span></span>

<span data-ttu-id="c3165-211">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c3165-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c3165-212">Lorsque vous cliquez sur la mosaïque Abintegro dans le panneau d’accès, la page de connexion de l’application Abintegro doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="c3165-212">When you click the Abintegro tile in the Access Panel, you should get login page of Abintegro application.</span></span>
<span data-ttu-id="c3165-213">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c3165-213">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c3165-214">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c3165-214">Additional resources</span></span>

* [<span data-ttu-id="c3165-215">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3165-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c3165-216">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c3165-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_203.png

