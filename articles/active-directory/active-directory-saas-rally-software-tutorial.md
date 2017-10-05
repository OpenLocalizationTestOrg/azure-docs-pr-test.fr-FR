---
title: "Didacticiel : Intégration d’Azure Active Directory à Rally Software | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Rally Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba25fade-e152-42dd-8377-a30bbc48c3ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: jeedes
ms.openlocfilehash: 6481c9ef0ca71419ccfa6f7956f4702985743df3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rally-software"></a><span data-ttu-id="32137-103">Didacticiel : Intégration d’Azure Active Directory à Rally Software</span><span class="sxs-lookup"><span data-stu-id="32137-103">Tutorial: Azure Active Directory integration with Rally Software</span></span>

<span data-ttu-id="32137-104">Dans ce didacticiel, vous allez apprendre à intégrer Rally Software à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32137-104">In this tutorial, you learn how to integrate Rally Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32137-105">L’intégration de Rally Software à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="32137-105">Integrating Rally Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="32137-106">Dans Azure AD, vous pouvez contrôler qui a accès à Rally Software.</span><span class="sxs-lookup"><span data-stu-id="32137-106">You can control in Azure AD who has access to Rally Software.</span></span>
- <span data-ttu-id="32137-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Rally Software (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32137-107">You can enable your users to automatically get signed-on to Rally Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="32137-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="32137-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="32137-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32137-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32137-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="32137-110">Prerequisites</span></span>

<span data-ttu-id="32137-111">Pour configurer l’intégration d’Azure AD à Rally Software, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="32137-111">To configure Azure AD integration with Rally Software, you need the following items:</span></span>

- <span data-ttu-id="32137-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="32137-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32137-113">Un abonnement Rally Software pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="32137-113">A Rally Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32137-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="32137-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32137-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="32137-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32137-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="32137-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32137-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32137-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32137-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="32137-118">Scenario description</span></span>
<span data-ttu-id="32137-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="32137-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32137-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="32137-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32137-121">Ajout de Rally Software à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="32137-121">Adding Rally Software from the gallery</span></span>
2. <span data-ttu-id="32137-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="32137-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rally-software-from-the-gallery"></a><span data-ttu-id="32137-123">Ajout de Rally Software à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="32137-123">Adding Rally Software from the gallery</span></span>
<span data-ttu-id="32137-124">Pour configurer l’intégration de Rally Software à Azure AD, vous devez ajouter Rally Software à partir de la galerie, à votre liste d’applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="32137-124">To configure the integration of Rally Software into Azure AD, you need to add Rally Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="32137-125">**Pour ajouter Rally Software à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="32137-125">**To add Rally Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="32137-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="32137-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="32137-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="32137-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="32137-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="32137-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="32137-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="32137-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="32137-133">Dans la zone de recherche, tapez **Rally Software**, sélectionnez **Rally Software** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="32137-133">In the search box, type **Rally Software**, select **Rally Software** from result panel then click **Add** button to add the application.</span></span>

    ![Rally Software dans la liste des résultats](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="32137-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="32137-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="32137-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Rally Software à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="32137-136">In this section, you configure and test Azure AD single sign-on with Rally Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="32137-137">Pour que l’authentification unique fonctionne, Azure AD a besoin de savoir qui est l’utilisateur Rally Software équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32137-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Rally Software is to a user in Azure AD.</span></span> <span data-ttu-id="32137-138">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur Rally Software associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="32137-138">In other words, a link relationship between an Azure AD user and the related user in Rally Software needs to be established.</span></span>

<span data-ttu-id="32137-139">Dans Rally Software, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="32137-139">In Rally Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="32137-140">Pour configurer et tester l’authentification unique Azure AD avec Rally Software, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="32137-140">To configure and test Azure AD single sign-on with Rally Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="32137-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="32137-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="32137-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32137-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32137-143">**[Création d’un utilisateur de test Rally Software](#create-a-rally-software-test-user)** pour avoir un équivalent de Britta Simon dans Rally Software lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="32137-143">**[Create a Rally Software test user](#create-a-rally-software-test-user)** - to have a counterpart of Britta Simon in Rally Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="32137-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32137-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32137-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="32137-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="32137-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="32137-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="32137-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Rally Software.</span><span class="sxs-lookup"><span data-stu-id="32137-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rally Software application.</span></span>

<span data-ttu-id="32137-148">**Pour configurer l’authentification unique Azure AD avec Rally Software, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="32137-148">**To configure Azure AD single sign-on with Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="32137-149">Dans le portail Azure, dans la page d’intégration de l’application **Rally Software**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="32137-149">In the Azure portal, on the **Rally Software** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="32137-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="32137-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_samlbase.png)

3. <span data-ttu-id="32137-153">Dans la section **Domaine et URL Rally Software**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="32137-153">On the **Rally Software Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_url.png)

    <span data-ttu-id="32137-155">a.</span><span class="sxs-lookup"><span data-stu-id="32137-155">a.</span></span> <span data-ttu-id="32137-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="32137-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    <span data-ttu-id="32137-157">b.</span><span class="sxs-lookup"><span data-stu-id="32137-157">b.</span></span> <span data-ttu-id="32137-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<tenant-name>.rally.com`</span><span class="sxs-lookup"><span data-stu-id="32137-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.rally.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32137-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="32137-159">These values are not real.</span></span> <span data-ttu-id="32137-160">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="32137-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="32137-161">Pour obtenir ces valeurs, contactez [l’équipe du support Rally Software](https://help.rallydev.com/).</span><span class="sxs-lookup"><span data-stu-id="32137-161">Contact [Rally Software Client support team](https://help.rallydev.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="32137-162">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="32137-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_certificate.png) 

