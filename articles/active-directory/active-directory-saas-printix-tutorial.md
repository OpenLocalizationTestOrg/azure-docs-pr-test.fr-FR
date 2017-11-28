---
title: "Didacticiel : Intégration d’Azure Active Directory à Printix | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Printix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 97dbb3fa0531f2f679badb6bb9752f2e42fc9cb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="46644-103">Didacticiel : Intégration d’Azure Active Directory à Printix</span><span class="sxs-lookup"><span data-stu-id="46644-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="46644-104">Dans ce didacticiel, vous allez apprendre à intégrer Printix à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="46644-104">In this tutorial, you learn how to integrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="46644-105">L’intégration de Printix à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="46644-105">Integrating Printix with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="46644-106">Dans Azure AD, vous pouvez contrôler qui a accès à Printix.</span><span class="sxs-lookup"><span data-stu-id="46644-106">You can control in Azure AD who has access to Printix</span></span>
- <span data-ttu-id="46644-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Printix (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46644-107">You can enable your users to automatically get signed-on to Printix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="46644-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="46644-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="46644-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="46644-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46644-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="46644-110">Prerequisites</span></span>

<span data-ttu-id="46644-111">Pour configurer l’intégration d’Azure AD à Printix, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="46644-111">To configure Azure AD integration with Printix, you need the following items:</span></span>

- <span data-ttu-id="46644-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="46644-112">An Azure AD subscription</span></span>
- <span data-ttu-id="46644-113">Un abonnement Printix pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="46644-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="46644-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="46644-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="46644-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="46644-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="46644-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="46644-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="46644-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="46644-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="46644-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="46644-118">Scenario description</span></span>
<span data-ttu-id="46644-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="46644-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="46644-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="46644-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="46644-121">Ajout de Printix à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="46644-121">Adding Printix from the gallery</span></span>
2. <span data-ttu-id="46644-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="46644-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-the-gallery"></a><span data-ttu-id="46644-123">Ajout de Printix à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="46644-123">Adding Printix from the gallery</span></span>
<span data-ttu-id="46644-124">Pour configurer l’intégration de Printix à Azure AD, vous devez ajouter Printix à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="46644-124">To configure the integration of Printix into Azure AD, you need to add Printix from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="46644-125">**Pour ajouter Printix à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="46644-125">**To add Printix from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="46644-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46644-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="46644-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="46644-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="46644-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="46644-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="46644-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="46644-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="46644-133">Dans la zone de recherche, tapez **Printix**.</span><span class="sxs-lookup"><span data-stu-id="46644-133">In the search box, type **Printix**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_search.png)

5. <span data-ttu-id="46644-135">Dans le panneau des résultats, sélectionnez **Printix**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="46644-135">In the results panel, select **Printix**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="46644-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="46644-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="46644-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Printix avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="46644-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="46644-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Printix équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46644-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Printix is to a user in Azure AD.</span></span> <span data-ttu-id="46644-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Printix associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="46644-140">In other words, a link relationship between an Azure AD user and the related user in Printix needs to be established.</span></span>

<span data-ttu-id="46644-141">Dans Printix, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="46644-141">In Printix, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="46644-142">Pour configurer et tester l’authentification unique Azure AD avec Printix, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="46644-142">To configure and test Azure AD single sign-on with Printix, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="46644-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="46644-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="46644-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="46644-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="46644-145">**[Création d’un utilisateur de test Printix](#creating-a-printix-test-user)** pour obtenir un équivalent de Britta Simon dans Printix lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="46644-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - to have a counterpart of Britta Simon in Printix that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="46644-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="46644-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="46644-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="46644-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="46644-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="46644-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="46644-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Printix.</span><span class="sxs-lookup"><span data-stu-id="46644-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="46644-150">**Pour configurer l’authentification unique Azure AD avec Printix, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="46644-150">**To configure Azure AD single sign-on with Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="46644-151">Dans le Portail Azure, sur la page d’intégration de l’application **Printix**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="46644-151">In the Azure portal, on the **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="46644-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="46644-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_samlbase.png)

3. <span data-ttu-id="46644-155">Dans la section **Domaine et URL Printix**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="46644-155">On the **Printix Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="46644-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="46644-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="46644-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="46644-158">The value is not real.</span></span> <span data-ttu-id="46644-159">Mettez à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="46644-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="46644-160">Pour obtenir cette valeur, contactez l’[équipe du support technique Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="46644-160">Contact [Printix Client support team](mailto:support@printix.net) to get the value.</span></span> 
 
4. <span data-ttu-id="46644-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="46644-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_certificate.png) 

5. <span data-ttu-id="46644-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="46644-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="46644-165">Connectez-vous à votre client Printix en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="46644-165">Sign-on to your Printix tenant as an administrator.</span></span>

7. <span data-ttu-id="46644-166">Dans le menu situé en haut, cliquez sur l’icône dans le coin supérieur droit et sélectionnez**Authentification**(Authentification).</span><span class="sxs-lookup"><span data-stu-id="46644-166">In the menu on the top, click the icon at the upper right corner and select "**Authentication**".</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_06.png)

8. <span data-ttu-id="46644-168">Sous l’onglet **Setup** (Configuration), sélectionnez **Enable Azure/Office 365 authentication** (Activer l’authentification Azure/Office 365).</span><span class="sxs-lookup"><span data-stu-id="46644-168">On the **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_07.png)

