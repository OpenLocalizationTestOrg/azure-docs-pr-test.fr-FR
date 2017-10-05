---
title: "Didacticiel : Intégration d’Azure Active Directory à Image Relay | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Image Relay."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65bb5990-07ef-4244-9f41-cd28fc2cb5a2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 0bfbbaee7a74df6508584b7c8846fd07c2dc15c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-image-relay"></a><span data-ttu-id="0b4af-103">Didacticiel : Intégration d’Azure Active Directory à ImageRelay</span><span class="sxs-lookup"><span data-stu-id="0b4af-103">Tutorial: Azure Active Directory integration with Image Relay</span></span>

<span data-ttu-id="0b4af-104">Dans ce didacticiel, vous allez apprendre à intégrer Image Relay avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0b4af-104">In this tutorial, you learn how to integrate Image Relay with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0b4af-105">L’intégration d’Image Relay à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="0b4af-105">Integrating Image Relay with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0b4af-106">Dans Azure AD, vous pouvez contrôler qui a accès à Image Relay.</span><span class="sxs-lookup"><span data-stu-id="0b4af-106">You can control in Azure AD who has access to Image Relay</span></span>
- <span data-ttu-id="0b4af-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Image Relay (via l’authentification unique) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b4af-107">You can enable your users to automatically get signed-on to Image Relay (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0b4af-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="0b4af-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0b4af-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0b4af-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b4af-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0b4af-110">Prerequisites</span></span>

<span data-ttu-id="0b4af-111">Pour configurer l’intégration d’Azure AD avec Image Relay, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0b4af-111">To configure Azure AD integration with Image Relay, you need the following items:</span></span>

- <span data-ttu-id="0b4af-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b4af-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0b4af-113">Un abonnement Image Relay pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="0b4af-113">An Image Relay single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0b4af-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="0b4af-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0b4af-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0b4af-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0b4af-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0b4af-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0b4af-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b4af-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0b4af-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="0b4af-118">Scenario description</span></span>
<span data-ttu-id="0b4af-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="0b4af-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0b4af-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="0b4af-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0b4af-121">Ajout d’Image Relay à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="0b4af-121">Adding Image Relay from the gallery</span></span>
2. <span data-ttu-id="0b4af-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b4af-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-image-relay-from-the-gallery"></a><span data-ttu-id="0b4af-123">Ajout d’Image Relay à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="0b4af-123">Adding Image Relay from the gallery</span></span>
<span data-ttu-id="0b4af-124">Pour configurer l’intégration d’Image Relay avec Azure AD, vous devez ajouter Image Relay à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="0b4af-124">To configure the integration of Image Relay into Azure AD, you need to add Image Relay from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0b4af-125">**Pour ajouter Image Relay à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0b4af-125">**To add Image Relay from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0b4af-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0b4af-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0b4af-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="0b4af-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0b4af-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="0b4af-133">Dans la zone de recherche, tapez **Image Relay**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-133">In the search box, type **Image Relay**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_search.png)

5. <span data-ttu-id="0b4af-135">Dans le volet de résultats, sélectionnez **Image Relay**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="0b4af-135">In the results panel, select **Image Relay**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0b4af-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b4af-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0b4af-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Image Relay, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="0b4af-138">In this section, you configure and test Azure AD single sign-on with Image Relay based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0b4af-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Image Relay équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b4af-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Image Relay is to a user in Azure AD.</span></span> <span data-ttu-id="0b4af-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Image Relay associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="0b4af-140">In other words, a link relationship between an Azure AD user and the related user in Image Relay needs to be established.</span></span>

