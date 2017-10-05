---
title: "Didacticiel : Intégration d’Azure Active Directory à Mimecast Admin Console | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Mimecast Admin Console."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: f401f592d79ad954aa466de74d3e3fbb18aa9a5b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a><span data-ttu-id="8683f-103">Didacticiel : Intégration d’Azure Active Directory à Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="8683f-103">Tutorial: Azure Active Directory integration with Mimecast Admin Console</span></span>

<span data-ttu-id="8683f-104">Dans ce didacticiel, vous allez apprendre à intégrer Mimecast Admin Console à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8683f-104">In this tutorial, you learn how to integrate Mimecast Admin Console with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8683f-105">L’intégration de Mimecast Admin Console à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8683f-105">Integrating Mimecast Admin Console with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8683f-106">Dans Azure AD, vous pouvez contrôler qui a accès à Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="8683f-106">You can control in Azure AD who has access to Mimecast Admin Console.</span></span>
- <span data-ttu-id="8683f-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Mimecast Admin Console (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8683f-107">You can enable your users to automatically get signed-on to Mimecast Admin Console (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8683f-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8683f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="8683f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8683f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8683f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8683f-110">Prerequisites</span></span>

<span data-ttu-id="8683f-111">Pour configurer l’intégration d’Azure AD à Mimecast Admin Console, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8683f-111">To configure Azure AD integration with Mimecast Admin Console, you need the following items:</span></span>

- <span data-ttu-id="8683f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8683f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8683f-113">Un abonnement Mimecast Admin Console pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8683f-113">A Mimecast Admin Console single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8683f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8683f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8683f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8683f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8683f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8683f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8683f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8683f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8683f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8683f-118">Scenario description</span></span>
<span data-ttu-id="8683f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8683f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8683f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="8683f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8683f-121">Ajout de Mimecast Admin Console à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8683f-121">Adding Mimecast Admin Console from the gallery</span></span>
2. <span data-ttu-id="8683f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8683f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-admin-console-from-the-gallery"></a><span data-ttu-id="8683f-123">Ajout de Mimecast Admin Console à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8683f-123">Adding Mimecast Admin Console from the gallery</span></span>
<span data-ttu-id="8683f-124">Pour configurer l’intégration de Mimecast Admin Console à Azure AD, vous devez ajouter Mimecast Admin Console à partir de la galerie, à votre liste d’applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="8683f-124">To configure the integration of Mimecast Admin Console into Azure AD, you need to add Mimecast Admin Console from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8683f-125">**Pour ajouter Mimecast Admin Console à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="8683f-125">**To add Mimecast Admin Console from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8683f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8683f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="8683f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8683f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8683f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8683f-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="8683f-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8683f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="8683f-133">Dans la zone de recherche, tapez **Mimecast Admin Console**, sélectionnez **Mimecast Admin Console** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="8683f-133">In the search box, type **Mimecast Admin Console**, select **Mimecast Admin Console** from result panel then click **Add** button to add the application.</span></span>

    ![Mimecast Admin Console dans la liste des résultats](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8683f-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8683f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8683f-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Mimecast Admin Console sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8683f-136">In this section, you configure and test Azure AD single sign-on with Mimecast Admin Console based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8683f-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Mimecast Admin Console équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8683f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Admin Console is to a user in Azure AD.</span></span> <span data-ttu-id="8683f-138">En d’autres termes, une relation doit être établie entre un utilisateur Azure AD et l’utilisateur Mimecast Admin Console associé.</span><span class="sxs-lookup"><span data-stu-id="8683f-138">In other words, a link relationship between an Azure AD user and the related user in Mimecast Admin Console needs to be established.</span></span>

<span data-ttu-id="8683f-139">Dans Mimecast Admin Console, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="8683f-139">In Mimecast Admin Console, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8683f-140">Pour configurer et tester l’authentification unique Azure AD avec Mimecast Admin Console, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="8683f-140">To configure and test Azure AD single sign-on with Mimecast Admin Console, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8683f-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8683f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8683f-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8683f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8683f-143">**[Création d’un utilisateur de test Mimecast Admin Console](#create-a-mimecast-admin-console-test-user)** pour obtenir un équivalent de Britta Simon dans Mimecast Admin Console lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="8683f-143">**[Create a Mimecast Admin Console test user](#create-a-mimecast-admin-console-test-user)** - to have a counterpart of Britta Simon in Mimecast Admin Console that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8683f-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8683f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8683f-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="8683f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8683f-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8683f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8683f-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="8683f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Admin Console application.</span></span>

<span data-ttu-id="8683f-148">**Pour configurer l’authentification unique Azure AD avec Mimecast Admin Console, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="8683f-148">**To configure Azure AD single sign-on with Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="8683f-149">Dans le portail Azure, dans la page d’intégration de l’application **Mimecast Admin Console**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8683f-149">In the Azure portal, on the **Mimecast Admin Console** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="8683f-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8683f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. <span data-ttu-id="8683f-153">Dans la section **Domaine et URL Mimecast Admin Console**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8683f-153">On the **Mimecast Admin Console Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    <span data-ttu-id="8683f-155">Dans la zone de texte **URL de connexion**, tapez l’URL :</span><span class="sxs-lookup"><span data-stu-id="8683f-155">In the **Sign-on URL** textbox, type the URL:</span></span>
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > <span data-ttu-id="8683f-156">L’URL d’ouverture de session est spécifique à la région.</span><span class="sxs-lookup"><span data-stu-id="8683f-156">The sign on URL is region specific.</span></span>

4. <span data-ttu-id="8683f-157">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8683f-157">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Lien de téléchargement du certificat](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. <span data-ttu-id="8683f-159">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8683f-159">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8683f-161">Dans la section **Configuration de Mimecast Admin Console**, cliquez sur **Configurer Mimecast Admin Console** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="8683f-161">On the **Mimecast Admin Console Configuration** section, click **Configure Mimecast Admin Console** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8683f-162">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="8683f-162">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration de Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. <span data-ttu-id="8683f-164">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Mimecast Admin Console en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8683f-164">In a different web browser window, log into your Mimecast Admin Console as an administrator.</span></span>

8. <span data-ttu-id="8683f-165">Accédez à **Services \> Application**.</span><span class="sxs-lookup"><span data-stu-id="8683f-165">Go to **Services \> Application**.</span></span>

    <span data-ttu-id="8683f-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span><span class="sxs-lookup"><span data-stu-id="8683f-166">![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")</span></span>

9. <span data-ttu-id="8683f-167">Cliquez sur **Authentication Profiles**.</span><span class="sxs-lookup"><span data-stu-id="8683f-167">Click **Authentication Profiles**.</span></span>

    <span data-ttu-id="8683f-168">![Profils d’authentification](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Profils d’authentification")</span><span class="sxs-lookup"><span data-stu-id="8683f-168">![Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Authentication Profiles")</span></span>
    
10. <span data-ttu-id="8683f-169">Cliquez sur **New Authentication Profile**.</span><span class="sxs-lookup"><span data-stu-id="8683f-169">Click **New Authentication Profile**.</span></span>

    <span data-ttu-id="8683f-170">![Nouveaux profils d’authentification](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "Nouveaux profils d’authentification")</span><span class="sxs-lookup"><span data-stu-id="8683f-170">![New Authentication Profiles](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "New Authentication Profiles")</span></span>

11. <span data-ttu-id="8683f-171">Dans la section **Authentication Profile** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8683f-171">In the **Authentication Profile** section, perform the following steps:</span></span>

    <span data-ttu-id="8683f-172">![Profil d’authentification](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Profil d’authentification")</span><span class="sxs-lookup"><span data-stu-id="8683f-172">![Authentication Profile](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Authentication Profile")</span></span>
    
    <span data-ttu-id="8683f-173">a.</span><span class="sxs-lookup"><span data-stu-id="8683f-173">a.</span></span> <span data-ttu-id="8683f-174">Dans la zone de texte **Description** , indiquez un nom pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="8683f-174">In the **Description** textbox, type a name for your configuration.</span></span>
    
    <span data-ttu-id="8683f-175">b.</span><span class="sxs-lookup"><span data-stu-id="8683f-175">b.</span></span> <span data-ttu-id="8683f-176">Sélectionnez **Enforce SAML Authentication for Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="8683f-176">Select **Enforce SAML Authentication for Mimecast Admin Console**.</span></span>
    
    <span data-ttu-id="8683f-177">c.</span><span class="sxs-lookup"><span data-stu-id="8683f-177">c.</span></span> <span data-ttu-id="8683f-178">Pour **Provider**, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8683f-178">As **Provider**, select **Azure Active Directory**.</span></span>
    
    <span data-ttu-id="8683f-179">d.</span><span class="sxs-lookup"><span data-stu-id="8683f-179">d.</span></span> <span data-ttu-id="8683f-180">Collez **l’ID d’entité SAML** que vous avez copié sur le portail Azure dans la zone de texte **Issuer URL** (URL de l’émetteur).</span><span class="sxs-lookup"><span data-stu-id="8683f-180">Paste **SAML Entity ID**, which you have copied from the Azure portal into the **Issuer URL** textbox.</span></span>
    
    <span data-ttu-id="8683f-181">e.</span><span class="sxs-lookup"><span data-stu-id="8683f-181">e.</span></span> <span data-ttu-id="8683f-182">Collez **l’URL du service d’authentification unique SAML**, copiée à partir du portail Azure, dans la zone de texte **Login URL** (URL de connexion).</span><span class="sxs-lookup"><span data-stu-id="8683f-182">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Login URL** textbox.</span></span>

    <span data-ttu-id="8683f-183">f.</span><span class="sxs-lookup"><span data-stu-id="8683f-183">f.</span></span> <span data-ttu-id="8683f-184">Collez **l’URL du service d’authentification unique SAML**, copiée à partir du portail Azure, dans la zone de texte **Logout URL** (URL de déconnexion).</span><span class="sxs-lookup"><span data-stu-id="8683f-184">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **Logout URL** textbox.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="8683f-185">Les valeurs d’URL de connexion et de déconnexion sont identiques pour Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="8683f-185">The Login URL value and the Logout URL value are for the Mimecast Admin Console the same.</span></span>
    
    <span data-ttu-id="8683f-186">g.</span><span class="sxs-lookup"><span data-stu-id="8683f-186">g.</span></span> <span data-ttu-id="8683f-187">Dans le Bloc-notes, ouvrez le certificat codé en base 64 que vous avez téléchargé à partir du portail Azure, supprimez la première ligne (« *--* ») et la dernière ligne (« *--* »), copiez le contenu restant dans le Presse-papiers, puis collez-le dans la zone de texte **Identity Provider Certificate (Metadata)** (Certificat du fournisseur d’identité (Métadonnées)).</span><span class="sxs-lookup"><span data-stu-id="8683f-187">Open your base-64 certificate downloaded from Azure portal in notepad, remove the first line (“*--*“) and the last line (“*--*“), copy the remaining content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>
    
    <span data-ttu-id="8683f-188">h.</span><span class="sxs-lookup"><span data-stu-id="8683f-188">h.</span></span> <span data-ttu-id="8683f-189">Sélectionnez **Allow Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="8683f-189">Select **Allow Single Sign On**.</span></span>
    
    <span data-ttu-id="8683f-190">i.</span><span class="sxs-lookup"><span data-stu-id="8683f-190">i.</span></span> <span data-ttu-id="8683f-191">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="8683f-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8683f-192">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="8683f-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8683f-193">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="8683f-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8683f-194">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8683f-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8683f-195">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8683f-195">Create an Azure AD test user</span></span>

<span data-ttu-id="8683f-196">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8683f-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="8683f-198">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8683f-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8683f-199">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8683f-199">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8683f-201">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8683f-201">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8683f-203">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8683f-203">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8683f-205">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8683f-205">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8683f-207">a.</span><span class="sxs-lookup"><span data-stu-id="8683f-207">a.</span></span> <span data-ttu-id="8683f-208">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8683f-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8683f-209">b.</span><span class="sxs-lookup"><span data-stu-id="8683f-209">b.</span></span> <span data-ttu-id="8683f-210">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8683f-210">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="8683f-211">c.</span><span class="sxs-lookup"><span data-stu-id="8683f-211">c.</span></span> <span data-ttu-id="8683f-212">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8683f-212">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="8683f-213">d.</span><span class="sxs-lookup"><span data-stu-id="8683f-213">d.</span></span> <span data-ttu-id="8683f-214">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="8683f-214">Click **Create**.</span></span>
 
### <a name="create-a-mimecast-admin-console-test-user"></a><span data-ttu-id="8683f-215">Créer un utilisateur de test Mimecast Admin Console</span><span class="sxs-lookup"><span data-stu-id="8683f-215">Create a Mimecast Admin Console test user</span></span>

<span data-ttu-id="8683f-216">Pour permettre aux utilisateurs Azure AD de se connecter à Mimecast Admin Console, vous devez les approvisionner dans Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="8683f-216">In order to enable Azure AD users to log into Mimecast Admin Console, they must be provisioned into Mimecast Admin Console.</span></span> <span data-ttu-id="8683f-217">Dans le cas de Mimecast Admin Console, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="8683f-217">In the case of Mimecast Admin Console, provisioning is a manual task.</span></span>

* <span data-ttu-id="8683f-218">Vous devez enregistrer un domaine avant de pouvoir créer des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8683f-218">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="8683f-219">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8683f-219">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="8683f-220">Connectez-vous à **Mimecast Admin Console** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8683f-220">Sign on to your **Mimecast Admin Console** as administrator.</span></span>
2. <span data-ttu-id="8683f-221">Accédez à **Directories \> Internal**.</span><span class="sxs-lookup"><span data-stu-id="8683f-221">Go to **Directories \> Internal**.</span></span>
   
   <span data-ttu-id="8683f-222">![Répertoires](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Répertoires")</span><span class="sxs-lookup"><span data-stu-id="8683f-222">![Directories](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Directories")</span></span>
3. <span data-ttu-id="8683f-223">Cliquez sur **Register New Domain**.</span><span class="sxs-lookup"><span data-stu-id="8683f-223">Click **Register New Domain**.</span></span>
   
   <span data-ttu-id="8683f-224">![Enregistrer un nouveau domaine](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Enregistrer un nouveau domaine")</span><span class="sxs-lookup"><span data-stu-id="8683f-224">![Register New Domain](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Register New Domain")</span></span>
4. <span data-ttu-id="8683f-225">Après avoir créé votre domaine, cliquez sur **New Address**.</span><span class="sxs-lookup"><span data-stu-id="8683f-225">After your new domain has been created, click **New Address**.</span></span>
   
   <span data-ttu-id="8683f-226">![Nouvelle adresse](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "Nouvelle adresse")</span><span class="sxs-lookup"><span data-stu-id="8683f-226">![New Address](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "New Address")</span></span>
5. <span data-ttu-id="8683f-227">Dans la boîte de dialogue New Address, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8683f-227">In the new address dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="8683f-228">![Enregistrer](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "enregistrer")</span><span class="sxs-lookup"><span data-stu-id="8683f-228">![Save](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "Save")</span></span>
   
   <span data-ttu-id="8683f-229">a.</span><span class="sxs-lookup"><span data-stu-id="8683f-229">a.</span></span> <span data-ttu-id="8683f-230">Tapez l’adresse e-mail, le nom global, le mot de passe et sa confirmation pour un compte Azure AD valide que vous souhaitez approvisionner dans les zones de texte correspondantes, à savoir, **Email Address**, **Global Name**, **Password** et **Confirm Password**.</span><span class="sxs-lookup"><span data-stu-id="8683f-230">Type the **Email Address**, **Global Name**, **Password**, and **Confirm Password** attributes of a valid Azure AD account you want to provision into the related textboxes.</span></span>

   <span data-ttu-id="8683f-231">b.</span><span class="sxs-lookup"><span data-stu-id="8683f-231">b.</span></span> <span data-ttu-id="8683f-232">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="8683f-232">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="8683f-233">Vous pouvez utiliser tout autre outil ou API de création de compte d’utilisateur fournis par Mimecast Admin Console, pour approvisionner des comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8683f-233">You can use any other Mimecast Admin Console user account creation tools or APIs provided by Mimecast Admin Console to provision Azure AD user accounts.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8683f-234">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8683f-234">Assign the Azure AD test user</span></span>

<span data-ttu-id="8683f-235">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="8683f-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Admin Console.</span></span>

![Attribuer le rôle utilisateur][200] 

<span data-ttu-id="8683f-237">**Pour attribuer Britta Simon à Mimecast Admin Console, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="8683f-237">**To assign Britta Simon to Mimecast Admin Console, perform the following steps:**</span></span>

1. <span data-ttu-id="8683f-238">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8683f-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8683f-240">Dans la liste des applications, sélectionnez **Mimecast Admin Console**.</span><span class="sxs-lookup"><span data-stu-id="8683f-240">In the applications list, select **Mimecast Admin Console**.</span></span>

    ![Lien Mimecast Admin Console dans la liste des applications](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. <span data-ttu-id="8683f-242">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8683f-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="8683f-244">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8683f-244">Click **Add** button.</span></span> <span data-ttu-id="8683f-245">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8683f-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="8683f-247">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8683f-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8683f-248">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8683f-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8683f-249">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8683f-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="8683f-250">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8683f-250">Test single sign-on</span></span>

<span data-ttu-id="8683f-251">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="8683f-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8683f-252">Lorsque vous cliquez sur la vignette Mimecast Admin Console dans le panneau d’accès, vous devez être connecté automatiquement à votre application Mimecast Admin Console.</span><span class="sxs-lookup"><span data-stu-id="8683f-252">When you click the Mimecast Admin Console tile in the Access Panel, you should get automatically signed-on to your Mimecast Admin Console application.</span></span>
<span data-ttu-id="8683f-253">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8683f-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8683f-254">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8683f-254">Additional resources</span></span>

* [<span data-ttu-id="8683f-255">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8683f-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8683f-256">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8683f-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

