---
title: "Didacticiel : Intégration d’Azure Active Directory à 15Five | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et 15Five."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: ea36774747a0fcfa4ace1aefb2d46dba815d92c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="06671-103">Didacticiel : Intégration d’Azure Active Directory à 15Five</span><span class="sxs-lookup"><span data-stu-id="06671-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="06671-104">Dans ce didacticiel, vous allez apprendre à intégrer 15Five dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="06671-104">In this tutorial, you learn how to integrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="06671-105">L’intégration de 15Five dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="06671-105">Integrating 15Five with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="06671-106">Dans Azure AD, vous pouvez contrôler qui a accès à 15Five</span><span class="sxs-lookup"><span data-stu-id="06671-106">You can control in Azure AD who has access to 15Five</span></span>
- <span data-ttu-id="06671-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à 15Five (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="06671-107">You can enable your users to automatically get signed-on to 15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="06671-108">Vous pouvez gérer vos comptes depuis un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="06671-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="06671-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="06671-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06671-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="06671-110">Prerequisites</span></span>

<span data-ttu-id="06671-111">Pour configurer l’intégration d’Azure AD avec 15Five, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="06671-111">To configure Azure AD integration with 15Five, you need the following items:</span></span>

- <span data-ttu-id="06671-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="06671-112">An Azure AD subscription</span></span>
- <span data-ttu-id="06671-113">Un abonnement 15Five pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="06671-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="06671-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="06671-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="06671-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="06671-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="06671-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="06671-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="06671-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="06671-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="06671-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="06671-118">Scenario description</span></span>
<span data-ttu-id="06671-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="06671-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="06671-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="06671-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="06671-121">Ajout de 15Five à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="06671-121">Adding 15Five from the gallery</span></span>
2. <span data-ttu-id="06671-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="06671-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-the-gallery"></a><span data-ttu-id="06671-123">Ajout de 15Five à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="06671-123">Adding 15Five from the gallery</span></span>
<span data-ttu-id="06671-124">Pour configurer l’intégration de 15Five dans Azure AD, vous devez ajouter 15Five à partir de la galerie dans votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="06671-124">To configure the integration of 15Five into Azure AD, you need to add 15Five from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="06671-125">**Pour ajouter 15Five à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="06671-125">**To add 15Five from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="06671-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="06671-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="06671-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="06671-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="06671-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="06671-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="06671-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="06671-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="06671-133">Dans la zone de recherche, tapez **15Five**.</span><span class="sxs-lookup"><span data-stu-id="06671-133">In the search box, type **15Five**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="06671-135">Dans le volet de résultats, sélectionnez **15Five**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="06671-135">In the results panel, select **15Five**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="06671-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="06671-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="06671-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec 15Five, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="06671-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="06671-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur 15Five correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06671-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 15Five is to a user in Azure AD.</span></span> <span data-ttu-id="06671-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur 15Five associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="06671-140">In other words, a link relationship between an Azure AD user and the related user in 15Five needs to be established.</span></span>