<span data-ttu-id="0b4af-141">Dans Image Relay, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="0b4af-141">In Image Relay, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0b4af-142">Pour configurer et tester l’authentification unique Azure AD avec Image Relay, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="0b4af-142">To configure and test Azure AD single sign-on with Image Relay, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0b4af-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="0b4af-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0b4af-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b4af-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0b4af-145">**[Création d’un utilisateur de test Image Relay](#creating-an-image-relay-test-user)** pour avoir un équivalent de Britta Simon dans Image Relay lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="0b4af-145">**[Creating an Image Relay test user](#creating-an-image-relay-test-user)** - to have a counterpart of Britta Simon in Image Relay that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0b4af-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b4af-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0b4af-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="0b4af-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0b4af-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b4af-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0b4af-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Image Relay.</span><span class="sxs-lookup"><span data-stu-id="0b4af-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Image Relay application.</span></span>

<span data-ttu-id="0b4af-150">**Pour configurer l’authentification unique Azure AD avec Image Relay, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0b4af-150">**To configure Azure AD single sign-on with Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="0b4af-151">Dans le portail Azure, sur la page d’intégration de l’application **Image Relay**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-151">In the Azure portal, on the **Image Relay** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="0b4af-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0b4af-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_samlbase.png)

3. <span data-ttu-id="0b4af-155">Dans la section **Domaine et URL Image Relay**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0b4af-155">On the **Image Relay Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_url.png)

    <span data-ttu-id="0b4af-157">a.</span><span class="sxs-lookup"><span data-stu-id="0b4af-157">a.</span></span> <span data-ttu-id="0b4af-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.imagerelay.com/`</span><span class="sxs-lookup"><span data-stu-id="0b4af-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/`</span></span>

    <span data-ttu-id="0b4af-159">b.</span><span class="sxs-lookup"><span data-stu-id="0b4af-159">b.</span></span> <span data-ttu-id="0b4af-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.imagerelay.com/sso/metadata`</span><span class="sxs-lookup"><span data-stu-id="0b4af-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.imagerelay.com/sso/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0b4af-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="0b4af-161">These values are not real.</span></span> <span data-ttu-id="0b4af-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="0b4af-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0b4af-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique d’Image Relay](http://support.imagerelay.com/).</span><span class="sxs-lookup"><span data-stu-id="0b4af-163">Contact [Image Relay Client support team](http://support.imagerelay.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="0b4af-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0b4af-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_certificate.png) 

5. <span data-ttu-id="0b4af-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="0b4af-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0b4af-168">Dans la section **Configuration d’Image Relay**, cliquez sur **Configurer Image Relay** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-168">On the **Image Relay Configuration** section, click **Configure Image Relay** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0b4af-169">Copiez **l’URL du service de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-169">Copy the **Sign-Out Service URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_configure.png) 

7. <span data-ttu-id="0b4af-171">Dans une autre fenêtre de navigateur, connectez-vous à votre site d’entreprise Image Relay en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="0b4af-171">In another browser window, sign in to your Image Relay company site as an administrator.</span></span>

8. <span data-ttu-id="0b4af-172">Dans la barre d’outils du haut, cliquez sur la charge de travail **Utilisateurs et autorisations**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-172">In the toolbar on the top, click the **Users & Permissions** workload.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_06.png) 

9. <span data-ttu-id="0b4af-174">Cliquez sur **Créer une nouvelle autorisation**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-174">Click **Create New Permission**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_08.png)

10. <span data-ttu-id="0b4af-176">Dans la charge de travail **Paramètres d’authentification unique**, sélectionnez la case à cocher **Ce groupe peut se connecter uniquement via l’authentification unique**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-176">In the **Single Sign On Settings** workload, select the **This Group can only sign-in via Single Sign On** check box, and then click **Save**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_09.png) 

11. <span data-ttu-id="0b4af-178">Accédez à **Paramètres du compte**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-178">Go to **Account Settings**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_10.png) 

12. <span data-ttu-id="0b4af-180">Accédez à la charge de travail **Paramètres d’authentification unique** .</span><span class="sxs-lookup"><span data-stu-id="0b4af-180">Go to the **Single Sign On Settings** workload.</span></span>
    
     ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_11.png)

