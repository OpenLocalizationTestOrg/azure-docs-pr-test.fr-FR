---
title: "Didacticiel : Intégration d’Azure Active Directory à Citrix ShareFile | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Citrix ShareFile."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: b85680104fe4f33638c559b2a12483a2312a4476
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="7ed3e-103">Didacticiel : Intégration d’Azure Active Directory à Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="7ed3e-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="7ed3e-104">Dans ce didacticiel, vous allez apprendre à intégrer Citrix ShareFile à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7ed3e-104">In this tutorial, you learn how to integrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7ed3e-105">L’intégration de Citrix ShareFile à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7ed3e-105">Integrating Citrix ShareFile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7ed3e-106">Dans Azure AD, vous pouvez contrôler qui a accès à Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-106">You can control in Azure AD who has access to Citrix ShareFile.</span></span>
- <span data-ttu-id="7ed3e-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Citrix ShareFile (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-107">You can enable your users to automatically get signed-on to Citrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7ed3e-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7ed3e-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7ed3e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ed3e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7ed3e-110">Prerequisites</span></span>

<span data-ttu-id="7ed3e-111">Pour configurer l’intégration d’Azure AD à Citrix ShareFile, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7ed3e-111">To configure Azure AD integration with Citrix ShareFile, you need the following items:</span></span>

- <span data-ttu-id="7ed3e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ed3e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7ed3e-113">Un abonnement Citrix ShareFile pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="7ed3e-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7ed3e-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7ed3e-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7ed3e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7ed3e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7ed3e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7ed3e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7ed3e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="7ed3e-118">Scenario description</span></span>
<span data-ttu-id="7ed3e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7ed3e-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="7ed3e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7ed3e-121">Ajout de Citrix ShareFile à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="7ed3e-121">Add Citrix ShareFile from the gallery</span></span>
2. <span data-ttu-id="7ed3e-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ed3e-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-the-gallery"></a><span data-ttu-id="7ed3e-123">Ajout de Citrix ShareFile à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="7ed3e-123">Add Citrix ShareFile from the gallery</span></span>
<span data-ttu-id="7ed3e-124">Pour configurer l’intégration de Citrix ShareFile avec Azure AD, vous devez ajouter Citrix ShareFile, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-124">To configure the integration of Citrix ShareFile into Azure AD, you need to add Citrix ShareFile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7ed3e-125">**Pour ajouter Citrix ShareFile à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7ed3e-125">**To add Citrix ShareFile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7ed3e-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="7ed3e-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7ed3e-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="7ed3e-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="7ed3e-133">Dans la zone de recherche, tapez **Citrix ShareFile**, sélectionnez **Citrix ShareFile** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-133">In the search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button to add the application.</span></span>

    ![Citrix ShareFile dans la liste des résultats](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7ed3e-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ed3e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7ed3e-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Citrix ShareFile avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="7ed3e-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7ed3e-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Citrix ShareFile équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix ShareFile is to a user in Azure AD.</span></span> <span data-ttu-id="7ed3e-138">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur Citrix ShareFile associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-138">In other words, a link relationship between an Azure AD user and the related user in Citrix ShareFile needs to be established.</span></span>

<span data-ttu-id="7ed3e-139">Dans Citrix ShareFile, attribuez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-139">In Citrix ShareFile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7ed3e-140">Pour configurer et tester l’authentification unique Azure AD avec Citrix ShareFile, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="7ed3e-140">To configure and test Azure AD single sign-on with Citrix ShareFile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7ed3e-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7ed3e-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7ed3e-143">**[Création d’un utilisateur de test Citrix ShareFile](#create-a-citrix-sharefile-test-user)** pour avoir un équivalent de Britta Simon dans Citrix ShareFile, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - to have a counterpart of Britta Simon in Citrix ShareFile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7ed3e-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7ed3e-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7ed3e-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ed3e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7ed3e-147">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et vous configurez l’authentification unique dans votre application Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="7ed3e-148">**Pour configurer l’authentification unique Azure AD avec Citrix ShareFile, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7ed3e-148">**To configure Azure AD single sign-on with Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="7ed3e-149">Dans le portail Azure, dans la page d’intégration de l’application **Citrix ShareFile**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-149">In the Azure portal, on the **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="7ed3e-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="7ed3e-153">Dans la section **Domaine et URL Citrix ShareFile**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7ed3e-153">On the **Citrix ShareFile Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="7ed3e-155">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="7ed3e-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7ed3e-156">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-156">This value is not real.</span></span> <span data-ttu-id="7ed3e-157">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="7ed3e-158">Pour obtenir cette valeur, contactez [l’équipe du support Citrix ShareFile](https://www.citrix.co.in/products/sharefile/support.html).</span><span class="sxs-lookup"><span data-stu-id="7ed3e-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) to get this value.</span></span> 

