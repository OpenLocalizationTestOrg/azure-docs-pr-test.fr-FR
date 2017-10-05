---
title: "Didacticiel : Intégration d’Azure Active Directory avec FileCloud | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et FileCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ad03516f684acc59912ffc57f6e0712828bd03f2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="91b99-103">Didacticiel : Intégration d’Azure Active Directory avec FileCloud</span><span class="sxs-lookup"><span data-stu-id="91b99-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="91b99-104">Dans ce didacticiel, vous allez apprendre à intégrer FileCloud à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="91b99-104">In this tutorial, you learn how to integrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91b99-105">L’intégration de FileCloud avec Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="91b99-105">Integrating FileCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="91b99-106">Dans Azure AD, vous pouvez contrôler qui a accès à FileCloud.</span><span class="sxs-lookup"><span data-stu-id="91b99-106">You can control in Azure AD who has access to FileCloud.</span></span>
- <span data-ttu-id="91b99-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à FileCloud (authentification unique) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91b99-107">You can enable your users to automatically get signed-on to FileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="91b99-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="91b99-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="91b99-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="91b99-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91b99-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="91b99-110">Prerequisites</span></span>

<span data-ttu-id="91b99-111">Pour configurer l’intégration d’Azure AD avec FileCloud, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="91b99-111">To configure Azure AD integration with FileCloud, you need the following items:</span></span>