9. <span data-ttu-id="46644-170">Sous l’onglet **Azure**, entrez l’URL des métadonnées de fédération dans la zone de texte **Federation metadata document** (Document de métadonnées de fédération).</span><span class="sxs-lookup"><span data-stu-id="46644-170">On the **Azure** tab, input federation metadata URL to the textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="46644-171">Envoyez le fichier XML de métadonnées que vous avez téléchargé sur Azure AD à [l’équipe de support Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="46644-171">Attach the metadata xml file which you downloaded from Azure AD to [Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="46644-172">Elle charge alors le fichier XML et vous fournit une URL des métadonnées de fédération.</span><span class="sxs-lookup"><span data-stu-id="46644-172">Then they upload the xml file and provide a federation metadata URL.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_08.png)
   
10. <span data-ttu-id="46644-174">Cliquez sur le bouton **Test**, puis sur le bouton **OK** si le test a réussi.</span><span class="sxs-lookup"><span data-stu-id="46644-174">Click the "**Test**" button and click "**OK**" button if the test was successful.</span></span>
   
     <span data-ttu-id="46644-175">La page Azure Active Directory s’affiche après que vous avez cliqué sur le bouton **Test**.</span><span class="sxs-lookup"><span data-stu-id="46644-175">Azure active directory page will show after clicking the **test** button.</span></span> <span data-ttu-id="46644-176">Le message « Test réussi » signifie qu’après avoir entré les informations d’identification de votre compte test Azure, le message « Paramètres testés correctement » s’affiche. Cliquez alors sur le bouton **OK**.</span><span class="sxs-lookup"><span data-stu-id="46644-176">"The test was successful" here means after entering the credentials of your Azure test account it will pop up a message "Settings tested OK".Then click the **OK** button.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_09.png)

11. <span data-ttu-id="46644-178">Cliquez sur le bouton **Save** (Enregistrer) dans la page **Authentication** (Authentification).</span><span class="sxs-lookup"><span data-stu-id="46644-178">Click the **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="46644-179">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="46644-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="46644-180">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="46644-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="46644-181">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="46644-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="46644-182">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="46644-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="46644-183">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="46644-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="46644-185">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="46644-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="46644-186">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="46644-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="46644-188">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="46644-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="46644-190">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="46644-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="46644-192">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="46644-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="46644-194">a.</span><span class="sxs-lookup"><span data-stu-id="46644-194">a.</span></span> <span data-ttu-id="46644-195">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="46644-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="46644-196">b.</span><span class="sxs-lookup"><span data-stu-id="46644-196">b.</span></span> <span data-ttu-id="46644-197">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="46644-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="46644-198">c.</span><span class="sxs-lookup"><span data-stu-id="46644-198">c.</span></span> <span data-ttu-id="46644-199">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="46644-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="46644-200">d.</span><span class="sxs-lookup"><span data-stu-id="46644-200">d.</span></span> <span data-ttu-id="46644-201">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="46644-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="46644-202">Création d’un utilisateur de test Printix</span><span class="sxs-lookup"><span data-stu-id="46644-202">Creating a Printix test user</span></span>

<span data-ttu-id="46644-203">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Printix.</span><span class="sxs-lookup"><span data-stu-id="46644-203">The objective of this section is to create a user called Britta Simon in Printix.</span></span> <span data-ttu-id="46644-204">Printix prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="46644-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="46644-205">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="46644-205">There is no action item for you in this section.</span></span> <span data-ttu-id="46644-206">Un nouvel utilisateur est créé lors d’une tentative d’accès à Printix, s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="46644-206">A new user is created during an attempt to access Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="46644-207">Si vous devez créer un utilisateur manuellement, contactez [l’équipe de support Printix](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="46644-207">If you need to create a user manually, you need to contact the [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="46644-208">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="46644-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="46644-209">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Printix.</span><span class="sxs-lookup"><span data-stu-id="46644-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Printix.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="46644-211">**Pour affecter Britta Simon à Printix, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="46644-211">**To assign Britta Simon to Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="46644-212">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="46644-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="46644-214">Dans la liste des applications, sélectionnez **Printix**.</span><span class="sxs-lookup"><span data-stu-id="46644-214">In the applications list, select **Printix**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-printix-tutorial/tutorial_printix_app.png) 

3. <span data-ttu-id="46644-216">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="46644-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="46644-218">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="46644-218">Click **Add** button.</span></span> <span data-ttu-id="46644-219">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="46644-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="46644-221">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="46644-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="46644-222">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="46644-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="46644-223">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="46644-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="46644-224">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="46644-224">Testing single sign-on</span></span>

<span data-ttu-id="46644-225">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="46644-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="46644-226">Lorsque vous cliquez sur la vignette Printix dans le volet d’accès, vous devez être connecté automatiquement à votre application Printix.</span><span class="sxs-lookup"><span data-stu-id="46644-226">When you click the Printix tile in the Access Panel, you should get automatically signed-on to your Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="46644-227">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="46644-227">Additional resources</span></span>

* [<span data-ttu-id="46644-228">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="46644-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="46644-229">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="46644-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-printix-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-printix-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-printix-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-printix-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-printix-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-printix-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-printix-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-printix-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-printix-tutorial/tutorial_general_203.png
