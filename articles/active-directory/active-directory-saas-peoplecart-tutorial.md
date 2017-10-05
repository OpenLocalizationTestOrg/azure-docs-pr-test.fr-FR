---
title: "Didacticiel : Intégration d’Azure Active Directory à Peoplecart | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Peoplecart."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c83b5d9d-2638-4689-b9f0-f56a9159e7a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b83a1621263cac0b23bbd35a49fda213d2e4271a
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-peoplecart"></a><span data-ttu-id="30405-103">Didacticiel : Intégration d’Azure Active Directory à Peoplecart</span><span class="sxs-lookup"><span data-stu-id="30405-103">Tutorial: Azure Active Directory integration with Peoplecart</span></span>

<span data-ttu-id="30405-104">Ce didacticiel explique comment intégrer Peoplecart avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="30405-104">In this tutorial, you learn how to integrate Peoplecart with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="30405-105">L’intégration de Peoplecart à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="30405-105">Integrating Peoplecart with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="30405-106">Dans Azure AD, vous pouvez contrôler qui a accès à Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="30405-106">You can control in Azure AD who has access to Peoplecart</span></span>
- <span data-ttu-id="30405-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Peoplecart (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30405-107">You can enable your users to automatically get signed-on to Peoplecart (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="30405-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="30405-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="30405-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="30405-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30405-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="30405-110">Prerequisites</span></span>

<span data-ttu-id="30405-111">Pour configurer l’intégration de Peoplecart à Azure AD, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="30405-111">To configure Azure AD integration with Peoplecart, you need the following items:</span></span>

- <span data-ttu-id="30405-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="30405-112">An Azure AD subscription</span></span>
- <span data-ttu-id="30405-113">Un abonnement Peoplecart pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="30405-113">A Peoplecart single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="30405-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="30405-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="30405-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="30405-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="30405-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="30405-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="30405-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="30405-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="30405-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="30405-118">Scenario description</span></span>
<span data-ttu-id="30405-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="30405-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="30405-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="30405-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="30405-121">Ajout de Peoplecart à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="30405-121">Adding Peoplecart from the gallery</span></span>
2. <span data-ttu-id="30405-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="30405-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-peoplecart-from-the-gallery"></a><span data-ttu-id="30405-123">Ajout de Peoplecart à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="30405-123">Adding Peoplecart from the gallery</span></span>
<span data-ttu-id="30405-124">Pour configurer l’intégration de Peoplecart à Azure AD, vous devez ajouter Peoplecart, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="30405-124">To configure the integration of Peoplecart into Azure AD, you need to add Peoplecart from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="30405-125">**Pour ajouter Peoplecart à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="30405-125">**To add Peoplecart from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="30405-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30405-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="30405-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="30405-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="30405-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="30405-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="30405-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="30405-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="30405-133">Dans la zone de recherche, tapez **Peoplecart**, sélectionnez **Peoplecart** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="30405-133">In the search box, type **Peoplecart**, select **Peoplecart** from result panel then click **Add** button to add the application.</span></span>

    ![Peoplecart dans la liste des résultats](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="30405-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="30405-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="30405-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Peoplecart avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="30405-136">In this section, you configure and test Azure AD single sign-on with Peoplecart based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="30405-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Peoplecart équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30405-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Peoplecart is to a user in Azure AD.</span></span> <span data-ttu-id="30405-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Peoplecart associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="30405-138">In other words, a link relationship between an Azure AD user and the related user in Peoplecart needs to be established.</span></span>

<span data-ttu-id="30405-139">Dans Peoplecart, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="30405-139">In Peoplecart, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="30405-140">Pour configurer et tester l’authentification unique Azure AD avec Peoplecart, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="30405-140">To configure and test Azure AD single sign-on with Peoplecart, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="30405-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="30405-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="30405-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="30405-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="30405-143">**[Créer un utilisateur de test Peoplecart](#create-a-peoplecart-test-user)** pour avoir un équivalent de Britta Simon dans Peoplecart lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="30405-143">**[Create a Peoplecart test user](#create-a-peoplecart-test-user)** - to have a counterpart of Britta Simon in Peoplecart that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="30405-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30405-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="30405-145">**[Tester l’authentification unique](#test-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="30405-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="30405-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="30405-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="30405-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="30405-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Peoplecart application.</span></span>

<span data-ttu-id="30405-148">**Pour configurer l’authentification unique Azure AD avec Peoplecart, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="30405-148">**To configure Azure AD single sign-on with Peoplecart, perform the following steps:**</span></span>

1. <span data-ttu-id="30405-149">Dans le portail Azure, sur la page d’intégration de l’application **Peoplecart**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="30405-149">In the Azure portal, on the **Peoplecart** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="30405-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="30405-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_samlbase.png)

3. <span data-ttu-id="30405-153">Dans la section **Domaine et URL Peoplecart**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="30405-153">On the **Peoplecart Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_url.png)

    <span data-ttu-id="30405-155">a.</span><span class="sxs-lookup"><span data-stu-id="30405-155">a.</span></span> <span data-ttu-id="30405-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<tenantname>.peoplecart.com/SignIn.aspx`</span><span class="sxs-lookup"><span data-stu-id="30405-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.peoplecart.com/SignIn.aspx`</span></span>

    <span data-ttu-id="30405-157">b.</span><span class="sxs-lookup"><span data-stu-id="30405-157">b.</span></span> <span data-ttu-id="30405-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<tenantname>.peoplecart.com`</span><span class="sxs-lookup"><span data-stu-id="30405-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.peoplecart.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="30405-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="30405-159">These values are not real.</span></span> <span data-ttu-id="30405-160">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="30405-160">Update these values with the actual Sign-On URL, and Identifier.</span></span> <span data-ttu-id="30405-161">Pour obtenir ces valeurs, contactez [l’équipe du support client Peoplecart](https://peoplecart.com/ContactUs.aspx).</span><span class="sxs-lookup"><span data-stu-id="30405-161">Contact [Peoplecart Client support team](https://peoplecart.com/ContactUs.aspx) to get these values.</span></span> 
 
4. <span data-ttu-id="30405-162">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="30405-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_certificate.png) 

5. <span data-ttu-id="30405-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="30405-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-peoplecart-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="30405-166">Dans la section **Configuration de Peoplecart**, cliquez sur **Configurer Peoplecart** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="30405-166">On the **Peoplecart Configuration** section, click **Configure Peoplecart** to open **Configure sign-on** window.</span></span> <span data-ttu-id="30405-167">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="30405-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration de Peoplecart](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_configure.png) 

7. <span data-ttu-id="30405-169">Pour configurer l’authentification unique du côté **Peoplecart**, vous devez envoyer le fichier **XML de métadonnées** et **l’URL du service d’authentification unique SAML** téléchargés à [l’équipe du support technique de Peoplecart](https://peoplecart.com/ContactUs.aspx).</span><span class="sxs-lookup"><span data-stu-id="30405-169">To configure single sign-on on **Peoplecart** side, you need to send the downloaded **Metadata XML** and **SAML Single Sign-On Service URL** to [Peoplecart support team](https://peoplecart.com/ContactUs.aspx).</span></span> <span data-ttu-id="30405-170">Celles-ci configurent ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="30405-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="30405-171">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="30405-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="30405-172">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="30405-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="30405-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="30405-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="30405-174">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="30405-174">Create an Azure AD test user</span></span>
<span data-ttu-id="30405-175">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="30405-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="30405-177">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="30405-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="30405-178">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30405-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="30405-180">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="30405-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="30405-182">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="30405-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="30405-184">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="30405-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-peoplecart-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="30405-186">a.</span><span class="sxs-lookup"><span data-stu-id="30405-186">a.</span></span> <span data-ttu-id="30405-187">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="30405-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="30405-188">b.</span><span class="sxs-lookup"><span data-stu-id="30405-188">b.</span></span> <span data-ttu-id="30405-189">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="30405-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="30405-190">c.</span><span class="sxs-lookup"><span data-stu-id="30405-190">c.</span></span> <span data-ttu-id="30405-191">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="30405-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="30405-192">d.</span><span class="sxs-lookup"><span data-stu-id="30405-192">d.</span></span> <span data-ttu-id="30405-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="30405-193">Click **Create**.</span></span>
 
### <a name="create-a-peoplecart-test-user"></a><span data-ttu-id="30405-194">Créer un utilisateur de test Peoplecart</span><span class="sxs-lookup"><span data-stu-id="30405-194">Create a Peoplecart test user</span></span>

<span data-ttu-id="30405-195">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="30405-195">In this section, you create a user called Britta Simon in Peoplecart.</span></span> <span data-ttu-id="30405-196">Collaborez avec l’[équipe du support technique Peoplecart](https://peoplecart.com/ContactUs.aspx) pour ajouter des utilisateurs dans la plate-forme Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="30405-196">Work with [Peoplecart support team](https://peoplecart.com/ContactUs.aspx) to add the users in the Peoplecart platform.</span></span> <span data-ttu-id="30405-197">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="30405-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="30405-198">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="30405-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="30405-199">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Peoplecart.</span><span class="sxs-lookup"><span data-stu-id="30405-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Peoplecart.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="30405-201">**Pour affecter Britta Simon à Peoplecart, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="30405-201">**To assign Britta Simon to Peoplecart, perform the following steps:**</span></span>

1. <span data-ttu-id="30405-202">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="30405-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="30405-204">Dans la liste des applications, sélectionnez **Peoplecart**.</span><span class="sxs-lookup"><span data-stu-id="30405-204">In the applications list, select **Peoplecart**.</span></span>

    ![Lien Peoplecart dans la liste des applications](./media/active-directory-saas-peoplecart-tutorial/tutorial_peoplecart_app.png) 

3. <span data-ttu-id="30405-206">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="30405-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202] 

4. <span data-ttu-id="30405-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="30405-208">Click **Add** button.</span></span> <span data-ttu-id="30405-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="30405-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="30405-211">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="30405-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="30405-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="30405-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="30405-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="30405-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="30405-214">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="30405-214">Test single sign-on</span></span>

<span data-ttu-id="30405-215">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="30405-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="30405-216">Lorsque vous cliquez sur la vignette Peoplecart dans le volet d’accès, la page de connexion de l’application Peoplecart devrait apparaître.</span><span class="sxs-lookup"><span data-stu-id="30405-216">When you click the Peoplecart tile in the Access Panel, you should get login page of Peoplecart application.</span></span>
<span data-ttu-id="30405-217">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="30405-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="30405-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="30405-218">Additional resources</span></span>

* [<span data-ttu-id="30405-219">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30405-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="30405-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="30405-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-peoplecart-tutorial/tutorial_general_203.png

