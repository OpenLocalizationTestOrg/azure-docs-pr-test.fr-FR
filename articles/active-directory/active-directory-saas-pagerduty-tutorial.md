---
title: "Didacticiel : Intégration d’Azure Active Directory avec Pagerduty | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et PagerDuty."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0410456a-76f7-42a7-9bb5-f767de75a0e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: bf5263ce4d8fbc231029c101f167f4b55a921e60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pagerduty"></a><span data-ttu-id="016e3-103">Didacticiel : Intégration d’Azure Active Directory à Pagerduty</span><span class="sxs-lookup"><span data-stu-id="016e3-103">Tutorial: Azure Active Directory integration with PagerDuty</span></span>

<span data-ttu-id="016e3-104">Dans ce didacticiel, vous allez apprendre à intégrer PagerDuty avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="016e3-104">In this tutorial, you learn how to integrate PagerDuty with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="016e3-105">L’intégration de PagerDuty avec Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="016e3-105">Integrating PagerDuty with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="016e3-106">Dans Azure AD, vous pouvez contrôler qui a accès à PagerDuty</span><span class="sxs-lookup"><span data-stu-id="016e3-106">You can control in Azure AD who has access to PagerDuty</span></span>
- <span data-ttu-id="016e3-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à PagerDuty (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="016e3-107">You can enable your users to automatically get signed-on to PagerDuty (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="016e3-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="016e3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="016e3-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="016e3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="016e3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="016e3-110">Prerequisites</span></span>

<span data-ttu-id="016e3-111">Pour configurer l’intégration d’Azure AD avec PagerDuty, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="016e3-111">To configure Azure AD integration with PagerDuty, you need the following items:</span></span>

- <span data-ttu-id="016e3-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="016e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="016e3-113">Un abonnement PagerDuty pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="016e3-113">A PagerDuty single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="016e3-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="016e3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="016e3-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="016e3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="016e3-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="016e3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="016e3-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="016e3-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="016e3-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="016e3-118">Scenario description</span></span>
<span data-ttu-id="016e3-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="016e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="016e3-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="016e3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="016e3-121">Ajout de PagerDuty à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="016e3-121">Adding PagerDuty from the gallery</span></span>
2. <span data-ttu-id="016e3-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="016e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pagerduty-from-the-gallery"></a><span data-ttu-id="016e3-123">Ajout de PagerDuty à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="016e3-123">Adding PagerDuty from the gallery</span></span>
<span data-ttu-id="016e3-124">Pour configurer l’intégration de PagerDuty à Azure AD, vous devez ajouter PagerDuty, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="016e3-124">To configure the integration of PagerDuty into Azure AD, you need to add PagerDuty from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="016e3-125">**Pour ajouter PagerDuty à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="016e3-125">**To add PagerDuty from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="016e3-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="016e3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="016e3-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="016e3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="016e3-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="016e3-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="016e3-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="016e3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="016e3-133">Dans la zone de recherche, tapez **PagerDuty**, sélectionnez **PagerDuty** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="016e3-133">In the search box, type **PagerDuty**, select  **PagerDuty**  from result panel then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="016e3-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="016e3-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="016e3-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec PagerDuty, par le biais d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="016e3-136">In this section, you configure and test Azure AD single sign-on with PagerDuty based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="016e3-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur PagerDuty équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="016e3-137">For single sign-on to work, Azure AD needs to know what the counterpart user in PagerDuty is to a user in Azure AD.</span></span> <span data-ttu-id="016e3-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur PagerDuty associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="016e3-138">In other words, a link relationship between an Azure AD user and the related user in PagerDuty needs to be established.</span></span>