4. <span data-ttu-id="7ed3e-159">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="7ed3e-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7ed3e-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7ed3e-163">Dans la section **Configuration de Citrix ShareFile** , cliquez sur **Configurer Citrix ShareFile** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-163">On the **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7ed3e-164">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="7ed3e-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration de Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="7ed3e-166">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise **Citrix ShareFile** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="7ed3e-167">Dans la barre d’outils située en haut, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-167">In the toolbar on the top, click **Admin**.</span></span>

9. <span data-ttu-id="7ed3e-168">Dans le volet de navigation de gauche, sélectionnez **Configure Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-168">In the left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="7ed3e-169">![Compte d’administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Compte d’administration")</span><span class="sxs-lookup"><span data-stu-id="7ed3e-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="7ed3e-170">Dans la page de boîte de dialogue **Single Sign-On/ SAML 2.0 Configuration** sous **Basic Settings**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7ed3e-170">On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:</span></span>
   
    <span data-ttu-id="7ed3e-171">![Authentification unique](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="7ed3e-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="7ed3e-172">a.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-172">a.</span></span> <span data-ttu-id="7ed3e-173">Cliquez sur **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="7ed3e-174">b.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-174">b.</span></span> <span data-ttu-id="7ed3e-175">Dans la zone de texte **Your IDP Issuer/Entity ID** (Votre émetteur IDP/ID d’entité), collez la valeur **ID d’entité SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-175">In **Your IDP Issuer/ Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="7ed3e-176">c.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-176">c.</span></span> <span data-ttu-id="7ed3e-177">Cliquez sur **Change** (Modifier) en regard du champ **X.509 Certificate** (Certificat X.509), puis chargez le certificat que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-177">Click **Change** next to the **X.509 Certificate** field and then upload the certificate you downloaded from the Azure portal.</span></span>
    
    <span data-ttu-id="7ed3e-178">d.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-178">d.</span></span> <span data-ttu-id="7ed3e-179">Dans la zone de texte **URL de connexion**, collez la valeur **URL du service d’authentification unique SAML** que vous avez copiée dans portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-179">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="7ed3e-180">e.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-180">e.</span></span> <span data-ttu-id="7ed3e-181">Dans la zone de texte **Logout URL (URL de déconnexion)**, collez la valeur **URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-181">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="7ed3e-182">Cliquez sur **Save** dans le portail de gestion Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-182">Click **Save** on the Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="7ed3e-183">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7ed3e-184">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7ed3e-185">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7ed3e-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7ed3e-186">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ed3e-186">Create an Azure AD test user</span></span>

<span data-ttu-id="7ed3e-187">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="7ed3e-189">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7ed3e-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7ed3e-190">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-190">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7ed3e-192">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-192">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7ed3e-194">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-194">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7ed3e-196">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7ed3e-196">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7ed3e-198">a.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-198">a.</span></span> <span data-ttu-id="7ed3e-199">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-199">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7ed3e-200">b.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-200">b.</span></span> <span data-ttu-id="7ed3e-201">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-201">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7ed3e-202">c.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-202">c.</span></span> <span data-ttu-id="7ed3e-203">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-203">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7ed3e-204">d.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-204">d.</span></span> <span data-ttu-id="7ed3e-205">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="7ed3e-206">Créer un utilisateur de test Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="7ed3e-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="7ed3e-207">Pour permettre aux utilisateurs Azure AD de se connecter à Citrix ShareFile, vous devez les approvisionner dans Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-207">In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="7ed3e-208">En l’occurrence, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-208">In the case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="7ed3e-209">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7ed3e-209">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="7ed3e-210">Connectez-vous à votre locataire **Citrix ShareFile** .</span><span class="sxs-lookup"><span data-stu-id="7ed3e-210">Log in to your **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="7ed3e-211">Cliquez sur **Manage Users \> Manage Users Home \> + Create Employee**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="7ed3e-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span><span class="sxs-lookup"><span data-stu-id="7ed3e-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="7ed3e-213">Dans la section **Basic Information**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7ed3e-213">On the **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="7ed3e-214">![Informations de base](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Informations de base")</span><span class="sxs-lookup"><span data-stu-id="7ed3e-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="7ed3e-215">a.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-215">a.</span></span> <span data-ttu-id="7ed3e-216">Dans la zone de texte **Email Address** (Adresse e-mail), tapez l’adresse e-mail du compte de Britta Simon au format suivant : **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-216">In the **Email Address** textbox, type the email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="7ed3e-217">b.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-217">b.</span></span> <span data-ttu-id="7ed3e-218">Dans la zone de texte **First Name**, entrez le **prénom** de l’utilisateur. Ici, il s’agit de **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-218">In the **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="7ed3e-219">c.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-219">c.</span></span> <span data-ttu-id="7ed3e-220">Dans la zone de texte **Last Name**, entrez le **nom** de l’utilisateur. Ici, il s’agit de **Simon**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-220">In the **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="7ed3e-221">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="7ed3e-222">Le titulaire du compte Azure AD va recevoir un e-mail contenant un lien lui permettant de confirmer son compte avant que celui-ci ne soit activé. Vous pouvez utiliser n’importe quel autre outil de création de compte d’utilisateur Citrix ShareFile ou toute autre API fournie par Citrix ShareFile pour approvisionner des comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-222">The Azure AD account holder will receive an email and follow a link to confirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7ed3e-223">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ed3e-223">Assign the Azure AD test user</span></span>

<span data-ttu-id="7ed3e-224">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix ShareFile.</span></span>

![Attribuer le rôle utilisateur][200] 

<span data-ttu-id="7ed3e-226">**Pour affecter Britta Simon à Citrix ShareFile, suivez les étapes ci-dessous :**</span><span class="sxs-lookup"><span data-stu-id="7ed3e-226">**To assign Britta Simon to Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="7ed3e-227">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="7ed3e-229">Dans la liste des applications, sélectionnez **Citrix ShareFile**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-229">In the applications list, select **Citrix ShareFile**.</span></span>

    ![Lien Citrix ShareFile dans la liste des applications](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="7ed3e-231">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="7ed3e-233">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-233">Click **Add** button.</span></span> <span data-ttu-id="7ed3e-234">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="7ed3e-236">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7ed3e-237">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7ed3e-238">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7ed3e-239">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7ed3e-239">Test single sign-on</span></span>

<span data-ttu-id="7ed3e-240">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7ed3e-241">Si vous cliquez sur la mosaïque Citrix ShareFile dans le volet d’accès, vous devez vous connecter automatiquement à votre application Citrix ShareFile.</span><span class="sxs-lookup"><span data-stu-id="7ed3e-241">When you click the Citrix ShareFile tile in the Access Panel, you should get automatically signed-on to your Citrix ShareFile application.</span></span>
<span data-ttu-id="7ed3e-242">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7ed3e-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7ed3e-243">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7ed3e-243">Additional resources</span></span>

* [<span data-ttu-id="7ed3e-244">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ed3e-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7ed3e-245">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7ed3e-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

