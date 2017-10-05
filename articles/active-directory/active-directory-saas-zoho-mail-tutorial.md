---
title: "Didacticiel : Intégration d’Azure Active Directory à Zoho | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Zoho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: f0688cb75584ada805b944d2ef5409d66ab37339
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="220da-103">Didacticiel : Intégration d’Azure Active Directory à Zoho</span><span class="sxs-lookup"><span data-stu-id="220da-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="220da-104">Dans ce didacticiel, vous allez apprendre à intégrer Zoho dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="220da-104">In this tutorial, you learn how to integrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="220da-105">L’intégration de Zoho dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="220da-105">Integrating Zoho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="220da-106">Dans Azure AD, vous pouvez contrôler qui a accès à Zoho.</span><span class="sxs-lookup"><span data-stu-id="220da-106">You can control in Azure AD who has access to Zoho.</span></span>
- <span data-ttu-id="220da-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Zoho (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="220da-107">You can enable your users to automatically get signed-on to Zoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="220da-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="220da-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="220da-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="220da-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="220da-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="220da-110">Prerequisites</span></span>

<span data-ttu-id="220da-111">Pour configurer l’intégration d’Azure AD avec Zoho, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="220da-111">To configure Azure AD integration with Zoho, you need the following items:</span></span>

- <span data-ttu-id="220da-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="220da-112">An Azure AD subscription</span></span>
- <span data-ttu-id="220da-113">Un abonnement Zoho pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="220da-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="220da-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="220da-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="220da-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="220da-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="220da-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="220da-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="220da-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="220da-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="220da-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="220da-118">Scenario description</span></span>
<span data-ttu-id="220da-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="220da-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="220da-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="220da-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="220da-121">Ajout de Zoho à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="220da-121">Adding Zoho from the gallery</span></span>
2. <span data-ttu-id="220da-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="220da-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-the-gallery"></a><span data-ttu-id="220da-123">Ajout de Zoho à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="220da-123">Adding Zoho from the gallery</span></span>
<span data-ttu-id="220da-124">Pour configurer l’intégration de Zoho avec Azure AD, vous devez ajouter Zoho, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="220da-124">To configure the integration of Zoho into Azure AD, you need to add Zoho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="220da-125">**Pour ajouter Zoho à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="220da-125">**To add Zoho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="220da-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="220da-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="220da-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="220da-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="220da-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="220da-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="220da-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="220da-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="220da-133">Dans la zone de recherche, tapez **Zoho**, sélectionnez **Zoho** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="220da-133">In the search box, type **Zoho**, select **Zoho** from result panel then click **Add** button to add the application.</span></span>

    ![Zoho dans la liste des résultats](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="220da-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="220da-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="220da-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Zoho avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="220da-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="220da-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Zoho équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="220da-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoho is to a user in Azure AD.</span></span> <span data-ttu-id="220da-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Zoho associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="220da-138">In other words, a link relationship between an Azure AD user and the related user in Zoho needs to be established.</span></span>

<span data-ttu-id="220da-139">Dans Zoho, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="220da-139">In Zoho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="220da-140">Pour configurer et tester l’authentification unique Azure AD avec Zoho, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="220da-140">To configure and test Azure AD single sign-on with Zoho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="220da-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="220da-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="220da-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="220da-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="220da-143">**[Créer un utilisateur de test Zoho](#create-a-zoho-test-user)** pour avoir dans Zoho un équivalent de Britta Simon lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="220da-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - to have a counterpart of Britta Simon in Zoho that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="220da-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="220da-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="220da-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="220da-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="220da-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="220da-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="220da-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Zoho.</span><span class="sxs-lookup"><span data-stu-id="220da-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="220da-148">**Pour configurer l’authentification unique Azure AD avec Zoho, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="220da-148">**To configure Azure AD single sign-on with Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="220da-149">Dans le portail Azure, sur la page d’intégration de l’application **Zoho**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="220da-149">In the Azure portal, on the **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="220da-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="220da-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="220da-153">Dans la section **Domaine et URL Zoho**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="220da-153">On the **Zoho Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="220da-155">a.</span><span class="sxs-lookup"><span data-stu-id="220da-155">a.</span></span> <span data-ttu-id="220da-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="220da-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="220da-157">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="220da-157">This value is not real.</span></span> <span data-ttu-id="220da-158">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="220da-158">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="220da-159">Pour obtenir cette valeur, contactez [l’équipe du support Zoho](https://www.zoho.com/mail/contact.html).</span><span class="sxs-lookup"><span data-stu-id="220da-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) to get this value.</span></span> 
 
4. <span data-ttu-id="220da-160">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="220da-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Lien de téléchargement du certificat](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="220da-162">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="220da-162">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="220da-164">Dans la section **Configuration de Zoho**, cliquez sur **Configurer Zoho** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="220da-164">On the **Zoho Configuration** section, click **Configure Zoho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="220da-165">Copiez **l’URL de déconnexion, l’URL de modification du mot de passe et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="220da-165">Copy the **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration de Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="220da-167">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Zoho Mail en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="220da-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="220da-168">Accédez à **Control panel**.</span><span class="sxs-lookup"><span data-stu-id="220da-168">Go to the **Control panel**.</span></span>
   
    <span data-ttu-id="220da-169">![Panneau de configuration](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Panneau de configuration")</span><span class="sxs-lookup"><span data-stu-id="220da-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="220da-170">Cliquez sur l’onglet **SAML Authentication** .</span><span class="sxs-lookup"><span data-stu-id="220da-170">Click the **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="220da-171">![Authentification SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "Authentification SAML")</span><span class="sxs-lookup"><span data-stu-id="220da-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="220da-172">Dans la section **SAML Authentication Details** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="220da-172">In the **SAML Authentication Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="220da-173">![Détails d’authentification SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Détails d’authentification SAML")</span><span class="sxs-lookup"><span data-stu-id="220da-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="220da-174">a.</span><span class="sxs-lookup"><span data-stu-id="220da-174">a.</span></span> <span data-ttu-id="220da-175">Dans la zone de texte **Login URL**, collez l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="220da-175">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="220da-176">b.</span><span class="sxs-lookup"><span data-stu-id="220da-176">b.</span></span> <span data-ttu-id="220da-177">Dans la zone de texte **Logout URL**, collez la valeur de l’**URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="220da-177">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="220da-178">c.</span><span class="sxs-lookup"><span data-stu-id="220da-178">c.</span></span> <span data-ttu-id="220da-179">Dans la zone de texte **Change Password Link**, collez l’**URL de modification de mot de passe** que vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="220da-179">In the **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="220da-180">d.</span><span class="sxs-lookup"><span data-stu-id="220da-180">d.</span></span> <span data-ttu-id="220da-181">Ouvrez dans le Bloc-notes votre certificat codé en base 64 téléchargé à partir du portail Azure, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **PublicKey**.</span><span class="sxs-lookup"><span data-stu-id="220da-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="220da-182">e.</span><span class="sxs-lookup"><span data-stu-id="220da-182">e.</span></span> <span data-ttu-id="220da-183">Comme **Algorithme**, sélectionnez **RSA**.</span><span class="sxs-lookup"><span data-stu-id="220da-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="220da-184">f.</span><span class="sxs-lookup"><span data-stu-id="220da-184">f.</span></span> <span data-ttu-id="220da-185">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="220da-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="220da-186">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="220da-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="220da-187">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="220da-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="220da-188">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="220da-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="220da-189">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="220da-189">Create an Azure AD test user</span></span>

<span data-ttu-id="220da-190">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="220da-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="220da-192">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="220da-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="220da-193">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="220da-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="220da-195">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="220da-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="220da-197">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="220da-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="220da-199">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="220da-199">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="220da-201">a.</span><span class="sxs-lookup"><span data-stu-id="220da-201">a.</span></span> <span data-ttu-id="220da-202">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="220da-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="220da-203">b.</span><span class="sxs-lookup"><span data-stu-id="220da-203">b.</span></span> <span data-ttu-id="220da-204">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="220da-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="220da-205">c.</span><span class="sxs-lookup"><span data-stu-id="220da-205">c.</span></span> <span data-ttu-id="220da-206">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="220da-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="220da-207">d.</span><span class="sxs-lookup"><span data-stu-id="220da-207">d.</span></span> <span data-ttu-id="220da-208">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="220da-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="220da-209">Créer un utilisateur de test Zoho</span><span class="sxs-lookup"><span data-stu-id="220da-209">Create a Zoho test user</span></span>

<span data-ttu-id="220da-210">Pour que les utilisateurs d’Azure AD puissent se connecter à Zoho Mail, ils doivent être approvisionnés dans Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="220da-210">In order to enable Azure AD users to log into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="220da-211">Dans le cas de Zoho Mail, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="220da-211">In the case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="220da-212">Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par Zoho Mail pour approvisionner des comptes d’utilisateurs Azure AD.</span><span class="sxs-lookup"><span data-stu-id="220da-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail to provision AAD user accounts.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="220da-213">Pour approvisionner un compte d’utilisateur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="220da-213">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="220da-214">Connectez-vous à votre site d’entreprise **Zoho Mail** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="220da-214">Log in to your **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="220da-215">Accédez à **Control Panel \> Mail & Docs**.</span><span class="sxs-lookup"><span data-stu-id="220da-215">Go to **Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="220da-216">Accédez à **User Details \> Add User**.</span><span class="sxs-lookup"><span data-stu-id="220da-216">Go to **User Details \> Add User**.</span></span>
   
    <span data-ttu-id="220da-217">![Ajouter un utilisateur](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="220da-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="220da-218">Dans la boîte de dialogue **Add users** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="220da-218">On the **Add users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="220da-219">![Ajouter un utilisateur](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="220da-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="220da-220">a.</span><span class="sxs-lookup"><span data-stu-id="220da-220">a.</span></span> <span data-ttu-id="220da-221">Dans la zone de texte **First Name**, tapez le prénom de l’utilisateur, par exemple **Britta**.</span><span class="sxs-lookup"><span data-stu-id="220da-221">In the **First Name** textbox, type the first name of user like **Britta**.</span></span>

    <span data-ttu-id="220da-222">b.</span><span class="sxs-lookup"><span data-stu-id="220da-222">b.</span></span> <span data-ttu-id="220da-223">Dans la zone de texte **Last Name**, tapez le nom de l’utilisateur, par exemple **Simon**.</span><span class="sxs-lookup"><span data-stu-id="220da-223">In the **Last Name** textbox, type the last name of user like **Simon**.</span></span>

    <span data-ttu-id="220da-224">c.</span><span class="sxs-lookup"><span data-stu-id="220da-224">c.</span></span> <span data-ttu-id="220da-225">Dans la zone de texte **Email**, tapez l’ID d’e-mail d’un utilisateur, par exemple, **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="220da-225">In the **Email ID** textbox, type the email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="220da-226">d.</span><span class="sxs-lookup"><span data-stu-id="220da-226">d.</span></span> <span data-ttu-id="220da-227">Dans la zone de texte **Password**, tapez le mot de passe de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="220da-227">In the **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="220da-228">e.</span><span class="sxs-lookup"><span data-stu-id="220da-228">e.</span></span> <span data-ttu-id="220da-229">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="220da-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="220da-230">Le titulaire du compte Azure AD reçoit un message électronique contenant un lien pour confirmer le compte avant qu’il ne soit activé.</span><span class="sxs-lookup"><span data-stu-id="220da-230">The Azure Active Directory account holder will receive an email with a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="220da-231">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="220da-231">Assign the Azure AD test user</span></span>

<span data-ttu-id="220da-232">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Zoho.</span><span class="sxs-lookup"><span data-stu-id="220da-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoho.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="220da-234">**Pour affecter Britta Simon à Zoho, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="220da-234">**To assign Britta Simon to Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="220da-235">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="220da-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="220da-237">Dans la liste des applications, sélectionnez **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="220da-237">In the applications list, select **Zoho**.</span></span>

    ![Lien Zoho dans la liste des applications](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="220da-239">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="220da-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="220da-241">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="220da-241">Click **Add** button.</span></span> <span data-ttu-id="220da-242">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="220da-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="220da-244">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="220da-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="220da-245">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="220da-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="220da-246">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="220da-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="220da-247">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="220da-247">Test single sign-on</span></span>

<span data-ttu-id="220da-248">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="220da-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="220da-249">Quand vous cliquez sur la mosaïque Zoho dans le volet d’accès, vous devez être connecté automatiquement à votre application Zoho.</span><span class="sxs-lookup"><span data-stu-id="220da-249">When you click the Zoho tile in the Access Panel, you should get automatically signed-on to your Zoho application.</span></span>
<span data-ttu-id="220da-250">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="220da-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="220da-251">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="220da-251">Additional resources</span></span>

* [<span data-ttu-id="220da-252">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="220da-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="220da-253">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="220da-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

