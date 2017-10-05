---
title: "Didacticiel : Intégration d’Azure Active Directory dans Dow Jones Factiva | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Dow Jones Factiva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b36e97e8-37a6-4096-a894-530427ee1331
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: dab48c24ff25fd68df1ee540bb8f0929e7e81bcb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dow-jones-factiva"></a><span data-ttu-id="cc09a-103">Didacticiel : Intégration d’Azure Active Directory dans Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="cc09a-103">Tutorial: Azure Active Directory integration with Dow Jones Factiva</span></span>

<span data-ttu-id="cc09a-104">Dans ce didacticiel, vous allez apprendre à intégrer Dow Jones Factiva à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc09a-104">In this tutorial, you learn how to integrate Dow Jones Factiva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc09a-105">L’intégration de Dow Jones Factiva dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="cc09a-105">Integrating Dow Jones Factiva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cc09a-106">Dans Azure AD, vous pouvez contrôler qui a accès à Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="cc09a-106">You can control in Azure AD who has access to Dow Jones Factiva</span></span>
- <span data-ttu-id="cc09a-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Dow Jones Factiva (par authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc09a-107">You can enable your users to automatically get signed-on to Dow Jones Factiva (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc09a-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="cc09a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cc09a-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cc09a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc09a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cc09a-110">Prerequisites</span></span>

<span data-ttu-id="cc09a-111">Pour configurer l’intégration d’Azure AD avec Dow Jones Factiva, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cc09a-111">To configure Azure AD integration with Dow Jones Factiva, you need the following items:</span></span>

- <span data-ttu-id="cc09a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc09a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc09a-113">Un abonnement Dow Jones Factiva avec authentification unique activée</span><span class="sxs-lookup"><span data-stu-id="cc09a-113">A Dow Jones Factiva single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc09a-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="cc09a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc09a-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="cc09a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc09a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="cc09a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc09a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc09a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc09a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="cc09a-118">Scenario description</span></span>
<span data-ttu-id="cc09a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="cc09a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc09a-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="cc09a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc09a-121">Ajout de Dow Jones Factiva à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="cc09a-121">Adding Dow Jones Factiva from the gallery</span></span>
2. <span data-ttu-id="cc09a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc09a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dow-jones-factiva-from-the-gallery"></a><span data-ttu-id="cc09a-123">Ajout de Dow Jones Factiva à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="cc09a-123">Adding Dow Jones Factiva from the gallery</span></span>
<span data-ttu-id="cc09a-124">Pour configurer l’intégration de Dow Jones Factiva avec Azure AD, vous devez ajouter Dow Jones Factiva, à partir de la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="cc09a-124">To configure the integration of Dow Jones Factiva into Azure AD, you need to add Dow Jones Factiva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cc09a-125">**Pour ajouter Dow Jones Factiva à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cc09a-125">**To add Dow Jones Factiva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cc09a-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cc09a-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cc09a-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="cc09a-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="cc09a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="cc09a-133">Dans la zone de recherche, saisissez **Dow Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-133">In the search box, type **Dow Jones Factiva**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_search.png)

5. <span data-ttu-id="cc09a-135">Dans le volet de résultats, sélectionnez **Dow Jones Factiva**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="cc09a-135">In the results panel, select **Dow Jones Factiva**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc09a-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc09a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc09a-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Dow Jones Factiva avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="cc09a-138">In this section, you configure and test Azure AD single sign-on with Dow Jones Factiva based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cc09a-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Dow Jones Factiva équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc09a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dow Jones Factiva is to a user in Azure AD.</span></span> <span data-ttu-id="cc09a-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Dow Jones Factiva associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="cc09a-140">In other words, a link relationship between an Azure AD user and the related user in Dow Jones Factiva needs to be established.</span></span>

<span data-ttu-id="cc09a-141">Dans Dow Jones Factiva, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="cc09a-141">In Dow Jones Factiva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cc09a-142">Pour configurer et tester l'authentification unique Azure AD avec Dow Jones Factiva, vous devez suivre les blocs élémentaires suivants :</span><span class="sxs-lookup"><span data-stu-id="cc09a-142">To configure and test Azure AD single sign-on with Dow Jones Factiva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cc09a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="cc09a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cc09a-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc09a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cc09a-145">**[Création d’un utilisateur de test Dow Jones Factiva](#creating-a-dow-jones-factiva-test-user)** pour avoir un équivalent de Britta Simon dans Dow Jones Factiva lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cc09a-145">**[Creating a Dow Jones Factiva test user](#creating-a-dow-jones-factiva-test-user)** - to have a counterpart of Britta Simon in Dow Jones Factiva that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cc09a-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc09a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cc09a-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="cc09a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc09a-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc09a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc09a-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="cc09a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dow Jones Factiva application.</span></span>

<span data-ttu-id="cc09a-150">**Pour configurer l’authentification unique Azure AD avec Dow Jones Factiva, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cc09a-150">**To configure Azure AD single sign-on with Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="cc09a-151">Dans le portail Azure, dans la page d’intégration de l’application **Dow Jones Factiva**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-151">In the Azure portal, on the **Dow Jones Factiva** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="cc09a-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="cc09a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_samlbase.png)

3. <span data-ttu-id="cc09a-155">Dans la section **Domaine et URL Dow Jones Factiva**, l’utilisateur n’a pas à effectuer les étapes, car l’application est déjà préintégrée à Azure.</span><span class="sxs-lookup"><span data-stu-id="cc09a-155">On the **Dow Jones Factiva Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_url.png)