<span data-ttu-id="06671-141">Dans 15Five, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="06671-141">In 15Five, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="06671-142">Pour configurer et tester l’authentification unique Azure AD avec 15Five, vous devez vous conformer aux indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="06671-142">To configure and test Azure AD single sign-on with 15Five, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="06671-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="06671-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="06671-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="06671-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="06671-145">**[Création d’un utilisateur de test 15Five](#creating-a-15five-test-user)** pour avoir un équivalent de Britta Simon dans 15Five lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="06671-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - to have a counterpart of Britta Simon in 15Five that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="06671-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06671-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="06671-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="06671-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="06671-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="06671-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="06671-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application 15Five.</span><span class="sxs-lookup"><span data-stu-id="06671-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="06671-150">**Pour configurer l’authentification unique Azure AD avec 15Five, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="06671-150">**To configure Azure AD single sign-on with 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="06671-151">Dans le portail Azure, sur la page d’intégration de l’application **15Five**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="06671-151">In the Azure portal, on the **15Five** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="06671-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="06671-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="06671-155">Dans la section **Domaine et URL 15Five**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="06671-155">On the **15Five Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="06671-157">a.</span><span class="sxs-lookup"><span data-stu-id="06671-157">a.</span></span> <span data-ttu-id="06671-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.15five.com`</span><span class="sxs-lookup"><span data-stu-id="06671-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="06671-159">b.</span><span class="sxs-lookup"><span data-stu-id="06671-159">b.</span></span> <span data-ttu-id="06671-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.15five.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="06671-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="06671-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="06671-161">These values are not real.</span></span> <span data-ttu-id="06671-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="06671-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="06671-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique 15Five](https://www.15five.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="06671-163">Contact [15Five Client support team](https://www.15five.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="06671-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="06671-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="06671-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="06671-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="06671-168">Pour configurer l’authentification unique du côté **15Five**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à [l’équipe de support technique de 15Five](https://www.15five.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="06671-168">To configure single sign-on on **15Five** side, you need to send the downloaded **Metadata XML** to [15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="06671-169">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="06671-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="06671-170">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="06671-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="06671-171">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="06671-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="06671-172">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="06671-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="06671-173">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="06671-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="06671-175">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="06671-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="06671-176">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="06671-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="06671-178">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="06671-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="06671-180">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="06671-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="06671-182">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="06671-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="06671-184">a.</span><span class="sxs-lookup"><span data-stu-id="06671-184">a.</span></span> <span data-ttu-id="06671-185">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="06671-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="06671-186">b.</span><span class="sxs-lookup"><span data-stu-id="06671-186">b.</span></span> <span data-ttu-id="06671-187">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="06671-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="06671-188">c.</span><span class="sxs-lookup"><span data-stu-id="06671-188">c.</span></span> <span data-ttu-id="06671-189">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="06671-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="06671-190">d.</span><span class="sxs-lookup"><span data-stu-id="06671-190">d.</span></span> <span data-ttu-id="06671-191">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="06671-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="06671-192">Création d’un utilisateur de test 15Five</span><span class="sxs-lookup"><span data-stu-id="06671-192">Creating a 15Five test user</span></span>

<span data-ttu-id="06671-193">Pour se connecter à 15Five, les utilisateurs d’Azure AD doivent être approvisionnés dans 15Five.</span><span class="sxs-lookup"><span data-stu-id="06671-193">To enable Azure AD users to log in to 15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="06671-194">Dans le cas de 15Five, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="06671-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="06671-195">Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="06671-195">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="06671-196">Connectez-vous à votre site d’entreprise **15Five** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="06671-196">Log in to your **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="06671-197">Accédez à **Manage Company**.</span><span class="sxs-lookup"><span data-stu-id="06671-197">Go to **Manage Company**.</span></span>
   
    <span data-ttu-id="06671-198">![Gérer l’entreprise](./media/active-directory-saas-15five-tutorial/IC784675.png "Gérer l’entreprise")</span><span class="sxs-lookup"><span data-stu-id="06671-198">![Manage Company](./media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="06671-199">Accédez à **Contacts \> Ajouter des personnes**.</span><span class="sxs-lookup"><span data-stu-id="06671-199">Go to **People \> Add People**.</span></span>
   
    <span data-ttu-id="06671-200">![Personnes](./media/active-directory-saas-15five-tutorial/IC784676.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="06671-200">![People](./media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="06671-201">Dans la section Add New Person, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="06671-201">In the Add New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="06671-202">![Ajouter une nouvelle personne](./media/active-directory-saas-15five-tutorial/IC784677.png "Ajouter une nouvelle personne")</span><span class="sxs-lookup"><span data-stu-id="06671-202">![Add New Person](./media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="06671-203">a.</span><span class="sxs-lookup"><span data-stu-id="06671-203">a.</span></span> <span data-ttu-id="06671-204">Tapez le **prénom**, le **nom**, la **fonction** et **l’adresse de messagerie** du compte Azure Active Directory valide que vous souhaitez approvisionner dans les zones de texte correspondantes.</span><span class="sxs-lookup"><span data-stu-id="06671-204">Type the **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="06671-205">b.</span><span class="sxs-lookup"><span data-stu-id="06671-205">b.</span></span> <span data-ttu-id="06671-206">Cliquez sur **Done**.</span><span class="sxs-lookup"><span data-stu-id="06671-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="06671-207">Le titulaire du compte Azure AD reçoit alors un e-mail contenant un lien pour confirmer le compte avant qu’il ne soit activé.</span><span class="sxs-lookup"><span data-stu-id="06671-207">The Azure AD account holder receives an email including a link to confirm the account before it becomes active.</span></span>
   
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="06671-208">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="06671-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="06671-209">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à 15Five.</span><span class="sxs-lookup"><span data-stu-id="06671-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 15Five.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="06671-211">**Pour assigner Britta Simon à 15Five, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="06671-211">**To assign Britta Simon to 15Five, perform the following steps:**</span></span>

1. <span data-ttu-id="06671-212">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="06671-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="06671-214">Dans la liste des applications, sélectionnez **15Five**.</span><span class="sxs-lookup"><span data-stu-id="06671-214">In the applications list, select **15Five**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="06671-216">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="06671-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="06671-218">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="06671-218">Click **Add** button.</span></span> <span data-ttu-id="06671-219">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="06671-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="06671-221">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="06671-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="06671-222">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="06671-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="06671-223">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="06671-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="06671-224">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="06671-224">Testing single sign-on</span></span>

<span data-ttu-id="06671-225">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="06671-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="06671-226">Lorsque vous cliquez sur la mosaïque 15Five dans le panneau d’accès, la page de connexion de l’application 15Five doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="06671-226">When you click the 15Five tile in the Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="06671-227">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="06671-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="06671-228">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="06671-228">Additional resources</span></span>

* [<span data-ttu-id="06671-229">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="06671-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="06671-230">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="06671-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png

