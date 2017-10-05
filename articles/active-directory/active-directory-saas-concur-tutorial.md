---
title: "Didacticiel : Intégration d’Azure Active Directory à Concur | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 0b44437b3dcf69dae3587529da7d12e7809b9f55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="16541-103">Didacticiel : Intégration d’Azure Active Directory à Concur</span><span class="sxs-lookup"><span data-stu-id="16541-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="16541-104">Dans ce didacticiel, vous allez apprendre à intégrer Concur à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="16541-104">In this tutorial, you learn how to integrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="16541-105">L’intégration de Concur à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="16541-105">Integrating Concur with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="16541-106">Dans Azure AD, vous pouvez contrôler qui a accès à Concur.</span><span class="sxs-lookup"><span data-stu-id="16541-106">You can control in Azure AD who has access to Concur</span></span>
- <span data-ttu-id="16541-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Concur (par l’intermédiaire de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16541-107">You can enable your users to automatically get signed-on to Concur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="16541-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="16541-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="16541-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="16541-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16541-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="16541-110">Prerequisites</span></span>

<span data-ttu-id="16541-111">Pour configurer l’intégration d’Azure AD avec Concur, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="16541-111">To configure Azure AD integration with Concur, you need the following items:</span></span>

- <span data-ttu-id="16541-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="16541-112">An Azure AD subscription</span></span>
- <span data-ttu-id="16541-113">Un abonnement Concur pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="16541-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="16541-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="16541-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="16541-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="16541-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="16541-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="16541-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="16541-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="16541-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="16541-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="16541-118">Scenario description</span></span>
<span data-ttu-id="16541-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="16541-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="16541-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="16541-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="16541-121">Ajout de Concur à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="16541-121">Adding Concur from the gallery</span></span>
2. <span data-ttu-id="16541-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="16541-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="16541-123">La configuration de votre abonnement Concur pour l’authentification unique fédérée par le biais de SAML constitue une tâche séparée qui doit être effectuée par l’[équipe de support technique Concur](https://www.concur.co.in/contact) à votre demande.</span><span class="sxs-lookup"><span data-stu-id="16541-123">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 

## <a name="adding-concur-from-the-gallery"></a><span data-ttu-id="16541-124">Ajout de Concur à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="16541-124">Adding Concur from the gallery</span></span>
<span data-ttu-id="16541-125">Pour configurer l’intégration de Concur avec Azure AD, vous devez ajouter Concur dans la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="16541-125">To configure the integration of Concur into Azure AD, you need to add Concur from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="16541-126">**Pour ajouter Concur à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="16541-126">**To add Concur from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="16541-127">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16541-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="16541-129">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="16541-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="16541-130">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="16541-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="16541-132">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="16541-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="16541-134">Dans la zone de recherche, tapez **Concur**.</span><span class="sxs-lookup"><span data-stu-id="16541-134">In the search box, type **Concur**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="16541-136">Dans le volet de résultats, sélectionnez **Concur**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="16541-136">In the results panel, select **Concur**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="16541-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="16541-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="16541-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Concur avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="16541-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="16541-140">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Concur équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16541-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Concur is to a user in Azure AD.</span></span> <span data-ttu-id="16541-141">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Concur associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="16541-141">In other words, a link relationship between an Azure AD user and the related user in Concur needs to be established.</span></span>

<span data-ttu-id="16541-142">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Nom d’utilisateur** dans Concur.</span><span class="sxs-lookup"><span data-stu-id="16541-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Concur.</span></span>

<span data-ttu-id="16541-143">Pour configurer et tester l’authentification unique Azure AD avec Concur, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="16541-143">To configure and test Azure AD single sign-on with Concur, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="16541-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="16541-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="16541-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16541-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="16541-146">**[Création d’un utilisateur de test Concur](#creating-a-concur-test-user)** pour avoir un équivalent de Britta Simon dans Concur lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="16541-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - to have a counterpart of Britta Simon in Concur that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="16541-147">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16541-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="16541-148">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="16541-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="16541-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="16541-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="16541-150">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Concur.</span><span class="sxs-lookup"><span data-stu-id="16541-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="16541-151">**Pour configurer l’authentification unique Azure AD avec Concur, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="16541-151">**To configure Azure AD single sign-on with Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="16541-152">Dans le portail Azure, dans la page d’intégration de l’application **Concur**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="16541-152">In the Azure portal, on the **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="16541-154">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="16541-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="16541-156">Dans la section **Domaine et URL Concur**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="16541-156">On the **Concur Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="16541-158">a.</span><span class="sxs-lookup"><span data-stu-id="16541-158">a.</span></span> <span data-ttu-id="16541-159">Dans la zone de texte **URL de connexion**, tapez la valeur au format suivant : `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="16541-159">In the **Sign on URL** textbox, type the value using the following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="16541-160">b.</span><span class="sxs-lookup"><span data-stu-id="16541-160">b.</span></span> <span data-ttu-id="16541-161">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="16541-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="16541-162">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="16541-162">These values are not the real.</span></span> <span data-ttu-id="16541-163">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="16541-163">Update these values with the actual Sign on URL and Identifier.</span></span> <span data-ttu-id="16541-164">Pour obtenir ces valeurs, contactez l’[équipe de support technique Concur](https://www.concur.co.in/contact).</span><span class="sxs-lookup"><span data-stu-id="16541-164">Contact [Concur Client support team](https://www.concur.co.in/contact) to get these values.</span></span> 

4. <span data-ttu-id="16541-165">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="16541-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="16541-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="16541-167">Click **Save** button.</span></span>

    <span data-ttu-id="16541-168">![Configurer l’authentification unique](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="16541-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="16541-169">Pour configurer l’authentification unique du côté **Concur**, vous devez envoyer le **XML de métadonnées** téléchargé aux techniciens du support technique Concur.</span><span class="sxs-lookup"><span data-stu-id="16541-169">To configure single sign-on on **Concur** side, you need to send the downloaded **Metadata XML** to Concur support.</span></span> <span data-ttu-id="16541-170">Ils configurent ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="16541-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="16541-171">La configuration de votre abonnement Concur pour l’authentification unique fédérée par le biais de SAML constitue une tâche séparée qui doit être effectuée par l’[équipe de support technique Concur](https://www.concur.co.in/contact) à votre demande.</span><span class="sxs-lookup"><span data-stu-id="16541-171">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="16541-172">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="16541-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="16541-173">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="16541-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="16541-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="16541-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="16541-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="16541-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="16541-176">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="16541-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="16541-178">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="16541-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="16541-179">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="16541-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="16541-181">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="16541-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="16541-183">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="16541-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="16541-185">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="16541-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="16541-187">a.</span><span class="sxs-lookup"><span data-stu-id="16541-187">a.</span></span> <span data-ttu-id="16541-188">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="16541-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="16541-189">b.</span><span class="sxs-lookup"><span data-stu-id="16541-189">b.</span></span> <span data-ttu-id="16541-190">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="16541-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="16541-191">c.</span><span class="sxs-lookup"><span data-stu-id="16541-191">c.</span></span> <span data-ttu-id="16541-192">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="16541-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="16541-193">d.</span><span class="sxs-lookup"><span data-stu-id="16541-193">d.</span></span> <span data-ttu-id="16541-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="16541-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="16541-195">Création d’un utilisateur de test Concur</span><span class="sxs-lookup"><span data-stu-id="16541-195">Creating a Concur test user</span></span>

<span data-ttu-id="16541-196">L’application prend en charge l’approvisionnement d’utilisateur juste-à-temps, et après authentification, les utilisateurs sont créés automatiquement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="16541-196">Application supports the Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="16541-197">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="16541-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="16541-198">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Concur.</span><span class="sxs-lookup"><span data-stu-id="16541-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Concur.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="16541-200">**Pour affecter Britta Simon à Concur, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="16541-200">**To assign Britta Simon to Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="16541-201">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="16541-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="16541-203">Dans la liste des applications, sélectionnez **Concur**.</span><span class="sxs-lookup"><span data-stu-id="16541-203">In the applications list, select **Concur**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="16541-205">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="16541-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="16541-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="16541-207">Click **Add** button.</span></span> <span data-ttu-id="16541-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="16541-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="16541-210">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="16541-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="16541-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="16541-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="16541-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="16541-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="16541-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="16541-213">Testing single sign-on</span></span>

<span data-ttu-id="16541-214">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="16541-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="16541-215">Quand vous cliquez sur la mosaïque Concur dans le panneau d’accès, la page de connexion de l’application Concur doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="16541-215">When you click the Concur tile in the Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="16541-216">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="16541-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="16541-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="16541-217">Additional resources</span></span>

* [<span data-ttu-id="16541-218">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="16541-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="16541-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="16541-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="16541-220">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="16541-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png

