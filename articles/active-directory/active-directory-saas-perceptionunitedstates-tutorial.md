---
title: "Didacticiel : Intégration d’Azure Active Directory à Perception United States (Non-UltiPro) | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Perception United States (Non-UltiPro)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 8e2f9f979f8b94e0c043d4db6e93bd7a53c3dd27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a><span data-ttu-id="505c0-103">Didacticiel : Intégration d’Azure Active Directory à Perception United States (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="505c0-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span></span>

<span data-ttu-id="505c0-104">Dans ce didacticiel, vous allez apprendre à intégrer Perception United States (Non-UltiPro) à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="505c0-104">In this tutorial, you learn how to integrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="505c0-105">L’intégration de Perception United States (Non-UltiPro) à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="505c0-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="505c0-106">Dans Azure AD, vous pouvez contrôler qui a accès à Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="505c0-106">You can control in Azure AD who has access to Perception United States (Non-UltiPro).</span></span>
- <span data-ttu-id="505c0-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Perception United States (Non-UltiPro) (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="505c0-107">You can enable your users to automatically get signed-on to Perception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="505c0-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="505c0-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="505c0-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="505c0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="505c0-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="505c0-110">Prerequisites</span></span>

<span data-ttu-id="505c0-111">Pour configurer l’intégration d’Azure AD avec Perception United States (Non-UltiPro), vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="505c0-111">To configure Azure AD integration with Perception United States (Non-UltiPro), you need the following items:</span></span>