5. <span data-ttu-id="32137-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="32137-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-rally-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32137-166">Dans la section **Configuration de Rally Software**, cliquez sur **Configurer Rally Software** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="32137-166">On the **Rally Software Configuration** section, click **Configure Rally Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="32137-167">Copiez **l’URL de déconnexion et l’ID d’entité SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="32137-167">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configuration de Rally Software](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_configure.png) 

7. <span data-ttu-id="32137-169">Connectez-vous à votre locataire **Rally Software** .</span><span class="sxs-lookup"><span data-stu-id="32137-169">Log in to your **Rally Software** tenant.</span></span>

8. <span data-ttu-id="32137-170">Dans la barre d’outils située en haut, cliquez sur **Setup**, puis sélectionnez **Subscription**.</span><span class="sxs-lookup"><span data-stu-id="32137-170">In the toolbar on the top, click **Setup**, and then select **Subscription**.</span></span>
   
    <span data-ttu-id="32137-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span><span class="sxs-lookup"><span data-stu-id="32137-171">![Subscription](./media/active-directory-saas-rally-software-tutorial/ic769531.png "Subscription")</span></span>

9. <span data-ttu-id="32137-172">Cliquez sur le bouton **Action**.</span><span class="sxs-lookup"><span data-stu-id="32137-172">Click the **Action** button.</span></span> <span data-ttu-id="32137-173">Sélectionnez **Modifier l’abonnement** en haut à droite de la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="32137-173">Select **Edit Subscription** at the top right side of the toolbar.</span></span>

10. <span data-ttu-id="32137-174">Dans la page **Subscription**, procédez comme suit, puis cliquez sur **Save & Close** :</span><span class="sxs-lookup"><span data-stu-id="32137-174">On the **Subscription** dialog page, perform the following steps, and then click **Save & Close**:</span></span>
   
    <span data-ttu-id="32137-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="32137-175">![Authentication](./media/active-directory-saas-rally-software-tutorial/ic769542.png "Authentication")</span></span>
   
    <span data-ttu-id="32137-176">a.</span><span class="sxs-lookup"><span data-stu-id="32137-176">a.</span></span> <span data-ttu-id="32137-177">Sélectionnez **Rally or SSO authentication** dans la liste déroulante Authentication.</span><span class="sxs-lookup"><span data-stu-id="32137-177">Select **Rally or SSO authentication** from Authentication dropdown.</span></span>

    <span data-ttu-id="32137-178">b.</span><span class="sxs-lookup"><span data-stu-id="32137-178">b.</span></span> <span data-ttu-id="32137-179">Dans la zone de texte **Identity provider URL** (URL du fournisseur d’identité), collez **l’ID d’entité SAML** copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="32137-179">In the **Identity provider URL** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="32137-180">c.</span><span class="sxs-lookup"><span data-stu-id="32137-180">c.</span></span> <span data-ttu-id="32137-181">Dans la zone de texte **SSO Logout** (Déconnexion SSO), collez **l’URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="32137-181">In the **SSO Logout** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="32137-182">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="32137-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="32137-183">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="32137-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="32137-184">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="32137-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="32137-185">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="32137-185">Create an Azure AD test user</span></span>

<span data-ttu-id="32137-186">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="32137-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="32137-188">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="32137-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="32137-189">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="32137-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-rally-software-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="32137-191">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="32137-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-rally-software-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="32137-193">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="32137-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-rally-software-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="32137-195">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="32137-195">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-rally-software-tutorial/create_aaduser_04.png)

    <span data-ttu-id="32137-197">a.</span><span class="sxs-lookup"><span data-stu-id="32137-197">a.</span></span> <span data-ttu-id="32137-198">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32137-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32137-199">b.</span><span class="sxs-lookup"><span data-stu-id="32137-199">b.</span></span> <span data-ttu-id="32137-200">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32137-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="32137-201">c.</span><span class="sxs-lookup"><span data-stu-id="32137-201">c.</span></span> <span data-ttu-id="32137-202">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="32137-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="32137-203">d.</span><span class="sxs-lookup"><span data-stu-id="32137-203">d.</span></span> <span data-ttu-id="32137-204">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="32137-204">Click **Create**.</span></span>
 
### <a name="create-a-rally-software-test-user"></a><span data-ttu-id="32137-205">Créer un utilisateur de test Rally Software</span><span class="sxs-lookup"><span data-stu-id="32137-205">Create a Rally Software test user</span></span>