- <span data-ttu-id="91b99-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="91b99-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91b99-113">Un abonnement FileCloud pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="91b99-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91b99-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="91b99-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91b99-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="91b99-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91b99-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="91b99-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91b99-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91b99-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91b99-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="91b99-118">Scenario description</span></span>
<span data-ttu-id="91b99-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="91b99-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91b99-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="91b99-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91b99-121">Ajout de FileCloud à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="91b99-121">Adding FileCloud from the gallery</span></span>
2. <span data-ttu-id="91b99-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="91b99-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-the-gallery"></a><span data-ttu-id="91b99-123">Ajout de FileCloud à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="91b99-123">Adding FileCloud from the gallery</span></span>
<span data-ttu-id="91b99-124">Pour configurer l’intégration de FileCloud à Azure AD, vous devez ajouter FileCloud à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="91b99-124">To configure the integration of FileCloud into Azure AD, you need to add FileCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="91b99-125">**Pour ajouter FileCloud à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="91b99-125">**To add FileCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="91b99-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="91b99-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="91b99-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="91b99-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="91b99-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="91b99-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="91b99-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="91b99-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="91b99-133">Dans la zone de recherche, tapez **FileCloud**, sélectionnez **FileCloud** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="91b99-133">In the search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button to add the application.</span></span>

    ![FileCloud dans la liste des résultats](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="91b99-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="91b99-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="91b99-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec FileCloud, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="91b99-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="91b99-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir quel est l’utilisateur FileCloud équivalent à un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91b99-137">For single sign-on to work, Azure AD needs to know what the counterpart user in FileCloud is to a user in Azure AD.</span></span> <span data-ttu-id="91b99-138">En d’autres termes, une relation doit être établie entre un utilisateur Azure AD et l’utilisateur associé dans FileCloud.</span><span class="sxs-lookup"><span data-stu-id="91b99-138">In other words, a link relationship between an Azure AD user and the related user in FileCloud needs to be established.</span></span>

<span data-ttu-id="91b99-139">Dans FileCloud, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="91b99-139">In FileCloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="91b99-140">Pour configurer et tester l’authentification unique Azure AD avec FileCloud, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="91b99-140">To configure and test Azure AD single sign-on with FileCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="91b99-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="91b99-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="91b99-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91b99-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="91b99-143">**[Créer un utilisateur de test FileCloud](#create-a-filecloud-test-user)** pour avoir un équivalent de Britta Simon dans FileCloud, lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="91b99-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - to have a counterpart of Britta Simon in FileCloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="91b99-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91b99-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="91b99-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="91b99-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="91b99-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="91b99-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="91b99-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application FileCloud.</span><span class="sxs-lookup"><span data-stu-id="91b99-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="91b99-148">**Pour configurer l’authentification unique Azure AD avec FileCloud, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="91b99-148">**To configure Azure AD single sign-on with FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="91b99-149">Sur le portail Azure, à la page d’intégration de l’application **FileCloud**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="91b99-149">In the Azure portal, on the **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="91b99-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="91b99-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. <span data-ttu-id="91b99-153">Dans la section **Domaine et URL FileCloud**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="91b99-153">On the **FileCloud Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="91b99-155">a.</span><span class="sxs-lookup"><span data-stu-id="91b99-155">a.</span></span> <span data-ttu-id="91b99-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.filecloudhosted.com`</span><span class="sxs-lookup"><span data-stu-id="91b99-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com`</span></span>

    <span data-ttu-id="91b99-157">b.</span><span class="sxs-lookup"><span data-stu-id="91b99-157">b.</span></span> <span data-ttu-id="91b99-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="91b99-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="91b99-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="91b99-159">These values are not real.</span></span> <span data-ttu-id="91b99-160">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="91b99-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="91b99-161">Pour obtenir ces valeurs, contactez l’[équipe de prise en charge des clients FileCloud](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="91b99-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) to get these values.</span></span>

4. <span data-ttu-id="91b99-162">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="91b99-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. <span data-ttu-id="91b99-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="91b99-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de Configurer l’authentification unique](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="91b99-166">Dans la section **Configuration de FileCloud**, cliquez sur **Configurer FileCloud** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="91b99-166">On the **FileCloud Configuration** section, click **Configure FileCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="91b99-167">Copiez **l’ID d’entité SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="91b99-167">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configuration de FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. <span data-ttu-id="91b99-169">Dans une autre fenêtre de navigateur web, connectez-vous à votre client FileCloud en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="91b99-169">In a different web browser window, sign-on to your FileCloud tenant as an administrator.</span></span>

8. <span data-ttu-id="91b99-170">Dans le volet de navigation gauche, cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="91b99-170">On the left navigation pane, click **Settings**.</span></span> 
   
    ![Section Paramètres côté application](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. <span data-ttu-id="91b99-172">Dans la section Paramètres, cliquez sur l’onglet **SSO**.</span><span class="sxs-lookup"><span data-stu-id="91b99-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![Onglet Authentification unique côté application](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. <span data-ttu-id="91b99-174">Dans le panneau **Single Sign On (SSO) Settings** (Paramètres d’authentification unique), sélectionnez **SAML** comme **Default SSO Type** (Type d’authentification unique par défaut).</span><span class="sxs-lookup"><span data-stu-id="91b99-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![Volet Paramètres de l’authentification unique côté application](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. <span data-ttu-id="91b99-176">Collez l’**ID d’entité SAML** que vous avez copié à partir du portail Azure dans la zone de texte **IdP End Point URL** (URL du point de terminaison IdP).</span><span class="sxs-lookup"><span data-stu-id="91b99-176">Paste **SAML Entity ID**, which you have copied from Azure portal into the **IdP End Point URL** textbox.</span></span>

    ![Zone de texte IDP End Point URL (URL du point de terminaison IdP)](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. <span data-ttu-id="91b99-178">Ouvrez votre fichier de métadonnées téléchargé dans le bloc-notes, copiez le contenu de celui-ci dans le Presse-papiers, puis collez-le dans la zone de texte **IdP Meta Data** (métadonnées IdP) du panneau **SAML Settings** (Paramètres SAML).</span><span class="sxs-lookup"><span data-stu-id="91b99-178">Open your downloaded metadata file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![Section IDP Meta Data (Métadonnées IDP) côté application](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. <span data-ttu-id="91b99-180">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="91b99-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="91b99-181">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="91b99-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="91b99-182">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="91b99-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="91b99-183">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="91b99-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="91b99-184">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="91b99-184">Create an Azure AD test user</span></span>

<span data-ttu-id="91b99-185">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="91b99-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="91b99-187">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="91b99-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="91b99-188">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="91b99-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="91b99-190">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="91b99-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="91b99-192">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="91b99-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="91b99-194">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="91b99-194">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="91b99-196">a.</span><span class="sxs-lookup"><span data-stu-id="91b99-196">a.</span></span> <span data-ttu-id="91b99-197">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="91b99-197">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91b99-198">b.</span><span class="sxs-lookup"><span data-stu-id="91b99-198">b.</span></span> <span data-ttu-id="91b99-199">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91b99-199">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="91b99-200">c.</span><span class="sxs-lookup"><span data-stu-id="91b99-200">c.</span></span> <span data-ttu-id="91b99-201">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="91b99-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="91b99-202">d.</span><span class="sxs-lookup"><span data-stu-id="91b99-202">d.</span></span> <span data-ttu-id="91b99-203">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="91b99-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="91b99-204">Créer un utilisateur de test de FileCloud</span><span class="sxs-lookup"><span data-stu-id="91b99-204">Create a FileCloud test user</span></span>

<span data-ttu-id="91b99-205">L’objectif de cette section est de créer un utilisateur nommé Britta Simon dans FileCloud.</span><span class="sxs-lookup"><span data-stu-id="91b99-205">The objective of this section is to create a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="91b99-206">FileCloud prend en charge le déploiement juste-à-temps, qui est l’option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="91b99-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="91b99-207">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="91b99-207">There is no action item for you in this section.</span></span> <span data-ttu-id="91b99-208">Un utilisateur est créé lors d’une tentative d’accès à FileCloud s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="91b99-208">A new user is created during an attempt to access FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="91b99-209">Si vous devez créer un utilisateur manuellement, contactez l’[équipe de prise en charge des clients FileCloud](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="91b99-209">If you need to create a user manually, you need to contact the [FileCloud Client support team](mailto:support@codelathe.com).</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="91b99-210">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="91b99-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="91b99-211">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à FileCloud.</span><span class="sxs-lookup"><span data-stu-id="91b99-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FileCloud.</span></span>

![Assigner le rôle d’utilisateur][200] 

<span data-ttu-id="91b99-213">**Pour affecter Britta Simon à FileCloud, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="91b99-213">**To assign Britta Simon to FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="91b99-214">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="91b99-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="91b99-216">Dans la liste des applications, sélectionnez **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="91b99-216">In the applications list, select **FileCloud**.</span></span>

    ![Lien FileCloud dans la liste Applications](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. <span data-ttu-id="91b99-218">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="91b99-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="91b99-220">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="91b99-220">Click **Add** button.</span></span> <span data-ttu-id="91b99-221">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="91b99-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="91b99-223">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="91b99-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="91b99-224">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="91b99-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="91b99-225">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="91b99-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="91b99-226">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="91b99-226">Test single sign-on</span></span>

<span data-ttu-id="91b99-227">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="91b99-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="91b99-228">Lorsque vous cliquez sur la vignette FileCloud dans le volet d’accès, vous devez être automatiquement authentifié auprès de votre application FileCloud.</span><span class="sxs-lookup"><span data-stu-id="91b99-228">When you click the FileCloud tile in the Access Panel, you should get automatically signed-on to your FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="91b99-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="91b99-229">Additional resources</span></span>

* [<span data-ttu-id="91b99-230">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91b99-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="91b99-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="91b99-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