13. <span data-ttu-id="0b4af-182">Dans la boîte de dialogue **SAML Settings** (Paramètres SAML), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0b4af-182">On the **SAML Settings** dialog, perform the following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_12.png)
    
    <span data-ttu-id="0b4af-184">a.</span><span class="sxs-lookup"><span data-stu-id="0b4af-184">a.</span></span> <span data-ttu-id="0b4af-185">Dans la zone de texte **URL de connexion**, collez la valeur de **l’URL du service d’authentification unique** copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0b4af-185">In **Login URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0b4af-186">b.</span><span class="sxs-lookup"><span data-stu-id="0b4af-186">b.</span></span> <span data-ttu-id="0b4af-187">Dans la zone de texte **URL de déconnexion**, collez la valeur de **l’URL du service de déconnexion unique** copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0b4af-187">In **Logout URL**  textbox, paste the value of **Single Sign-Out Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0b4af-188">c.</span><span class="sxs-lookup"><span data-stu-id="0b4af-188">c.</span></span> <span data-ttu-id="0b4af-189">Sous **Name Id Format** (Format d’ID de nom), sélectionnez **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-189">As **Name Id Format**, select **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="0b4af-190">d.</span><span class="sxs-lookup"><span data-stu-id="0b4af-190">d.</span></span> <span data-ttu-id="0b4af-191">Sous **Binding Options for Requests from the Service Provider (Image Relay)** (Options de liaison pour les demandes provenant du fournisseur de services (ImageRelay)), sélectionnez **POST Binding** (Liaison POST).</span><span class="sxs-lookup"><span data-stu-id="0b4af-191">As **Binding Options for Requests from the Service Provider (Image Relay)**, select **POST Binding**.</span></span>

    <span data-ttu-id="0b4af-192">e.</span><span class="sxs-lookup"><span data-stu-id="0b4af-192">e.</span></span> <span data-ttu-id="0b4af-193">Sous **Certificat x.509**, cliquez sur **Mettre à jour le certificat**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-193">Under **x.509 Certificate**, click **Update Certificate**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_17.png)

    <span data-ttu-id="0b4af-195">f.</span><span class="sxs-lookup"><span data-stu-id="0b4af-195">f.</span></span> <span data-ttu-id="0b4af-196">Ouvrez le certificat que vous avez téléchargé dans le Bloc-notes, copiez son contenu, puis collez-le dans la zone de texte Certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="0b4af-196">Open the downloaded certificate in notepad, copy the content, and then paste it into the x.509 Certificate textbox.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_18.png)

    <span data-ttu-id="0b4af-198">g.</span><span class="sxs-lookup"><span data-stu-id="0b4af-198">g.</span></span> <span data-ttu-id="0b4af-199">Dans la section **Approvisionnement juste à temps des utilisateurs**, sélectionnez la case à cocher **Activer l’approvisionnement juste à temps des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-199">In **Just-In-Time User Provisioning** section, select the **Enable Just-In-Time User Provisioning**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_19.png)

    <span data-ttu-id="0b4af-201">h.</span><span class="sxs-lookup"><span data-stu-id="0b4af-201">h.</span></span> <span data-ttu-id="0b4af-202">Sélectionnez le groupe d’autorisations (par exemple, **SSO de base**) qui sera autorisé à se connecter uniquement via l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0b4af-202">Select the permission group (for example, **SSO Basic**) which is allowed to sign in only through single sign-on.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_20.png)

    <span data-ttu-id="0b4af-204">i.</span><span class="sxs-lookup"><span data-stu-id="0b4af-204">i.</span></span> <span data-ttu-id="0b4af-205">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-205">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0b4af-206">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="0b4af-206">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0b4af-207">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="0b4af-207">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0b4af-208">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0b4af-208">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0b4af-209">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b4af-209">Creating an Azure AD test user</span></span>
