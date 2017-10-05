---
title: "Didacticiel : Intégration d’Azure Active Directory avec Voyance | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Voyance."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e860b810904fb7972d75d55d913d5622ff9a406a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="1875d-103">Didacticiel : Intégration d’Azure Active Directory à Voyance</span><span class="sxs-lookup"><span data-stu-id="1875d-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="1875d-104">Dans ce didacticiel, vous allez apprendre à intégrer Voyance à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1875d-104">In this tutorial, you learn how to integrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1875d-105">L’intégration de Voyance à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1875d-105">Integrating Voyance with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1875d-106">Dans Azure AD, vous pouvez contrôler qui a accès à Voyance</span><span class="sxs-lookup"><span data-stu-id="1875d-106">You can control in Azure AD who has access to Voyance</span></span>
- <span data-ttu-id="1875d-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Voyance (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="1875d-107">You can enable your users to automatically get signed-on to Voyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1875d-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="1875d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1875d-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1875d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1875d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1875d-110">Prerequisites</span></span>

<span data-ttu-id="1875d-111">Pour configurer l’intégration d’Azure AD à Voyance, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1875d-111">To configure Azure AD integration with Voyance, you need the following items:</span></span>

- <span data-ttu-id="1875d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1875d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1875d-113">Un abonnement Voyance pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1875d-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1875d-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1875d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1875d-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1875d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1875d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1875d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1875d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1875d-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1875d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1875d-118">Scenario description</span></span>
<span data-ttu-id="1875d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1875d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1875d-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="1875d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1875d-121">Ajout de Voyance à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1875d-121">Adding Voyance from the gallery</span></span>
2. <span data-ttu-id="1875d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1875d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-the-gallery"></a><span data-ttu-id="1875d-123">Ajout de Voyance à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="1875d-123">Adding Voyance from the gallery</span></span>
<span data-ttu-id="1875d-124">Pour configurer l’intégration de Voyance à Azure AD, vous devez ajouter Voyance à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1875d-124">To configure the integration of Voyance into Azure AD, you need to add Voyance from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1875d-125">**Pour ajouter Voyance à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1875d-125">**To add Voyance from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1875d-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1875d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="1875d-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1875d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1875d-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1875d-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="1875d-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1875d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="1875d-133">Dans la zone de recherche, tapez **Voyance**, sélectionnez **Voyance** dans le panneau de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="1875d-133">In the search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button to add the application.</span></span>

    ![Voyance dans la liste des résultats](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1875d-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1875d-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1875d-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Voyance avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1875d-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1875d-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Voyance équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1875d-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Voyance is to a user in Azure AD.</span></span> <span data-ttu-id="1875d-138">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Voyance associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="1875d-138">In other words, a link relationship between an Azure AD user and the related user in Voyance needs to be established.</span></span>

<span data-ttu-id="1875d-139">Dans Voyance, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="1875d-139">In Voyance, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1875d-140">Pour configurer et tester l’authentification unique Azure AD avec Voyance, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1875d-140">To configure and test Azure AD single sign-on with Voyance, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1875d-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1875d-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1875d-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1875d-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1875d-143">**[Créer un utilisateur de test Voyance](#create-a-voyance-test-user)** pour avoir un équivalent de Britta Simon dans Voyance lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="1875d-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - to have a counterpart of Britta Simon in Voyance that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1875d-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1875d-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1875d-145">**[Tester l’authentification unique](#test-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="1875d-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1875d-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1875d-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1875d-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Voyance.</span><span class="sxs-lookup"><span data-stu-id="1875d-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="1875d-148">**Pour configurer l’authentification unique Azure AD avec Voyance, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1875d-148">**To configure Azure AD single sign-on with Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="1875d-149">Dans le portail Azure, sur la page d’intégration de l’application **Voyance**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1875d-149">In the Azure portal, on the **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="1875d-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1875d-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="1875d-153">Dans la section **Domaines et URL Voyance**, suivez les étapes ci-dessous pour configurer l’application en mode initié par **IDP** :</span><span class="sxs-lookup"><span data-stu-id="1875d-153">On the **Voyance Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Voyance pour IDP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="1875d-155">a.</span><span class="sxs-lookup"><span data-stu-id="1875d-155">a.</span></span> <span data-ttu-id="1875d-156">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="1875d-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="1875d-157">b.</span><span class="sxs-lookup"><span data-stu-id="1875d-157">b.</span></span> <span data-ttu-id="1875d-158">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="1875d-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="1875d-159">Si vous souhaitez configurer l’application en mode démarré par le **fournisseur de service**, cochez **Afficher les paramètres d’URL avancés**, puis effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1875d-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Voyance pour SP](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="1875d-161">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="1875d-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1875d-162">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1875d-162">These values are not real.</span></span> <span data-ttu-id="1875d-163">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="1875d-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="1875d-164">Pour obtenir ces valeurs, contactez [l’équipe de support technique Voyance](mailto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="1875d-164">Contact [Voyance Client support team](mailto:support@nyansa.com) to get these values.</span></span> 

5. <span data-ttu-id="1875d-165">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1875d-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Lien de téléchargement du certificat](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="1875d-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1875d-167">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="1875d-169">Dans la section **Configuration de Voyance**, cliquez sur **Configurer Voyance** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="1875d-169">On the **Voyance Configuration** section, click **Configure Voyance** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1875d-170">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="1875d-170">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration de Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="1875d-172">Dans une autre fenêtre de navigateur web, connectez-vous à votre client Voyance en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1875d-172">In a different web browser window, sign-on to your Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="1875d-173">Accédez au coin supérieur droit de la barre de navigation et cliquez sur la liste déroulante indiquant « **Acme University** ».</span><span class="sxs-lookup"><span data-stu-id="1875d-173">Go to the top right corner of the navigation bar and click on the drop-down that says "**Acme University**".</span></span>
    
    ![Configurer l’authentification unique côté application - Acme University](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="1875d-175">Cliquez sur **Paramètres d’administration**.</span><span class="sxs-lookup"><span data-stu-id="1875d-175">Click "**Admin Settings**".</span></span>

    ![Configurer l’authentification unique côté application - Paramètres d’administration](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="1875d-177">Cliquez sur l’onglet **Accès utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="1875d-177">Click "**User Access**" tab.</span></span>

    ![Configurer l’authentification unique côté application - Accès utilisateur](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="1875d-179">Cliquez sur le bouton **SSO is disabled** (L’authentification unique est désactivée) pour configurer Azure AD en tant que fournisseur d’identité à l’aide de SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="1875d-179">Click the "**SSO is disabled**" button to configure Azure AD as an IdP using SAML 2.0.</span></span>

    ![Configurer l’authentification unique côté application - Bouton SSO désactivée](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="1875d-181">Accédez à la section **SAML v2** et suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1875d-181">Go to **SAML v2** section and perform below steps:</span></span>

    ![Configurer l’authentification unique côté application - SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="1875d-183">a.</span><span class="sxs-lookup"><span data-stu-id="1875d-183">a.</span></span> <span data-ttu-id="1875d-184">Sélectionnez **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="1875d-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="1875d-185">b.</span><span class="sxs-lookup"><span data-stu-id="1875d-185">b.</span></span> <span data-ttu-id="1875d-186">Collez l’**URL du service d’authentification unique SAML**, copiée à partir du portail Azure, dans la zone de texte **IdP Login URL** (URL de connexion IdP).</span><span class="sxs-lookup"><span data-stu-id="1875d-186">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal Into the **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="1875d-187">c.</span><span class="sxs-lookup"><span data-stu-id="1875d-187">c.</span></span> <span data-ttu-id="1875d-188">Ouvrez le certificat codé en base64 que vous avez téléchargé dans le Bloc-notes, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **IdP Cert** (Certificat IdP).</span><span class="sxs-lookup"><span data-stu-id="1875d-188">Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="1875d-189">d.</span><span class="sxs-lookup"><span data-stu-id="1875d-189">d.</span></span> <span data-ttu-id="1875d-190">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="1875d-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1875d-191">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="1875d-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1875d-192">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="1875d-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1875d-193">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1875d-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1875d-194">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1875d-194">Create an Azure AD test user</span></span>

<span data-ttu-id="1875d-195">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1875d-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="1875d-197">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1875d-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1875d-198">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1875d-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1875d-200">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1875d-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1875d-202">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1875d-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1875d-204">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1875d-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1875d-206">a.</span><span class="sxs-lookup"><span data-stu-id="1875d-206">a.</span></span> <span data-ttu-id="1875d-207">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1875d-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1875d-208">b.</span><span class="sxs-lookup"><span data-stu-id="1875d-208">b.</span></span> <span data-ttu-id="1875d-209">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1875d-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1875d-210">c.</span><span class="sxs-lookup"><span data-stu-id="1875d-210">c.</span></span> <span data-ttu-id="1875d-211">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1875d-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1875d-212">d.</span><span class="sxs-lookup"><span data-stu-id="1875d-212">d.</span></span> <span data-ttu-id="1875d-213">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1875d-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="1875d-214">Créer un utilisateur de test Voyance</span><span class="sxs-lookup"><span data-stu-id="1875d-214">Create a Voyance test user</span></span>

<span data-ttu-id="1875d-215">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Voyance.</span><span class="sxs-lookup"><span data-stu-id="1875d-215">The objective of this section is to create a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="1875d-216">Voyance prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="1875d-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="1875d-217">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="1875d-217">There is no action item for you in this section.</span></span> <span data-ttu-id="1875d-218">Un utilisateur est créé lors d’une tentative d’accès à Voyance s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="1875d-218">A new user is created during an attempt to access Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="1875d-219">Si vous devez créer un utilisateur manuellement, contactez [l’équipe du support technique Voyance](maiLto:support@nyansa.com).</span><span class="sxs-lookup"><span data-stu-id="1875d-219">If you need to create a user manually, you need to contact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="1875d-220">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1875d-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="1875d-221">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Voyance.</span><span class="sxs-lookup"><span data-stu-id="1875d-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Voyance.</span></span>

![Attribuer le rôle d’utilisateur][200]

<span data-ttu-id="1875d-223">**Pour affecter Britta Simon à Voyance, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1875d-223">**To assign Britta Simon to Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="1875d-224">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1875d-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1875d-226">Dans la liste des applications, sélectionnez **Voyance**.</span><span class="sxs-lookup"><span data-stu-id="1875d-226">In the applications list, select **Voyance**.</span></span>

    ![Lien Voyance dans la liste des applications](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="1875d-228">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1875d-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="1875d-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1875d-230">Click **Add** button.</span></span> <span data-ttu-id="1875d-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1875d-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="1875d-233">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1875d-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1875d-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1875d-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1875d-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1875d-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1875d-236">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1875d-236">Test single sign-on</span></span>

<span data-ttu-id="1875d-237">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="1875d-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1875d-238">Si vous cliquez sur la mosaïque Voyance dans le volet d’accès, vous devez vous connecter automatiquement à votre application Voyance.</span><span class="sxs-lookup"><span data-stu-id="1875d-238">When you click the Voyance tile in the Access Panel, you should get automatically signed-on to your Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1875d-239">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1875d-239">Additional resources</span></span>

* [<span data-ttu-id="1875d-240">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1875d-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1875d-241">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1875d-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