<span data-ttu-id="016e3-139">Dans PagerDuty, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="016e3-139">In PagerDuty, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="016e3-140">Pour configurer et tester l’authentification unique Azure AD avec PagerDuty, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="016e3-140">To configure and test Azure AD single sign-on with PagerDuty, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="016e3-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="016e3-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="016e3-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="016e3-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="016e3-143">**[Créer utilisateur de test PagerDuty](#create-a-pagerduty-test-user)** pour avoir un équivalent de Britta Simon dans PagerDuty lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="016e3-143">**[Create a PagerDuty test user](#create-a-pagerduty-test-user)** - to have a counterpart of Britta Simon in PagerDuty that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="016e3-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="016e3-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="016e3-145">**[Tester l’authentification unique](#test-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="016e3-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="016e3-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="016e3-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="016e3-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="016e3-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PagerDuty application.</span></span>

<span data-ttu-id="016e3-148">**Pour configurer l’authentification unique Azure AD avec PagerDuty, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="016e3-148">**To configure Azure AD single sign-on with PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="016e3-149">Dans le portail Azure, dans la page d’intégration de l’application **PagerDuty**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="016e3-149">In the Azure portal, on the **PagerDuty** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="016e3-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="016e3-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_samlbase.png)

3. <span data-ttu-id="016e3-153">Dans la section **Domaine et URL PagerDuty**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="016e3-153">On the **PagerDuty Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_url.png)

    <span data-ttu-id="016e3-155">a.</span><span class="sxs-lookup"><span data-stu-id="016e3-155">a.</span></span> <span data-ttu-id="016e3-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="016e3-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    <span data-ttu-id="016e3-157">b.</span><span class="sxs-lookup"><span data-stu-id="016e3-157">b.</span></span> <span data-ttu-id="016e3-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<tenant-name>.pagerduty.com`</span><span class="sxs-lookup"><span data-stu-id="016e3-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.pagerduty.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="016e3-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="016e3-159">These values are not real.</span></span> <span data-ttu-id="016e3-160">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="016e3-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="016e3-161">Pour obtenir ces valeurs, contactez l’[équipe de support technique PagerDuty](https://www.pagerduty.com/support/).</span><span class="sxs-lookup"><span data-stu-id="016e3-161">Contact [PagerDuty Client support team](https://www.pagerduty.com/support/) to get these values.</span></span> 

4. <span data-ttu-id="016e3-162">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="016e3-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Lien de téléchargement du certificat](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_certificate.png) 

5. <span data-ttu-id="016e3-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="016e3-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-pagerduty-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="016e3-166">Dans la section **Configuration de PagerDuty**, cliquez sur **Configurer PagerDuty** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="016e3-166">On the **PagerDuty Configuration** section, click **Configure PagerDuty** to open **Configure sign-on** window.</span></span> <span data-ttu-id="016e3-167">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="016e3-167">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration de PagerDuty](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_configure.png) 

7. <span data-ttu-id="016e3-169">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Pagerduty en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="016e3-169">In a different web browser window, log into your Pagerduty company site as an administrator.</span></span>

