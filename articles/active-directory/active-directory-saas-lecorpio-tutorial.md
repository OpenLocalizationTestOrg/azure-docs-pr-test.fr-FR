---
title: "Didacticiel : Intégration d’Azure Active Directory à Lecorpio | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Lecorpio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 35c94e2d9d8a938971f85ea732a74a7e1655545e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a><span data-ttu-id="cc330-103">Didacticiel : Intégration d’Azure Active Directory à Lecorpio</span><span class="sxs-lookup"><span data-stu-id="cc330-103">Tutorial: Azure Active Directory integration with Lecorpio</span></span>

<span data-ttu-id="cc330-104">Dans ce didacticiel, vous allez apprendre à intégrer Lecorpio à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc330-104">In this tutorial, you learn how to integrate Lecorpio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc330-105">L’intégration de Lecorpio à Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="cc330-105">Integrating Lecorpio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cc330-106">Dans Azure AD, vous pouvez contrôler qui a accès à Lecorpio</span><span class="sxs-lookup"><span data-stu-id="cc330-106">You can control in Azure AD who has access to Lecorpio</span></span>
- <span data-ttu-id="cc330-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Lecorpio (via l’authentification unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc330-107">You can enable your users to automatically get signed-on to Lecorpio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc330-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="cc330-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cc330-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc330-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc330-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="cc330-110">Prerequisites</span></span>

<span data-ttu-id="cc330-111">Pour configurer l’intégration d’Azure AD à Lecorpio, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cc330-111">To configure Azure AD integration with Lecorpio, you need the following items:</span></span>

- <span data-ttu-id="cc330-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc330-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc330-113">Un abonnement Lecorpio pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="cc330-113">A Lecorpio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc330-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="cc330-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc330-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="cc330-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc330-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="cc330-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc330-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc330-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc330-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="cc330-118">Scenario description</span></span>
<span data-ttu-id="cc330-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="cc330-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc330-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="cc330-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc330-121">Ajout de Lecorpio à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="cc330-121">Adding Lecorpio from the gallery</span></span>
2. <span data-ttu-id="cc330-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc330-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lecorpio-from-the-gallery"></a><span data-ttu-id="cc330-123">Ajout de Lecorpio à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="cc330-123">Adding Lecorpio from the gallery</span></span>
<span data-ttu-id="cc330-124">Pour configurer l’intégration de Lecorpio à Azure AD, vous devez ajouter Lecorpio à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="cc330-124">To configure the integration of Lecorpio into Azure AD, you need to add Lecorpio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cc330-125">**Pour ajouter Lecorpio à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="cc330-125">**To add Lecorpio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cc330-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cc330-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cc330-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="cc330-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cc330-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cc330-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="cc330-131">Cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="cc330-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="cc330-133">Dans la zone de recherche, tapez **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="cc330-133">In the search box, type **Lecorpio**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_search.png)

5. <span data-ttu-id="cc330-135">Dans le volet de résultats, sélectionnez **Lecorpio**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="cc330-135">In the results panel, select **Lecorpio**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc330-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc330-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc330-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Lecorpio pour un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="cc330-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cc330-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Lecorpio équivalent à un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc330-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Lecorpio is to a user in Azure AD.</span></span> <span data-ttu-id="cc330-140">En d’autres termes, une relation doit être établie entre un utilisateur Azure AD et l’utilisateur associé dans Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="cc330-140">In other words, a link relationship between an Azure AD user and the related user in Lecorpio needs to be established.</span></span>

<span data-ttu-id="cc330-141">Pour cela, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** dans Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="cc330-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Lecorpio.</span></span>

