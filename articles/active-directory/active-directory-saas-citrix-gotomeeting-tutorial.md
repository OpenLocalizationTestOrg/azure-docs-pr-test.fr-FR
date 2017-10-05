---
title: "Didacticiel : Intégration d’Azure Active Directory à Citrix GoToMeeting | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: c1ac144c4fa43312ec26fce03cd0ee1bfcf73d4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="93240-103">Didacticiel : Intégration d’Azure Active Directory à Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="93240-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="93240-104">Dans ce didacticiel, vous allez apprendre à intégrer Citrix GoToMeeting à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="93240-104">In this tutorial, you learn how to integrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="93240-105">L’intégration de Citrix GoToMeeting à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="93240-105">Integrating Citrix GoToMeeting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="93240-106">Dans Azure AD, vous pouvez contrôler qui a accès à Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="93240-106">You can control in Azure AD who has access to Citrix GoToMeeting</span></span>
- <span data-ttu-id="93240-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Citrix GoToMeeting (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93240-107">You can enable your users to automatically get signed-on to Citrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="93240-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="93240-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="93240-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="93240-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93240-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="93240-110">Prerequisites</span></span>

<span data-ttu-id="93240-111">Pour configurer l’intégration d’Azure AD à Citrix GoToMeeting, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="93240-111">To configure Azure AD integration with Citrix GoToMeeting, you need the following items:</span></span>

- <span data-ttu-id="93240-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="93240-112">An Azure AD subscription</span></span>
- <span data-ttu-id="93240-113">Un abonnement Citrix GoToMeeting pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="93240-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="93240-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="93240-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="93240-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="93240-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="93240-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="93240-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="93240-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="93240-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="93240-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="93240-118">Scenario description</span></span>
<span data-ttu-id="93240-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="93240-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="93240-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="93240-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="93240-121">Ajout de Citrix GoToMeeting à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="93240-121">Adding Citrix GoToMeeting from the gallery</span></span>
2. <span data-ttu-id="93240-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="93240-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-the-gallery"></a><span data-ttu-id="93240-123">Ajout de Citrix GoToMeeting à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="93240-123">Adding Citrix GoToMeeting from the gallery</span></span>
<span data-ttu-id="93240-124">Pour configurer l’intégration de Citrix GoToMeeting à Azure AD, vous devez ajouter Citrix GoToMeeting, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="93240-124">To configure the integration of Citrix GoToMeeting into Azure AD, you need to add Citrix GoToMeeting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="93240-125">**Pour ajouter Citrix GoToMeeting à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="93240-125">**To add Citrix GoToMeeting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="93240-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="93240-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="93240-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="93240-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="93240-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="93240-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="93240-131">Cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="93240-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="93240-133">Dans la zone de recherche, tapez **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="93240-133">In the search box, type **Citrix GoToMeeting**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="93240-135">Dans le volet de résultats, sélectionnez **Citrix GoToMeeting**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="93240-135">In the results panel, select **Citrix GoToMeeting**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="93240-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="93240-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="93240-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Citrix GoToMeeting avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="93240-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="93240-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Citrix GoToMeeting équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93240-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix GoToMeeting is to a user in Azure AD.</span></span> <span data-ttu-id="93240-140">En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur Citrix GoToMeeting associé.</span><span class="sxs-lookup"><span data-stu-id="93240-140">In other words, a link relationship between an Azure AD user and the related user in Citrix GoToMeeting needs to be established.</span></span>