8. <span data-ttu-id="016e3-170">Dans le menu situé en haut, cliquez sur **Account Settings**.</span><span class="sxs-lookup"><span data-stu-id="016e3-170">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="016e3-171">![Paramètres de compte](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Paramètres de compte")</span><span class="sxs-lookup"><span data-stu-id="016e3-171">![Account Settings](./media/active-directory-saas-pagerduty-tutorial/ic778535.png "Account Settings")</span></span>

9. <span data-ttu-id="016e3-172">Cliquez sur **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="016e3-172">Click **Single Sign-on**.</span></span>
   
    <span data-ttu-id="016e3-173">![Authentification unique](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="016e3-173">![Single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778536.png "Single sign-on")</span></span>

10. <span data-ttu-id="016e3-174">Dans la page **Enable Single Sign-on (SSO)**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="016e3-174">On the **Enable Single Sign-on (SSO)** page, perform the following steps:</span></span>
   
    <span data-ttu-id="016e3-175">![Activer l’authentification unique](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "activer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="016e3-175">![Enable single sign-on](./media/active-directory-saas-pagerduty-tutorial/ic778537.png "Enable single sign-on")</span></span>
   
    <span data-ttu-id="016e3-176">a.</span><span class="sxs-lookup"><span data-stu-id="016e3-176">a.</span></span> <span data-ttu-id="016e3-177">Ouvrez dans le Bloc-notes votre certificat codé en base 64 téléchargé à partir du portail Azure, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **X.509 Certificate**.</span><span class="sxs-lookup"><span data-stu-id="016e3-177">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
  
    <span data-ttu-id="016e3-178">b.</span><span class="sxs-lookup"><span data-stu-id="016e3-178">b.</span></span> <span data-ttu-id="016e3-179">Dans la zone de texte **Login URL**, collez l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="016e3-179">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="016e3-180">c.</span><span class="sxs-lookup"><span data-stu-id="016e3-180">c.</span></span> <span data-ttu-id="016e3-181">Dans la zone de texte **Logout URL**, collez la valeur de l’**URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="016e3-181">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="016e3-182">d.</span><span class="sxs-lookup"><span data-stu-id="016e3-182">d.</span></span> <span data-ttu-id="016e3-183">Sélectionnez **Turn on Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="016e3-183">Select **Turn on Single Sign-on**.</span></span>
 
    <span data-ttu-id="016e3-184">e.</span><span class="sxs-lookup"><span data-stu-id="016e3-184">e.</span></span> <span data-ttu-id="016e3-185">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="016e3-185">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="016e3-186">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="016e3-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="016e3-187">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="016e3-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="016e3-188">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="016e3-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="016e3-189">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="016e3-189">Create an Azure AD test user</span></span>

<span data-ttu-id="016e3-190">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="016e3-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="016e3-192">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="016e3-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="016e3-193">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="016e3-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="016e3-195">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="016e3-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="016e3-197">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="016e3-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="016e3-199">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="016e3-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-pagerduty-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="016e3-201">a.</span><span class="sxs-lookup"><span data-stu-id="016e3-201">a.</span></span> <span data-ttu-id="016e3-202">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="016e3-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="016e3-203">b.</span><span class="sxs-lookup"><span data-stu-id="016e3-203">b.</span></span> <span data-ttu-id="016e3-204">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="016e3-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="016e3-205">c.</span><span class="sxs-lookup"><span data-stu-id="016e3-205">c.</span></span> <span data-ttu-id="016e3-206">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="016e3-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="016e3-207">d.</span><span class="sxs-lookup"><span data-stu-id="016e3-207">d.</span></span> <span data-ttu-id="016e3-208">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="016e3-208">Click **Create**.</span></span>
 
### <a name="create-a-pagerduty-test-user"></a><span data-ttu-id="016e3-209">Créer un utilisateur de test PagerDuty</span><span class="sxs-lookup"><span data-stu-id="016e3-209">Create a PagerDuty test user</span></span>

<span data-ttu-id="016e3-210">Pour permettre aux utilisateurs Azure AD de se connecter à Pagerduty, vous devez les approvisionner dans Pagerduty.</span><span class="sxs-lookup"><span data-stu-id="016e3-210">To enable Azure AD users to log in to PagerDuty, they must be provisioned into PagerDuty.</span></span>  
<span data-ttu-id="016e3-211">Dans le cas de Pagerduty, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="016e3-211">In the case of PagerDuty, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="016e3-212">Vous pouvez utiliser n’importe quel outil ou API de création de compte utilisateur, fourni par Pagerduty, pour approvisionner des comptes d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="016e3-212">You can use any other Pagerduty user account creation tools or APIs provided by Pagerduty to provision Azure Active Directory user accounts.</span></span>

<span data-ttu-id="016e3-213">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="016e3-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="016e3-214">Connectez-vous à votre locataire **Pagerduty** .</span><span class="sxs-lookup"><span data-stu-id="016e3-214">Log in to your **Pagerduty** tenant.</span></span>

2. <span data-ttu-id="016e3-215">Dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="016e3-215">In the menu on the top, click **Users**.</span></span>

3. <span data-ttu-id="016e3-216">Cliquez sur **Add Users**.</span><span class="sxs-lookup"><span data-stu-id="016e3-216">Click **Add Users**.</span></span>
   
    <span data-ttu-id="016e3-217">![Ajouter des utilisateurs](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "ajouter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="016e3-217">![Add Users](./media/active-directory-saas-pagerduty-tutorial/ic778539.png "Add Users")</span></span>

4.  <span data-ttu-id="016e3-218">Dans la boîte de dialogue **Invite your team**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="016e3-218">On the **Invite your team** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="016e3-219">![Inviter votre équipe](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "inviter votre équipe")</span><span class="sxs-lookup"><span data-stu-id="016e3-219">![Invite your team](./media/active-directory-saas-pagerduty-tutorial/ic778540.png "Invite your team")</span></span>

    <span data-ttu-id="016e3-220">a.</span><span class="sxs-lookup"><span data-stu-id="016e3-220">a.</span></span> <span data-ttu-id="016e3-221">Tapez le **prénom et le nom** d’un utilisateur, par exemple **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="016e3-221">Type the **First and Last Name** of user like **Britta Simon**.</span></span> 
   
    <span data-ttu-id="016e3-222">b.</span><span class="sxs-lookup"><span data-stu-id="016e3-222">b.</span></span> <span data-ttu-id="016e3-223">Entrez l’**adresse e-mail** d’un utilisateur, par exemple **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="016e3-223">Enter **Email** address of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="016e3-224">c.</span><span class="sxs-lookup"><span data-stu-id="016e3-224">c.</span></span> <span data-ttu-id="016e3-225">Cliquez sur **Add**, puis sur **Send Invites**.</span><span class="sxs-lookup"><span data-stu-id="016e3-225">Click **Add**, and then click **Send Invites**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="016e3-226">Tous les utilisateurs recevront une invitation pour créer un compte PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="016e3-226">All added users will receive an invite to create a PagerDuty account.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="016e3-227">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="016e3-227">Assign the Azure AD test user</span></span>

<span data-ttu-id="016e3-228">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="016e3-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PagerDuty.</span></span>

![Attribuer le rôle d’utilisateur][200]

<span data-ttu-id="016e3-230">**Pour affecter Britta Simon à PagerDuty, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="016e3-230">**To assign Britta Simon to PagerDuty, perform the following steps:**</span></span>

1. <span data-ttu-id="016e3-231">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="016e3-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="016e3-233">Dans la liste des applications, sélectionnez **PagerDuty**.</span><span class="sxs-lookup"><span data-stu-id="016e3-233">In the applications list, select **PagerDuty**.</span></span>

    ![Lien PagerDuty dans la liste des applications](./media/active-directory-saas-pagerduty-tutorial/tutorial_pagerduty_app.png) 

3. <span data-ttu-id="016e3-235">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="016e3-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="016e3-237">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="016e3-237">Click **Add** button.</span></span> <span data-ttu-id="016e3-238">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="016e3-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="016e3-240">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="016e3-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="016e3-241">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="016e3-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="016e3-242">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="016e3-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="016e3-243">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="016e3-243">Test single sign-on</span></span>

<span data-ttu-id="016e3-244">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="016e3-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="016e3-245">Quand vous cliquez sur la vignette PagerDuty dans le volet d’accès, vous devez être connecté automatiquement à votre application PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="016e3-245">When you click the PagerDuty tile in the Access Panelyou should get automatically signed-on to your PagerDuty application.</span></span>

<span data-ttu-id="016e3-246">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="016e3-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="016e3-247">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="016e3-247">Additional resources</span></span>

* [<span data-ttu-id="016e3-248">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="016e3-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="016e3-249">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="016e3-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pagerduty-tutorial/tutorial_general_203.png