<span data-ttu-id="cc330-142">Pour configurer et tester l’authentification unique Azure AD avec Lecorpio, vous devez effectuer les actions essentielles suivantes :</span><span class="sxs-lookup"><span data-stu-id="cc330-142">To configure and test Azure AD single sign-on with Lecorpio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cc330-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="cc330-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cc330-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc330-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc330-145">**[Création d’un utilisateur de test Lecorpio](#creating-a-lecorpio-test-user)** pour avoir un équivalent de Britta Simon dans Lecorpio lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cc330-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - to have a counterpart of Britta Simon in Lecorpio that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc330-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc330-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc330-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="cc330-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc330-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc330-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc330-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="cc330-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Lecorpio application.</span></span>

<span data-ttu-id="cc330-150">**Pour configurer l’authentification unique Azure AD avec Lecorpio, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="cc330-150">**To configure Azure AD single sign-on with Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="cc330-151">Dans le portail Azure, sur la page d’intégration de l’application **Lecorpio**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="cc330-151">In the Azure portal, on the **Lecorpio** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="cc330-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cc330-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

3. <span data-ttu-id="cc330-155">Dans la section **Domaine et URL Lecorpio**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cc330-155">On the **Lecorpio Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_url.png)

    <span data-ttu-id="cc330-157">a.</span><span class="sxs-lookup"><span data-stu-id="cc330-157">a.</span></span> <span data-ttu-id="cc330-158">Dans la zone de texte **URL de connexion**, tapez la valeur au format suivant : `https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="cc330-158">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    <span data-ttu-id="cc330-159">b.</span><span class="sxs-lookup"><span data-stu-id="cc330-159">b.</span></span> <span data-ttu-id="cc330-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="cc330-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cc330-161">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="cc330-161">These values are not the real.</span></span> <span data-ttu-id="cc330-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="cc330-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="cc330-163">Nous vous suggérons d’utiliser ici la valeur de chaîne unique dans l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="cc330-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="cc330-164">Pour obtenir ces valeurs, contactez l’[équipe de support technique Lecorpio](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="cc330-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to get these values.</span></span> 
 
4. <span data-ttu-id="cc330-165">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cc330-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

5. <span data-ttu-id="cc330-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="cc330-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lecorpio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cc330-169">Pour configurer l’authentification unique côté **Lecorpio**, vous devez envoyer le fichier **XML des métadonnées** téléchargé à l’[équipe de support technique Lecorpio](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="cc330-169">To configure single sign-on on **Lecorpio** side, you need to send the downloaded **Metadata XML** to [Lecorpio support team](mailto:info@lecorpio.com).</span></span>

> [!TIP]
> <span data-ttu-id="cc330-170">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="cc330-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cc330-171">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="cc330-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cc330-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc330-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc330-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc330-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc330-174">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cc330-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="cc330-176">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cc330-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cc330-177">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cc330-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cc330-179">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cc330-179">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cc330-181">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="cc330-181">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cc330-183">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="cc330-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc330-185">a.</span><span class="sxs-lookup"><span data-stu-id="cc330-185">a.</span></span> <span data-ttu-id="cc330-186">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc330-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc330-187">b.</span><span class="sxs-lookup"><span data-stu-id="cc330-187">b.</span></span> <span data-ttu-id="cc330-188">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc330-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cc330-189">c.</span><span class="sxs-lookup"><span data-stu-id="cc330-189">c.</span></span> <span data-ttu-id="cc330-190">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="cc330-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cc330-191">d.</span><span class="sxs-lookup"><span data-stu-id="cc330-191">d.</span></span> <span data-ttu-id="cc330-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc330-192">Click **Create**.</span></span>
 
### <a name="creating-a-lecorpio-test-user"></a><span data-ttu-id="cc330-193">Création d’un utilisateur de test Lecorpio</span><span class="sxs-lookup"><span data-stu-id="cc330-193">Creating a Lecorpio test user</span></span>

<span data-ttu-id="cc330-194">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="cc330-194">In this section, you create a user called Britta Simon in Lecorpio.</span></span> 

<span data-ttu-id="cc330-195">Contactez l’[équipe de support technique Lecorpio](mailto:info@lecorpio.com) pour ajouter des utilisateurs dans l’application Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="cc330-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) to add the users in the Lecorpio application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cc330-196">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc330-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cc330-197">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en accordant l’accès à Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="cc330-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Lecorpio.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="cc330-199">**Pour affecter Britta Simon à Lecorpio, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="cc330-199">**To assign Britta Simon to Lecorpio, perform the following steps:**</span></span>

1. <span data-ttu-id="cc330-200">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cc330-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="cc330-202">Dans la liste des applications, sélectionnez **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="cc330-202">In the applications list, select **Lecorpio**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_app.png) 

3. <span data-ttu-id="cc330-204">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cc330-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="cc330-206">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="cc330-206">Click **Add** button.</span></span> <span data-ttu-id="cc330-207">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cc330-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="cc330-209">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cc330-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cc330-210">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cc330-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc330-211">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cc330-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc330-212">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="cc330-212">Testing single sign-on</span></span>

<span data-ttu-id="cc330-213">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="cc330-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cc330-214">Quand vous cliquez sur la mosaïque Lecorpio dans le volet d’accès, vous devez être automatiquement connecté à votre application Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="cc330-214">When you click the Lecorpio tile in the Access Panel, you should get automatically signed-on to your Lecorpio application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc330-215">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="cc330-215">Additional resources</span></span>

* [<span data-ttu-id="cc330-216">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc330-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc330-217">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="cc330-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_203.png

