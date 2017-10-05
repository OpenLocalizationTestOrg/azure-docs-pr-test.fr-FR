---
title: "Didacticiel : Intégration d’Azure Active Directory avec RolePoint | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et RolePoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68d37f40-15da-45f5-a9e1-d53f78e786d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: jeedes
ms.openlocfilehash: fcde562484f4401e9f936614b9978f839f4aa290
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rolepoint"></a><span data-ttu-id="70a72-103">Didacticiel : Intégration d’Azure Active Directory avec RolePoint</span><span class="sxs-lookup"><span data-stu-id="70a72-103">Tutorial: Azure Active Directory integration with RolePoint</span></span>

<span data-ttu-id="70a72-104">Dans ce didacticiel, vous allez apprendre à intégrer RolePoint avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="70a72-104">In this tutorial, you learn how to integrate RolePoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="70a72-105">L’intégration de RolePoint avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="70a72-105">Integrating RolePoint with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="70a72-106">Dans Azure AD, vous pouvez contrôler qui a accès à RolePoint.</span><span class="sxs-lookup"><span data-stu-id="70a72-106">You can control in Azure AD who has access to RolePoint</span></span>
- <span data-ttu-id="70a72-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à RolePoint (au moyen de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70a72-107">You can enable your users to automatically get signed-on to RolePoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="70a72-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="70a72-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="70a72-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="70a72-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70a72-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="70a72-110">Prerequisites</span></span>

<span data-ttu-id="70a72-111">Pour configurer l’intégration d’Azure AD à RolePoint, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="70a72-111">To configure Azure AD integration with RolePoint, you need the following items:</span></span>

- <span data-ttu-id="70a72-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="70a72-112">An Azure AD subscription</span></span>
- <span data-ttu-id="70a72-113">Un abonnement RolePoint pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="70a72-113">A RolePoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="70a72-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="70a72-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="70a72-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="70a72-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="70a72-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="70a72-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="70a72-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70a72-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="70a72-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="70a72-118">Scenario description</span></span>
<span data-ttu-id="70a72-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="70a72-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="70a72-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="70a72-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="70a72-121">Ajout de RolePoint à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="70a72-121">Adding RolePoint from the gallery</span></span>
2. <span data-ttu-id="70a72-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="70a72-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rolepoint-from-the-gallery"></a><span data-ttu-id="70a72-123">Ajout de RolePoint à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="70a72-123">Adding RolePoint from the gallery</span></span>
<span data-ttu-id="70a72-124">Pour configurer l’intégration de RolePoint avec Azure AD, vous devez ajouter RolePoint, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="70a72-124">To configure the integration of RolePoint into Azure AD, you need to add RolePoint from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="70a72-125">**Pour ajouter RolePoint à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="70a72-125">**To add RolePoint from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="70a72-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="70a72-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="70a72-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="70a72-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="70a72-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="70a72-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="70a72-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="70a72-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="70a72-133">Dans la zone de recherche, tapez **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="70a72-133">In the search box, type **RolePoint**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_search.png)

5. <span data-ttu-id="70a72-135">Dans le panneau de résultats, sélectionnez **RolePoint**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="70a72-135">In the results panel, select **RolePoint**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="70a72-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="70a72-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="70a72-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec RolePoint grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="70a72-138">In this section, you configure and test Azure AD single sign-on with RolePoint based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="70a72-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur RolePoint équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70a72-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RolePoint is to a user in Azure AD.</span></span> <span data-ttu-id="70a72-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur RolePoint associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="70a72-140">In other words, a link relationship between an Azure AD user and the related user in RolePoint needs to be established.</span></span>

<span data-ttu-id="70a72-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans RolePoint.</span><span class="sxs-lookup"><span data-stu-id="70a72-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in RolePoint.</span></span>

<span data-ttu-id="70a72-142">Pour configurer et tester l’authentification unique Azure AD avec RolePoint, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="70a72-142">To configure and test Azure AD single sign-on with RolePoint, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="70a72-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="70a72-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="70a72-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70a72-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="70a72-145">**[Création d’un utilisateur de test RolePoint](#creating-a-rolepoint-test-user)** pour avoir un équivalent de Britta Simon dans RolePoint qui est lié à la représentation d’un utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70a72-145">**[Creating a RolePoint test user](#creating-a-rolepoint-test-user)** - to have a counterpart of Britta Simon in RolePoint that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="70a72-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70a72-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="70a72-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="70a72-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="70a72-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="70a72-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="70a72-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application RolePoint.</span><span class="sxs-lookup"><span data-stu-id="70a72-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RolePoint application.</span></span>

<span data-ttu-id="70a72-150">**Pour configurer l’authentification unique Azure AD avec RolePoint, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="70a72-150">**To configure Azure AD single sign-on with RolePoint, perform the following steps:**</span></span>

1. <span data-ttu-id="70a72-151">Dans le portail Azure, sur la page d’intégration de l’application **RolePoint**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="70a72-151">In the Azure portal, on the **RolePoint** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="70a72-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="70a72-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_samlbase.png)