<span data-ttu-id="32137-206">Pour que les utilisateurs Azure AD puissent se connecter, ils doivent être attribués dans l’application Rally Software avec leur nom d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="32137-206">For Azure AD users to be able to sign in, they must be provisioned to the Rally Software application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="32137-207">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="32137-207">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="32137-208">Connectez-vous à votre locataire Rally Software.</span><span class="sxs-lookup"><span data-stu-id="32137-208">Log in to your Rally Software tenant.</span></span>

2. <span data-ttu-id="32137-209">Accédez à **Setup \> USERS**, puis cliquez sur **+ Add New**.</span><span class="sxs-lookup"><span data-stu-id="32137-209">Go to **Setup \> USERS**, and then click **+ Add New**.</span></span>
   
    <span data-ttu-id="32137-210">![Utilisateurs](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="32137-210">![Users](./media/active-directory-saas-rally-software-tutorial/ic781039.png "Users")</span></span>

3. <span data-ttu-id="32137-211">Tapez le nom dans la zone de texte New User, puis cliquez sur **Add with Details**.</span><span class="sxs-lookup"><span data-stu-id="32137-211">Type the name in the New User textbox, and then click **Add with Details**.</span></span>

4. <span data-ttu-id="32137-212">Dans la section **Create User** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="32137-212">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="32137-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="32137-213">![Create User](./media/active-directory-saas-rally-software-tutorial/ic781040.png "Create User")</span></span>

    <span data-ttu-id="32137-214">a.</span><span class="sxs-lookup"><span data-stu-id="32137-214">a.</span></span> <span data-ttu-id="32137-215">Dans la zone de texte **User Name** (Nom d’utilisateur), tapez le nom complet d’un utilisateur, par exemple **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="32137-215">In the **User Name** textbox, type the name of user like **Brittsimon**.</span></span>
   
    <span data-ttu-id="32137-216">b.</span><span class="sxs-lookup"><span data-stu-id="32137-216">b.</span></span> <span data-ttu-id="32137-217">Dans la zone de texte **E-mail Address** (Adresse e-mail), entrez l’adresse e-mail de l’utilisateur, par exemple **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="32137-217">In **E-mail Address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="32137-218">c.</span><span class="sxs-lookup"><span data-stu-id="32137-218">c.</span></span> <span data-ttu-id="32137-219">Dans la zone de texte **Prénom**, entrez le prénom de l’utilisateur, par exemple **Britta**.</span><span class="sxs-lookup"><span data-stu-id="32137-219">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="32137-220">d.</span><span class="sxs-lookup"><span data-stu-id="32137-220">d.</span></span> <span data-ttu-id="32137-221">Dans la zone de texte **Nom**, entrez le nom de l’utilisateur, par exemple **Simon**.</span><span class="sxs-lookup"><span data-stu-id="32137-221">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

    <span data-ttu-id="32137-222">e.</span><span class="sxs-lookup"><span data-stu-id="32137-222">e.</span></span> <span data-ttu-id="32137-223">Cliquez sur **Enregistrer et fermer**.</span><span class="sxs-lookup"><span data-stu-id="32137-223">Click **Save & Close**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="32137-224">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par Rally Software pour approvisionner des comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32137-224">You can use any other Rally Software user account creation tools or APIs provided by Rally Software to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="32137-225">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="32137-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="32137-226">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Rally Software.</span><span class="sxs-lookup"><span data-stu-id="32137-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rally Software.</span></span>

![Attribuer le rôle utilisateur][200] 

<span data-ttu-id="32137-228">**Pour attribuer Britta Simon à Rally Software, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="32137-228">**To assign Britta Simon to Rally Software, perform the following steps:**</span></span>

1. <span data-ttu-id="32137-229">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="32137-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="32137-231">Dans la liste des applications, sélectionnez **Rally Software**.</span><span class="sxs-lookup"><span data-stu-id="32137-231">In the applications list, select **Rally Software**.</span></span>

    ![Lien Rally Software dans la liste des applications](./media/active-directory-saas-rally-software-tutorial/tutorial_rallysoftware_app.png)  

3. <span data-ttu-id="32137-233">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="32137-233">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="32137-235">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="32137-235">Click **Add** button.</span></span> <span data-ttu-id="32137-236">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="32137-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="32137-238">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="32137-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="32137-239">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="32137-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32137-240">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="32137-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="32137-241">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="32137-241">Test single sign-on</span></span>

<span data-ttu-id="32137-242">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="32137-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="32137-243">Lorsque vous cliquez sur la vignette Rally Software dans le panneau d’accès, vous devez être connecté automatiquement à votre application Rally Software.</span><span class="sxs-lookup"><span data-stu-id="32137-243">When you click the Rally Software tile in the Access Panel, you should get automatically signed-on to your Rally Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32137-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="32137-244">Additional resources</span></span>

* [<span data-ttu-id="32137-245">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32137-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32137-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="32137-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rally-software-tutorial/tutorial_general_203.png