<span data-ttu-id="0b4af-210">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0b4af-210">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="0b4af-212">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0b4af-212">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0b4af-213">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-213">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0b4af-215">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-215">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0b4af-217">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0b4af-217">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0b4af-219">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0b4af-219">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-imagerelay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0b4af-221">a.</span><span class="sxs-lookup"><span data-stu-id="0b4af-221">a.</span></span> <span data-ttu-id="0b4af-222">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-222">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0b4af-223">b.</span><span class="sxs-lookup"><span data-stu-id="0b4af-223">b.</span></span> <span data-ttu-id="0b4af-224">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0b4af-224">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0b4af-225">c.</span><span class="sxs-lookup"><span data-stu-id="0b4af-225">c.</span></span> <span data-ttu-id="0b4af-226">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-226">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0b4af-227">d.</span><span class="sxs-lookup"><span data-stu-id="0b4af-227">d.</span></span> <span data-ttu-id="0b4af-228">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-228">Click **Create**.</span></span>
 
### <a name="creating-an-image-relay-test-user"></a><span data-ttu-id="0b4af-229">Création d’un utilisateur de test Image Relay</span><span class="sxs-lookup"><span data-stu-id="0b4af-229">Creating an Image Relay test user</span></span>

<span data-ttu-id="0b4af-230">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Image Relay.</span><span class="sxs-lookup"><span data-stu-id="0b4af-230">The objective of this section is to create a user called Britta Simon in Image Relay.</span></span>

<span data-ttu-id="0b4af-231">**Pour créer un utilisateur appelé Britta Simon dans Image Relay, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0b4af-231">**To create a user called Britta Simon in Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="0b4af-232">Connectez-vous à votre site d’entreprise Image Relay tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="0b4af-232">Sign-on to your Image Relay company site as an administrator.</span></span>

2. <span data-ttu-id="0b4af-233">Accédez à **Utilisateurs et autorisations** et sélectionnez **Créer un utilisateur SSO**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-233">Go to **Users & Permissions**     and select **Create SSO User**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_21.png) 

3. <span data-ttu-id="0b4af-235">Renseignez les champs **E-mail**, **Prénom**, **Nom** et **Société** de l’utilisateur que vous souhaitez configurer, puis sélectionnez le groupe d’autorisations (par exemple authentification unique de base), qui peut se connecter uniquement via l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0b4af-235">Enter the **Email**, **First Name**, **Last Name**, and **Company** of the user you want to provision and select the permission group (for example, SSO Basic) which is the group that can sign in only through single sign-on.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_22.png) 

4. <span data-ttu-id="0b4af-237">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-237">Click **Create**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0b4af-238">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0b4af-238">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0b4af-239">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Image Relay.</span><span class="sxs-lookup"><span data-stu-id="0b4af-239">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Image Relay.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="0b4af-241">**Pour affecter Britta Simon à Image Relay, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0b4af-241">**To assign Britta Simon to Image Relay, perform the following steps:**</span></span>

1. <span data-ttu-id="0b4af-242">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-242">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="0b4af-244">Dans la liste des applications, sélectionnez **Image Relay**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-244">In the applications list, select **Image Relay**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-imagerelay-tutorial/tutorial_imagerelay_app.png) 

3. <span data-ttu-id="0b4af-246">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-246">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="0b4af-248">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-248">Click **Add** button.</span></span> <span data-ttu-id="0b4af-249">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-249">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="0b4af-251">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0b4af-251">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0b4af-252">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-252">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0b4af-253">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0b4af-253">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0b4af-254">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0b4af-254">Testing single sign-on</span></span>

<span data-ttu-id="0b4af-255">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="0b4af-255">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>    

<span data-ttu-id="0b4af-256">Lorsque vous cliquez sur la mosaïque Image Relay dans le panneau d’accès, vous devriez être connecté automatiquement à votre application Image Relay.</span><span class="sxs-lookup"><span data-stu-id="0b4af-256">When you click the Image Relay tile in the Access Panel, you should get automatically signed-on to your Image Relay application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0b4af-257">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0b4af-257">Additional resources</span></span>

* [<span data-ttu-id="0b4af-258">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b4af-258">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0b4af-259">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="0b4af-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_04.png


[100]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-imagerelay-tutorial/tutorial_general_203.png