3. <span data-ttu-id="70a72-155">Dans la section **Domaine et URL RolePoint**, réalisez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="70a72-155">On the **RolePoint Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_url.png)

    <span data-ttu-id="70a72-157">a.</span><span class="sxs-lookup"><span data-stu-id="70a72-157">a.</span></span> <span data-ttu-id="70a72-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.rolepoint.com/login`</span><span class="sxs-lookup"><span data-stu-id="70a72-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.rolepoint.com/login`</span></span>
    
    <span data-ttu-id="70a72-159">b.</span><span class="sxs-lookup"><span data-stu-id="70a72-159">b.</span></span> <span data-ttu-id="70a72-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://app.rolepoint.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="70a72-160">In the **Identifier** textbox, type a URL using the following pattern: `https://app.rolepoint.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="70a72-161">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="70a72-161">These values are not the real.</span></span> <span data-ttu-id="70a72-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="70a72-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="70a72-163">Nous vous suggérons d’utiliser ici la valeur de chaîne unique dans l’identificateur. Pour obtenir la valeur, contacter l’[équipe de support RolePoint](mailto:info@rolepoint.com).</span><span class="sxs-lookup"><span data-stu-id="70a72-163">Here we suggest you to use the unique value of string in the Identifier.Contact [RolePoint support team](mailto:info@rolepoint.com) to get the value.</span></span> 
 
4. <span data-ttu-id="70a72-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="70a72-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_certificate.png) 

5. <span data-ttu-id="70a72-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="70a72-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rolepoint-tutorial/tutorial_general_400.png)


6. <span data-ttu-id="70a72-168">Pour configurer l’authentification unique côté **RolePoint**, vous devez envoyer le fichier **XML des métadonnées** téléchargé à [l’équipe de support RolePoint](mailto:info@rolepoint.com).</span><span class="sxs-lookup"><span data-stu-id="70a72-168">To configure single sign-on on **RolePoint** side, you need to send the downloaded **Metadata XML** to [RolePoint support team](mailto:info@rolepoint.com).</span></span>

> [!TIP]
> <span data-ttu-id="70a72-169">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="70a72-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="70a72-170">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="70a72-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="70a72-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="70a72-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="70a72-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="70a72-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="70a72-173">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="70a72-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="70a72-175">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="70a72-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="70a72-176">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="70a72-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="70a72-178">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="70a72-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="70a72-180">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="70a72-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="70a72-182">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="70a72-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="70a72-184">a.</span><span class="sxs-lookup"><span data-stu-id="70a72-184">a.</span></span> <span data-ttu-id="70a72-185">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="70a72-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="70a72-186">b.</span><span class="sxs-lookup"><span data-stu-id="70a72-186">b.</span></span> <span data-ttu-id="70a72-187">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="70a72-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="70a72-188">c.</span><span class="sxs-lookup"><span data-stu-id="70a72-188">c.</span></span> <span data-ttu-id="70a72-189">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="70a72-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="70a72-190">d.</span><span class="sxs-lookup"><span data-stu-id="70a72-190">d.</span></span> <span data-ttu-id="70a72-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="70a72-191">Click **Create**.</span></span>
 
### <a name="creating-a-rolepoint-test-user"></a><span data-ttu-id="70a72-192">Création d’un utilisateur de test RolePoint</span><span class="sxs-lookup"><span data-stu-id="70a72-192">Creating a RolePoint test user</span></span>

<span data-ttu-id="70a72-193">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans RolePoint.</span><span class="sxs-lookup"><span data-stu-id="70a72-193">In this section, you create a user called Britta Simon in RolePoint.</span></span> <span data-ttu-id="70a72-194">Travaillez en collaboration avec l’[équipe de support RolePoint](mailto:info@rolepoint.com) afin d’ajouter les utilisateurs à la plateforme RolePoint.</span><span class="sxs-lookup"><span data-stu-id="70a72-194">Work with [RolePoint support team](mailto:info@rolepoint.com) to add the users in the RolePoint platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="70a72-195">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="70a72-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="70a72-196">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à RolePoint.</span><span class="sxs-lookup"><span data-stu-id="70a72-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RolePoint.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="70a72-198">**Pour affecter Britta Simon à RolePoint, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="70a72-198">**To assign Britta Simon to RolePoint, perform the following steps:**</span></span>

1. <span data-ttu-id="70a72-199">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="70a72-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="70a72-201">Dans la liste des applications, sélectionnez **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="70a72-201">In the applications list, select **RolePoint**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_app.png) 

3. <span data-ttu-id="70a72-203">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="70a72-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="70a72-205">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="70a72-205">Click **Add** button.</span></span> <span data-ttu-id="70a72-206">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="70a72-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="70a72-208">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="70a72-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="70a72-209">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="70a72-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="70a72-210">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="70a72-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="70a72-211">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="70a72-211">Testing single sign-on</span></span>

<span data-ttu-id="70a72-212">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="70a72-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="70a72-213">Quand vous cliquez sur la mosaïque RolePoint dans le volet d’accès, vous devez être connecté automatiquement à votre application RolePoint.</span><span class="sxs-lookup"><span data-stu-id="70a72-213">When you click the RolePoint tile in the Access Panel, you should get automatically signed-on to your RolePoint application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="70a72-214">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="70a72-214">Additional resources</span></span>

* [<span data-ttu-id="70a72-215">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70a72-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="70a72-216">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="70a72-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_203.png