4. <span data-ttu-id="cc09a-157">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cc09a-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_certificate.png) 

5. <span data-ttu-id="cc09a-159">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="cc09a-159">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cc09a-161">Pour configurer l’authentification unique côté **Dow Jones Factiva**, vous devez envoyer les **métadonnées XML** téléchargées à [l’équipe du support technique Dow Jones Factiva](https://www.dowjones.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="cc09a-161">To configure single sign-on on **Dow Jones Factiva** side, you need to send the downloaded **Metadata XML** to [Dow Jones Factiva support team](https://www.dowjones.com/contact/).</span></span> <span data-ttu-id="cc09a-162">Elle configure ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="cc09a-162">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="cc09a-163">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="cc09a-163">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cc09a-164">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="cc09a-164">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cc09a-165">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc09a-165">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc09a-166">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc09a-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc09a-167">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cc09a-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="cc09a-169">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cc09a-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cc09a-170">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cc09a-172">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cc09a-174">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="cc09a-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cc09a-176">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="cc09a-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc09a-178">a.</span><span class="sxs-lookup"><span data-stu-id="cc09a-178">a.</span></span> <span data-ttu-id="cc09a-179">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc09a-180">b.</span><span class="sxs-lookup"><span data-stu-id="cc09a-180">b.</span></span> <span data-ttu-id="cc09a-181">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc09a-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cc09a-182">c.</span><span class="sxs-lookup"><span data-stu-id="cc09a-182">c.</span></span> <span data-ttu-id="cc09a-183">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cc09a-184">d.</span><span class="sxs-lookup"><span data-stu-id="cc09a-184">d.</span></span> <span data-ttu-id="cc09a-185">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-185">Click **Create**.</span></span>
 
### <a name="creating-a-dow-jones-factiva-test-user"></a><span data-ttu-id="cc09a-186">Création d’un utilisateur de test Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="cc09a-186">Creating a Dow Jones Factiva test user</span></span>

<span data-ttu-id="cc09a-187">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="cc09a-187">In this section, you create a user called Britta Simon in Dow Jones Factiva.</span></span> <span data-ttu-id="cc09a-188">Collaborez avec [l’équipe du support technique Dow Jones Factiva](https://www.dowjones.com/contact/) pour ajouter les utilisateurs à la plateforme Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="cc09a-188">Please work with Dow [Jones Factiva support team](https://www.dowjones.com/contact/) to add the users in the Dow Jones Factiva platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cc09a-189">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="cc09a-189">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cc09a-190">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="cc09a-190">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dow Jones Factiva.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="cc09a-192">**Pour affecter Britta Simon à Dow Jones Factiva, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="cc09a-192">**To assign Britta Simon to Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="cc09a-193">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-193">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="cc09a-195">Dans la liste des applications, sélectionnez **Dow Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-195">In the applications list, select **Dow Jones Factiva**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_app.png) 

3. <span data-ttu-id="cc09a-197">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-197">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="cc09a-199">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-199">Click **Add** button.</span></span> <span data-ttu-id="cc09a-200">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-200">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="cc09a-202">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cc09a-202">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cc09a-203">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-203">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cc09a-204">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="cc09a-204">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc09a-205">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="cc09a-205">Testing single sign-on</span></span>

<span data-ttu-id="cc09a-206">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="cc09a-206">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cc09a-207">Lorsque vous cliquez sur la mosaïque Dow Jones Factiva dans le volet d'accès, vous êtes connecté automatiquement à votre application Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="cc09a-207">When you click the Dow Jones Factiva tile in the Access Panel, you should get automatically signed-on to your Dow Jones Factiva application.</span></span>
<span data-ttu-id="cc09a-208">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cc09a-208">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cc09a-209">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="cc09a-209">Additional resources</span></span>

* [<span data-ttu-id="cc09a-210">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc09a-210">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cc09a-211">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="cc09a-211">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_203.png