<span data-ttu-id="93240-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="93240-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="93240-142">Pour configurer et tester l’authentification unique Azure AD avec Citrix GoToMeeting, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="93240-142">To configure and test Azure AD single sign-on with Citrix GoToMeeting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="93240-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="93240-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="93240-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="93240-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="93240-145">**[Création d’un utilisateur de test Citrix GoToMeeting](#creating-a-citrix-gotomeeting-test-user)** pour avoir un équivalent de Britta Simon dans Citrix GoToMeeting, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="93240-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - to have a counterpart of Britta Simon in Citrix GoToMeeting that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="93240-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="93240-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="93240-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="93240-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="93240-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="93240-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="93240-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="93240-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="93240-150">**Pour configurer l’authentification unique Azure AD avec Citrix GoToMeeting, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="93240-150">**To configure Azure AD single sign-on with Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="93240-151">Dans le portail Azure, dans la page d’intégration de l’application **Citrix GoToMeeting**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="93240-151">In the Azure portal, on the **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="93240-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="93240-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="93240-155">Aucune étape n’est à effectuer dans la section **Domaine et URL Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="93240-155">On the **Citrix GoToMeeting Domain and URLs** section, no need to perform any steps.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="93240-157">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="93240-157">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="93240-159">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="93240-159">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="93240-161">Dans la section Configuration SAML de Citrix GoToMeeting, cliquez sur Configurer Citrix GoToMeeting pour ouvrir la fenêtre Configurer l’authentification.</span><span class="sxs-lookup"><span data-stu-id="93240-161">On the Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML to open Configure sign-on window.</span></span> <span data-ttu-id="93240-162">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="93240-162">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

6. <span data-ttu-id="93240-163">Dans une autre fenêtre de navigateur, connectez-vous à [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="93240-163">In a different browser window, log in to your [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="93240-164">Cliquez sur l’onglet **Fournisseur d’identité** , puis effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="93240-164">Click the **Identity Provider** tab, and then perform the following steps:</span></span>  
   
    <span data-ttu-id="93240-165">![Configuration SAML](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "Configuration SAML")</span><span class="sxs-lookup"><span data-stu-id="93240-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="93240-166">a.</span><span class="sxs-lookup"><span data-stu-id="93240-166">a.</span></span> <span data-ttu-id="93240-167">Sélectionnez **Manual**</span><span class="sxs-lookup"><span data-stu-id="93240-167">Select **Manual**</span></span>

    <span data-ttu-id="93240-168">b.</span><span class="sxs-lookup"><span data-stu-id="93240-168">b.</span></span> <span data-ttu-id="93240-169">Dans le portail Azure, dans la boîte de dialogue **Configurer l’authentification unique sur Citrix GoToMeeting**, copiez **l’URL du service d’authentification unique SAML**, puis collez-la dans la zone de texte **Sign-in page URL** (URL de la page de connexion).</span><span class="sxs-lookup"><span data-stu-id="93240-169">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="93240-170">c.</span><span class="sxs-lookup"><span data-stu-id="93240-170">c.</span></span> <span data-ttu-id="93240-171">Dans le portail Azure, dans la boîte de dialogue **Configurer l’authentification unique sur Citrix GoToMeeting**, copiez **l’URL de déconnexion**, puis collez-la dans la zone de texte **Sign-out page URL** (URL de la page de déconnexion).</span><span class="sxs-lookup"><span data-stu-id="93240-171">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **Sign-Out URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="93240-172">d.</span><span class="sxs-lookup"><span data-stu-id="93240-172">d.</span></span> <span data-ttu-id="93240-173">Dans le portail Azure, dans la boîte de dialogue **Configurer l’authentification unique sur Citrix GoToMeeting**, copiez **l’ID d’entité SAML**, puis collez-la dans la zone de texte **Identity Provider Entity ID** (ID d’entité du fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="93240-173">In the Azure portal, on the **Configure single sign-on at Citrix GoToMeeting** dialog page, copy the **SAML Entity ID** value, and then paste it into the **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="93240-174">e.</span><span class="sxs-lookup"><span data-stu-id="93240-174">e.</span></span> <span data-ttu-id="93240-175">Pour charger votre certificat téléchargé, cliquez sur **Upload Certificate**.</span><span class="sxs-lookup"><span data-stu-id="93240-175">To upload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="93240-176">f.</span><span class="sxs-lookup"><span data-stu-id="93240-176">f.</span></span> <span data-ttu-id="93240-177">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="93240-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="93240-178">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="93240-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="93240-179">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="93240-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="93240-180">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="93240-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="93240-181">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="93240-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="93240-182">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="93240-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="93240-184">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="93240-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="93240-185">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="93240-185">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="93240-187">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="93240-187">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="93240-189">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="93240-189">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="93240-191">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="93240-191">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="93240-193">a.</span><span class="sxs-lookup"><span data-stu-id="93240-193">a.</span></span> <span data-ttu-id="93240-194">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="93240-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="93240-195">b.</span><span class="sxs-lookup"><span data-stu-id="93240-195">b.</span></span> <span data-ttu-id="93240-196">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="93240-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="93240-197">c.</span><span class="sxs-lookup"><span data-stu-id="93240-197">c.</span></span> <span data-ttu-id="93240-198">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="93240-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="93240-199">d.</span><span class="sxs-lookup"><span data-stu-id="93240-199">d.</span></span> <span data-ttu-id="93240-200">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="93240-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="93240-201">Création d’un utilisateur de test Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="93240-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="93240-202">Dans cette section, un utilisateur appelé Britta Simon est créé dans Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="93240-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="93240-203">Citrix GoToMeeting prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="93240-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="93240-204">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="93240-204">There is no action item for you in this section.</span></span> <span data-ttu-id="93240-205">Si un utilisateur n’existe pas dans Citrix GoToMeeting, un nouvel utilisateur est créé lorsque vous tentez d’accéder à Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="93240-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt to access Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="93240-206">Si vous devez créer un utilisateur manuellement, contactez [l’équipe du support Citrix GoToMeeting](https://care.citrixonline.com/gotomeeting).</span><span class="sxs-lookup"><span data-stu-id="93240-206">If you need to create a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="93240-207">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="93240-207">Assigning the Azure AD test user</span></span>

<span data-ttu-id="93240-208">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="93240-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix GoToMeeting.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="93240-210">**Pour attribuer Britta Simon à Citrix GoToMeeting, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="93240-210">**To assign Britta Simon to Citrix GoToMeeting, perform the following steps:**</span></span>

1. <span data-ttu-id="93240-211">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="93240-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="93240-213">Dans la liste des applications, sélectionnez **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="93240-213">In the applications list, select **Citrix GoToMeeting**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="93240-215">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="93240-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="93240-217">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="93240-217">Click **Add** button.</span></span> <span data-ttu-id="93240-218">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="93240-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="93240-220">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="93240-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="93240-221">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="93240-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="93240-222">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="93240-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="93240-223">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="93240-223">Testing single sign-on</span></span>

<span data-ttu-id="93240-224">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="93240-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="93240-225">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="93240-225">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="93240-226">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="93240-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="93240-227">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="93240-227">Additional resources</span></span>

* [<span data-ttu-id="93240-228">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="93240-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="93240-229">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="93240-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="93240-230">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="93240-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

