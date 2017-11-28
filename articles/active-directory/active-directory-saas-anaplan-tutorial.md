---
title: "Didacticiel : Intégration d’Azure Active Directory à Anaplan | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Anaplan."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a9c2914-6c8c-4a88-93e3-3753afb40e6b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jeedes
ms.openlocfilehash: c2ecfd5f066ed3bd10f74f935de2f2b80057329f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-anaplan"></a><span data-ttu-id="1a2ff-103">Didacticiel : Intégration d’Azure Active Directory à Anaplan</span><span class="sxs-lookup"><span data-stu-id="1a2ff-103">Tutorial: Azure Active Directory integration with Anaplan</span></span>

<span data-ttu-id="1a2ff-104">Dans ce didacticiel, vous allez apprendre à intégrer Anaplan à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1a2ff-104">In this tutorial, you learn how to integrate Anaplan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1a2ff-105">L’intégration d’Anaplan dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1a2ff-105">Integrating Anaplan with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1a2ff-106">Dans Azure AD, vous pouvez contrôler qui a accès à Anaplan</span><span class="sxs-lookup"><span data-stu-id="1a2ff-106">You can control in Azure AD who has access to Anaplan</span></span>
- <span data-ttu-id="1a2ff-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Anaplan (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a2ff-107">You can enable your users to automatically get signed-on to Anaplan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1a2ff-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1a2ff-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1a2ff-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1a2ff-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a2ff-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1a2ff-110">Prerequisites</span></span>

<span data-ttu-id="1a2ff-111">Pour configurer l’intégration d’Azure AD à Anaplan, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1a2ff-111">To configure Azure AD integration with Anaplan, you need the following items:</span></span>

- <span data-ttu-id="1a2ff-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a2ff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1a2ff-113">Un abonnement Anaplan pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1a2ff-113">An Anaplan single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1a2ff-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1a2ff-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1a2ff-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1a2ff-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1a2ff-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a2ff-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1a2ff-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1a2ff-118">Scenario description</span></span>
<span data-ttu-id="1a2ff-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1a2ff-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1a2ff-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1a2ff-121">Ajout d’Anaplan à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1a2ff-121">Adding Anaplan from the gallery</span></span>
2. <span data-ttu-id="1a2ff-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a2ff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-anaplan-from-the-gallery"></a><span data-ttu-id="1a2ff-123">Ajout d’Anaplan à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1a2ff-123">Adding Anaplan from the gallery</span></span>
<span data-ttu-id="1a2ff-124">Pour configurer l’intégration d’Anaplan à Azure AD, vous devez ajouter Anaplan à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-124">To configure the integration of Anaplan into Azure AD, you need to add Anaplan from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1a2ff-125">**Pour ajouter Anaplan à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1a2ff-125">**To add Anaplan from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1a2ff-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1a2ff-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1a2ff-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1a2ff-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1a2ff-133">Dans la zone de recherche, tapez **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-133">In the search box, type **Anaplan**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_search.png)

5. <span data-ttu-id="1a2ff-135">Dans le volet de résultats, sélectionnez **Anaplan**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-135">In the results panel, select **Anaplan**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1a2ff-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a2ff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1a2ff-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Anaplan, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1a2ff-138">In this section, you configure and test Azure AD single sign-on with Anaplan based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1a2ff-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Anaplan correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Anaplan is to a user in Azure AD.</span></span> <span data-ttu-id="1a2ff-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Anaplan associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-140">In other words, a link relationship between an Azure AD user and the related user in Anaplan needs to be established.</span></span>