- <span data-ttu-id="505c0-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="505c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="505c0-113">Un abonnement Perception United States (Non-UltiPro) pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="505c0-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="505c0-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="505c0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="505c0-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="505c0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="505c0-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="505c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="505c0-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="505c0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="505c0-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="505c0-118">Scenario description</span></span>
<span data-ttu-id="505c0-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="505c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="505c0-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="505c0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="505c0-121">Ajout de Perception United States (Non-UltiPro) à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="505c0-121">Adding Perception United States (Non-UltiPro) from the gallery</span></span>
2. <span data-ttu-id="505c0-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="505c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-perception-united-states-non-ultipro-from-the-gallery"></a><span data-ttu-id="505c0-123">Ajout de Perception United States (Non-UltiPro) à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="505c0-123">Adding Perception United States (Non-UltiPro) from the gallery</span></span>
<span data-ttu-id="505c0-124">Pour configurer l’intégration de Perception United States (Non-UltiPro) à Azure AD, vous devez ajouter Perception United States (Non-UltiPro) à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="505c0-124">To configure the integration of Perception United States (Non-UltiPro) into Azure AD, you need to add Perception United States (Non-UltiPro) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="505c0-125">**Pour ajouter Perception United States (Non-UltiPro) à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="505c0-125">**To add Perception United States (Non-UltiPro) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="505c0-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="505c0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="505c0-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="505c0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="505c0-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="505c0-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="505c0-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="505c0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="505c0-133">Dans la zone de recherche, tapez **Perception United States (Non-UltiPro)**, sélectionnez **Perception United States (Non-UltiPro)** à partir du volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="505c0-133">In the search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button to add the application.</span></span>

    ![Perception United States (Non-UltiPro) dans la liste des résultats](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="505c0-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="505c0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="505c0-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Perception United States (Non-UltiPro) grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="505c0-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="505c0-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur équivalent à l’utilisateur Azure AD dans Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="505c0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Perception United States (Non-UltiPro) is to a user in Azure AD.</span></span> <span data-ttu-id="505c0-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Perception United States (Non-UltiPro) associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="505c0-138">In other words, a link relationship between an Azure AD user and the related user in Perception United States (Non-UltiPro) needs to be established.</span></span>

<span data-ttu-id="505c0-139">Dans Perception United States (Non-UltiPro), affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="505c0-139">In Perception United States (Non-UltiPro), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="505c0-140">Pour configurer et tester l’authentification unique Azure AD avec Perception United States (Non-UltiPro), vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="505c0-140">To configure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="505c0-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="505c0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="505c0-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="505c0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="505c0-143">**[Créer un utilisateur de test Perception United States (Non-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)** pour avoir dans Perception United States (Non-UltiPro) un équivalent de Britta Simon lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="505c0-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - to have a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="505c0-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="505c0-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="505c0-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="505c0-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="505c0-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="505c0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="505c0-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="505c0-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span></span>

<span data-ttu-id="505c0-148">**Pour configurer l’intégration d’Azure AD avec Perception United States (Non-UltiPro), procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="505c0-148">**To configure Azure AD single sign-on with Perception United States (Non-UltiPro), perform the following steps:**</span></span>

1. <span data-ttu-id="505c0-149">Dans le portail Azure, sur la page d’intégration de l’application **Perception United States (Non-UltiPro)**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="505c0-149">In the Azure portal, on the **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="505c0-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="505c0-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. <span data-ttu-id="505c0-153">Dans la section **Domaine et URL Perception United States (Non-UltiPro)**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="505c0-153">On the **Perception United States (Non-UltiPro) Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification Domaine et URL Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    <span data-ttu-id="505c0-155">a.</span><span class="sxs-lookup"><span data-stu-id="505c0-155">a.</span></span> <span data-ttu-id="505c0-156">Dans la zone de texte **Identificateur**, saisissez l’URL : `https://perception.kanjoya.com/sp`</span><span class="sxs-lookup"><span data-stu-id="505c0-156">In the **Identifier** textbox, type the URL: `https://perception.kanjoya.com/sp`</span></span>

    <span data-ttu-id="505c0-157">b.</span><span class="sxs-lookup"><span data-stu-id="505c0-157">b.</span></span> <span data-ttu-id="505c0-158">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://perception.kanjoya.com/sso?idp=<entity_id>`</span><span class="sxs-lookup"><span data-stu-id="505c0-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="505c0-159">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="505c0-159">The value is not real.</span></span> <span data-ttu-id="505c0-160">Vous mettrez à jour la valeur avec l’URL de réponse réelle. La procédure est expliquée plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="505c0-160">You will update the value with the actual Reply URL, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="505c0-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="505c0-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. <span data-ttu-id="505c0-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="505c0-163">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="505c0-165">Dans la section **Configuration de Perception United States (Non-UltiPro)**, cliquez sur **Configurer Perception United States (Non-UltiPro)** pour ouvrir la fenêtre **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="505c0-165">On the **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** to open **Configure sign-on** window.</span></span> <span data-ttu-id="505c0-166">Copiez **l’ID d’entité SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="505c0-166">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="505c0-167">a.</span><span class="sxs-lookup"><span data-stu-id="505c0-167">a.</span></span> <span data-ttu-id="505c0-168">L’application **Perception United States (Non-UltiPro)** requiert le codage URI de la valeur d’**ID d’entité SAML** que vous avez copiée.</span><span class="sxs-lookup"><span data-stu-id="505c0-168">The **Perception United States (Non-UltiPro)** application requires the **SAML Entity ID** value, which you have copied, to be uri encoded.</span></span> <span data-ttu-id="505c0-169">Pour obtenir la valeur encodée en URI, utilisez le lien suivant : **http://www.url-encode-decode.com/**.</span><span class="sxs-lookup"><span data-stu-id="505c0-169">To get the uri encoded value, use the following link:**http://www.url-encode-decode.com/**.</span></span>

    <span data-ttu-id="505c0-170">b.</span><span class="sxs-lookup"><span data-stu-id="505c0-170">b.</span></span> <span data-ttu-id="505c0-171">Après l’obtention de la valeur encodée en URI, associez-la à l’**URL de réponse** comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="505c0-171">After getting the uri encoded value combine it with the **Reply URL** as mentioned below-</span></span>

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    <span data-ttu-id="505c0-172">c.</span><span class="sxs-lookup"><span data-stu-id="505c0-172">c.</span></span> <span data-ttu-id="505c0-173">Collez la valeur ci-dessus dans la zone de texte **URL de réponse** dans la section **Domaine et URL Perception United States (Non-UltiPro)**.</span><span class="sxs-lookup"><span data-stu-id="505c0-173">Paste the above value in the **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span></span>

    ![Configuration de Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. <span data-ttu-id="505c0-175">Dans une autre fenêtre de navigateur, connectez-vous à votre site d’entreprise Perception United States (Non-UltiPro) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="505c0-175">In another browser window, sign on to your Perception United States (Non-UltiPro) company site as an administrator.</span></span>

8. <span data-ttu-id="505c0-176">Dans la barre d’outils principale, cliquez sur **Paramètres du compte**.</span><span class="sxs-lookup"><span data-stu-id="505c0-176">In the main toolbar, click **Account Settings**.</span></span>

    ![Utilisateur Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. <span data-ttu-id="505c0-178">Sur la page **Paramètres du compte** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="505c0-178">On the **Account Settings** page, perform the following steps:</span></span>

    ![Utilisateur Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    <span data-ttu-id="505c0-180">a.</span><span class="sxs-lookup"><span data-stu-id="505c0-180">a.</span></span> <span data-ttu-id="505c0-181">Dans la zone de texte **Nom de l’entreprise**, entrez le nom de l’**entreprise**.</span><span class="sxs-lookup"><span data-stu-id="505c0-181">In the **Company Name** textbox, type the name of the **Company**.</span></span>
    
    <span data-ttu-id="505c0-182">b.</span><span class="sxs-lookup"><span data-stu-id="505c0-182">b.</span></span> <span data-ttu-id="505c0-183">Dans la zone de texte **Nom du compte**, entrez le nom du **compte**.</span><span class="sxs-lookup"><span data-stu-id="505c0-183">In the **Account Name** textbox, type the name of the **Account**.</span></span>

    <span data-ttu-id="505c0-184">c.</span><span class="sxs-lookup"><span data-stu-id="505c0-184">c.</span></span> <span data-ttu-id="505c0-185">Dans la zone de texte **Default Reply-To Email** (Adresse électronique de réponse par défaut), entrez une **adresse e-mail** valide.</span><span class="sxs-lookup"><span data-stu-id="505c0-185">In **Default Reply-To Email** text box, type the valid **Email**.</span></span>

    <span data-ttu-id="505c0-186">d.</span><span class="sxs-lookup"><span data-stu-id="505c0-186">d.</span></span> <span data-ttu-id="505c0-187">Sélectionnez le **fournisseur d’identité d’authentification unique** **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="505c0-187">Select **SSO Identity Provider** as **SAML 2.0**.</span></span>

10. <span data-ttu-id="505c0-188">Dans la page **Configuration SAML**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="505c0-188">On the **SSO Configuration** page, perform the following steps:</span></span>

    ![Configuration de l’authentification unique Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    <span data-ttu-id="505c0-190">a.</span><span class="sxs-lookup"><span data-stu-id="505c0-190">a.</span></span> <span data-ttu-id="505c0-191">Sélectionnez le **type de NameID SAML** **E-MAIL**.</span><span class="sxs-lookup"><span data-stu-id="505c0-191">Select **SAML NameID Type** as **EMAIL**.</span></span>

    <span data-ttu-id="505c0-192">b.</span><span class="sxs-lookup"><span data-stu-id="505c0-192">b.</span></span> <span data-ttu-id="505c0-193">Dans la zone de texte **Nom de configuration d’authentification unique**, tapez le nom de votre **configuration**.</span><span class="sxs-lookup"><span data-stu-id="505c0-193">In the **SSO Configuration Name** textbox, type the name of your **Configuration**.</span></span>
    
    <span data-ttu-id="505c0-194">c.</span><span class="sxs-lookup"><span data-stu-id="505c0-194">c.</span></span> <span data-ttu-id="505c0-195">Dans la zone de texte **Nom du fournisseur d’identité**, collez la valeur de l’**ID d’entité SAML** copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="505c0-195">In **Identity Provider Name** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="505c0-196">d.</span><span class="sxs-lookup"><span data-stu-id="505c0-196">d.</span></span> <span data-ttu-id="505c0-197">Dans la zone de texte **Domaine SAML**, entrez le domaine comme **@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="505c0-197">In **SAML Domain textbox**, enter the domain like **@contoso.com**.</span></span>

    <span data-ttu-id="505c0-198">e.</span><span class="sxs-lookup"><span data-stu-id="505c0-198">e.</span></span> <span data-ttu-id="505c0-199">Cliquez sur **Télécharger à nouveau** pour télécharger le fichier de **XML de métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="505c0-199">Click on **Upload Again** to upload the **Metadata XML** file.</span></span>

    <span data-ttu-id="505c0-200">f.</span><span class="sxs-lookup"><span data-stu-id="505c0-200">f.</span></span> <span data-ttu-id="505c0-201">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="505c0-201">Click **Update**.</span></span>


> [!TIP]
> <span data-ttu-id="505c0-202">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="505c0-202">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="505c0-203">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="505c0-203">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="505c0-204">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="505c0-204">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="505c0-205">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="505c0-205">Create an Azure AD test user</span></span>

<span data-ttu-id="505c0-206">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="505c0-206">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="505c0-208">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="505c0-208">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="505c0-209">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="505c0-209">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="505c0-211">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="505c0-211">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="505c0-213">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="505c0-213">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="505c0-215">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="505c0-215">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    <span data-ttu-id="505c0-217">a.</span><span class="sxs-lookup"><span data-stu-id="505c0-217">a.</span></span> <span data-ttu-id="505c0-218">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="505c0-218">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="505c0-219">b.</span><span class="sxs-lookup"><span data-stu-id="505c0-219">b.</span></span> <span data-ttu-id="505c0-220">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="505c0-220">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="505c0-221">c.</span><span class="sxs-lookup"><span data-stu-id="505c0-221">c.</span></span> <span data-ttu-id="505c0-222">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="505c0-222">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="505c0-223">d.</span><span class="sxs-lookup"><span data-stu-id="505c0-223">d.</span></span> <span data-ttu-id="505c0-224">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="505c0-224">Click **Create**.</span></span>
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a><span data-ttu-id="505c0-225">Créer un utilisateur de test Perception United States (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="505c0-225">Create a Perception United States (Non-UltiPro) test user</span></span>

<span data-ttu-id="505c0-226">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="505c0-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span></span> <span data-ttu-id="505c0-227">Collaborez avec l’[équipe de support Perception United States (Non-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) pour ajouter les utilisateurs dans la plateforme Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="505c0-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) to add the users in the Perception United States (Non-UltiPro) platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="505c0-228">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="505c0-228">Assign the Azure AD test user</span></span>

<span data-ttu-id="505c0-229">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="505c0-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Perception United States (Non-UltiPro).</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="505c0-231">**Pour affecter Britta Simon à Perception United States (Non-UltiPro), procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="505c0-231">**To assign Britta Simon to Perception United States (Non-UltiPro), perform the following steps:**</span></span>

1. <span data-ttu-id="505c0-232">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="505c0-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="505c0-234">Dans la liste des applications, sélectionnez **Perception United States (Non-UltiPro)**.</span><span class="sxs-lookup"><span data-stu-id="505c0-234">In the applications list, select **Perception United States (Non-UltiPro)**.</span></span>

    ![Lien Perception United States (Non-UltiPro) dans la liste des applications](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. <span data-ttu-id="505c0-236">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="505c0-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="505c0-238">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="505c0-238">Click **Add** button.</span></span> <span data-ttu-id="505c0-239">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="505c0-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="505c0-241">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="505c0-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="505c0-242">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="505c0-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="505c0-243">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="505c0-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="505c0-244">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="505c0-244">Test single sign-on</span></span>

<span data-ttu-id="505c0-245">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="505c0-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="505c0-246">Quand vous cliquez sur la vignette Perception United States (Non-UltiPro) dans le volet d’accès, vous devez être connecté automatiquement à votre application Perception United States (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="505c0-246">When you click the Perception United States (Non-UltiPro) tile in the Access Panel, you should get automatically signed-on to your Perception United States (Non-UltiPro) application.</span></span>
<span data-ttu-id="505c0-247">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="505c0-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="505c0-248">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="505c0-248">Additional resources</span></span>

* [<span data-ttu-id="505c0-249">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="505c0-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="505c0-250">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="505c0-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