<span data-ttu-id="1a2ff-141">Dans Anaplan, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-141">In Anaplan, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1a2ff-142">Pour configurer et tester l’authentification unique Azure AD avec Anaplan, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1a2ff-142">To configure and test Azure AD single sign-on with Anaplan, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1a2ff-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1a2ff-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1a2ff-145">**[Création d’un utilisateur de test Anaplan](#creating-an-anaplan-test-user)** pour avoir un équivalent de Britta Simon dans Anaplan, lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-145">**[Creating an Anaplan test user](#creating-an-anaplan-test-user)** - to have a counterpart of Britta Simon in Anaplan that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1a2ff-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1a2ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1a2ff-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a2ff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1a2ff-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Anaplan.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Anaplan application.</span></span>

<span data-ttu-id="1a2ff-150">**Pour configurer l’authentification unique Azure AD avec Anaplan, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1a2ff-150">**To configure Azure AD single sign-on with Anaplan, perform the following steps:**</span></span>

1. <span data-ttu-id="1a2ff-151">Dans le Portail Azure, sur la page d’intégration de l’application **Anaplan**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-151">In the Azure portal, on the **Anaplan** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1a2ff-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_samlbase.png)

3. <span data-ttu-id="1a2ff-155">Dans la section **Domaine et URL Anaplan**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1a2ff-155">On the **Anaplan Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_url.png)

    <span data-ttu-id="1a2ff-157">a.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-157">a.</span></span> <span data-ttu-id="1a2ff-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="1a2ff-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sdp.anaplan.com/frontdoor/saml/<tenant name>`</span></span>

    <span data-ttu-id="1a2ff-159">b.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-159">b.</span></span> <span data-ttu-id="1a2ff-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.anaplan.com`</span><span class="sxs-lookup"><span data-stu-id="1a2ff-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.anaplan.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1a2ff-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-161">These values are not real.</span></span> <span data-ttu-id="1a2ff-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1a2ff-163">Pour obtenir ces valeurs, contactez [l’équipe du support Anaplan](mailto:support@anaplan.com).</span><span class="sxs-lookup"><span data-stu-id="1a2ff-163">Contact [Anaplan Client support team](mailto:support@anaplan.com) to get these values.</span></span> 
 
4. <span data-ttu-id="1a2ff-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_certificate.png) 

5. <span data-ttu-id="1a2ff-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1a2ff-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-anaplan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1a2ff-168">Dans la section **Configuration d’Anaplan**, cliquez sur **Configurer Anaplan** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-168">On the **Anaplan Configuration** section, click **Configure Anaplan** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1a2ff-169">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="1a2ff-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_configure.png) 

7. <span data-ttu-id="1a2ff-171">Pour configurer l’authentification unique côté **Anaplan**, vous devez envoyer le fichier **XML des métadonnées** téléchargé, **l’ID d’entité SAML**, **l’URL du service d’authentification unique SAML** et **l’URL de déconnexion** à [l’équipe du support Anaplan](mailto:support@anaplan.com).</span><span class="sxs-lookup"><span data-stu-id="1a2ff-171">To configure single sign-on on **Anaplan** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL**   to [Anaplan support team](mailto:support@anaplan.com).</span></span> <span data-ttu-id="1a2ff-172">Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1a2ff-173">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1a2ff-174">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1a2ff-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1a2ff-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1a2ff-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a2ff-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="1a2ff-177">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1a2ff-179">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1a2ff-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1a2ff-180">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1a2ff-182">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1a2ff-184">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1a2ff-186">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1a2ff-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-anaplan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1a2ff-188">a.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-188">a.</span></span> <span data-ttu-id="1a2ff-189">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1a2ff-190">b.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-190">b.</span></span> <span data-ttu-id="1a2ff-191">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1a2ff-192">c.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-192">c.</span></span> <span data-ttu-id="1a2ff-193">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1a2ff-194">d.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-194">d.</span></span> <span data-ttu-id="1a2ff-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-195">Click **Create**.</span></span>
 
### <a name="creating-an-anaplan-test-user"></a><span data-ttu-id="1a2ff-196">Création d’un utilisateur de test Anaplan</span><span class="sxs-lookup"><span data-stu-id="1a2ff-196">Creating an Anaplan test user</span></span>

<span data-ttu-id="1a2ff-197">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Anaplan.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-197">In this section, you create a user called Britta Simon in Anaplan.</span></span> <span data-ttu-id="1a2ff-198">Pour ajouter les utilisateurs dans la plateforme Anaplan, contactez [l’équipe du support Anaplan](mailto:support@anaplan.com).</span><span class="sxs-lookup"><span data-stu-id="1a2ff-198">Please work with [Anaplan support team](mailto:support@anaplan.com) to add the users in the Anaplan platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1a2ff-199">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1a2ff-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1a2ff-200">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Anaplan.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Anaplan.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1a2ff-202">**Pour affecter Britta Simon à Anaplan, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1a2ff-202">**To assign Britta Simon to Anaplan, perform the following steps:**</span></span>

1. <span data-ttu-id="1a2ff-203">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1a2ff-205">Dans la liste des applications, sélectionnez **Anaplan**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-205">In the applications list, select **Anaplan**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-anaplan-tutorial/tutorial_anaplan_app.png) 

3. <span data-ttu-id="1a2ff-207">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1a2ff-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-209">Click **Add** button.</span></span> <span data-ttu-id="1a2ff-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1a2ff-212">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1a2ff-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1a2ff-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1a2ff-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1a2ff-215">Testing single sign-on</span></span>

<span data-ttu-id="1a2ff-216">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1a2ff-217">Lorsque vous cliquez sur la vignette Anaplan dans le volet d’accès, vous devez être connecté automatiquement à votre application Anaplan.</span><span class="sxs-lookup"><span data-stu-id="1a2ff-217">When you click the Anaplan tile in the Access Panel, you should get automatically signed-on to your Anaplan application.</span></span>

<span data-ttu-id="1a2ff-218">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1a2ff-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1a2ff-219">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1a2ff-219">Additional resources</span></span>

* [<span data-ttu-id="1a2ff-220">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a2ff-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1a2ff-221">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1a2ff-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-anaplan-tutorial/tutorial_general_203.png

