---
title: "Didacticiel : Intégration d’Azure Active Directory à EasyTerritory | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et EasyTerritory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d29b362d-e986-4f67-8ff2-e158e49353aa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 46f99496397e2ed39b1d9410453dac7983ced612
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-easyterritory"></a><span data-ttu-id="950e4-103">Didacticiel : Intégration d’Azure Active Directory à EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="950e4-103">Tutorial: Azure Active Directory integration with EasyTerritory</span></span>

<span data-ttu-id="950e4-104">Dans ce didacticiel, vous découvrez comment intégrer EasyTerritory à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="950e4-104">In this tutorial, you learn how to integrate EasyTerritory with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="950e4-105">L’intégration d’EasyTerritory à Azure AD vous procure les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="950e4-105">Integrating EasyTerritory with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="950e4-106">Dans Azure AD, vous pouvez contrôler qui a accès à EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="950e4-106">You can control in Azure AD who has access to EasyTerritory.</span></span>
- <span data-ttu-id="950e4-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à EasyTerritory (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="950e4-107">You can enable your users to automatically get signed-on to EasyTerritory (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="950e4-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="950e4-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="950e4-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="950e4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="950e4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="950e4-110">Prerequisites</span></span>

<span data-ttu-id="950e4-111">Pour configurer l’intégration d’Azure AD à EasyTerritory, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="950e4-111">To configure Azure AD integration with EasyTerritory, you need the following items:</span></span>

- <span data-ttu-id="950e4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="950e4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="950e4-113">Un abonnement EasyTerritory pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="950e4-113">A EasyTerritory single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="950e4-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="950e4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="950e4-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="950e4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="950e4-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="950e4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="950e4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="950e4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="950e4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="950e4-118">Scenario description</span></span>
<span data-ttu-id="950e4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="950e4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="950e4-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="950e4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="950e4-121">Ajout d’EasyTerritory à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="950e4-121">Adding EasyTerritory from the gallery</span></span>
2. <span data-ttu-id="950e4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="950e4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-easyterritory-from-the-gallery"></a><span data-ttu-id="950e4-123">Ajout d’EasyTerritory à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="950e4-123">Adding EasyTerritory from the gallery</span></span>
<span data-ttu-id="950e4-124">Pour configurer l’intégration d’EasyTerritory dans Azure AD, vous devez ajouter EasyTerritory à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="950e4-124">To configure the integration of EasyTerritory into Azure AD, you need to add EasyTerritory from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="950e4-125">**Pour ajouter EasyTerritory à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="950e4-125">**To add EasyTerritory from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="950e4-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="950e4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="950e4-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="950e4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="950e4-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="950e4-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="950e4-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="950e4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="950e4-133">Dans la zone de recherche, tapez **EasyTerritory**, sélectionnez **EasyTerritory** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="950e4-133">In the search box, type **EasyTerritory**, select **EasyTerritory** from result panel then click **Add** button to add the application.</span></span>

    ![EasyTerritory dans la liste des résultats](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="950e4-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="950e4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="950e4-136">Dans cette section, vous configurez et vous testez l’authentification unique Azure AD avec EasyTerritory, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="950e4-136">In this section, you configure and test Azure AD single sign-on with EasyTerritory based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="950e4-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur EasyTerritory équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="950e4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in EasyTerritory is to a user in Azure AD.</span></span> <span data-ttu-id="950e4-138">En d’autres termes, une relation de liaison entre un utilisateur Azure AD et un utilisateur EasyTerritory associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="950e4-138">In other words, a link relationship between an Azure AD user and the related user in EasyTerritory needs to be established.</span></span>

<span data-ttu-id="950e4-139">Dans EasyTerritory, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="950e4-139">In EasyTerritory, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="950e4-140">Pour configurer et tester l’authentification unique Azure AD avec EasyTerritory, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="950e4-140">To configure and test Azure AD single sign-on with EasyTerritory, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="950e4-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="950e4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="950e4-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="950e4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="950e4-143">**[Créer un utilisateur de test EasyTerritory](#create-a-easyterritory-test-user)** pour avoir un équivalent de Britta Simon dans EasyTerritory lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="950e4-143">**[Create a EasyTerritory test user](#create-a-easyterritory-test-user)** - to have a counterpart of Britta Simon in EasyTerritory that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="950e4-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="950e4-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="950e4-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="950e4-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="950e4-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="950e4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="950e4-147">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et vous configurez l’authentification unique dans votre application EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="950e4-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EasyTerritory application.</span></span>

<span data-ttu-id="950e4-148">**Pour configurer l’authentification unique Azure AD avec EasyTerritory, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="950e4-148">**To configure Azure AD single sign-on with EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="950e4-149">Dans le portail Azure, dans la page d’intégration de l’application **EasyTerritory**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="950e4-149">In the Azure portal, on the **EasyTerritory** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="950e4-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="950e4-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_samlbase.png)

3. <span data-ttu-id="950e4-153">Dans la section **Domaines et URL EasyTerritory**, si vous voulez configurer l’application en Mode initié par IDP, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="950e4-153">On the **EasyTerritory Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Informations d’authentification unique dans Domaine et URL EasyTerritory](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url.png)

    <span data-ttu-id="950e4-155">a.</span><span class="sxs-lookup"><span data-stu-id="950e4-155">a.</span></span> <span data-ttu-id="950e4-156">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://apps.easyterritory.com/<tenant id>/dev/`</span><span class="sxs-lookup"><span data-stu-id="950e4-156">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/`</span></span>

    <span data-ttu-id="950e4-157">b.</span><span class="sxs-lookup"><span data-stu-id="950e4-157">b.</span></span> <span data-ttu-id="950e4-158">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span><span class="sxs-lookup"><span data-stu-id="950e4-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span></span>

4. <span data-ttu-id="950e4-159">Si vous souhaitez configurer l’application en **mode démarré par le fournisseur de service**, cochez **Afficher les paramètres d’URL avancés**, puis effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="950e4-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Informations d’authentification unique dans Domaine et URL EasyTerritory](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url1.png)

    <span data-ttu-id="950e4-161">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company name>.easyterritory.com/`</span><span class="sxs-lookup"><span data-stu-id="950e4-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.easyterritory.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="950e4-162">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="950e4-162">These values are not real.</span></span> <span data-ttu-id="950e4-163">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="950e4-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="950e4-164">Pour obtenir ces valeurs, contactez [l’équipe de support technique EasyTerritory](mailto:sales@easyterritory.com).</span><span class="sxs-lookup"><span data-stu-id="950e4-164">Contact [EasyTerritory Client support team](mailto:sales@easyterritory.com) to get these values.</span></span> 

5. <span data-ttu-id="950e4-165">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="950e4-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_certificate.png) 

6. <span data-ttu-id="950e4-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="950e4-167">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-easyterritory-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="950e4-169">Pour configurer l’authentification unique du côté **EasyTerritory**, vous devez envoyer le fichier **XML de métadonnées** téléchargé à l’[équipe de support technique d’EasyTerritory](mailto:sales@easyterritory.com).</span><span class="sxs-lookup"><span data-stu-id="950e4-169">To configure single sign-on on **EasyTerritory** side, you need to send the downloaded **Metadata XML** to [EasyTerritory support team](mailto:sales@easyterritory.com).</span></span> <span data-ttu-id="950e4-170">Celle-ci configure ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="950e4-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="950e4-171">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="950e4-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="950e4-172">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="950e4-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="950e4-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="950e4-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="950e4-174">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="950e4-174">Create an Azure AD test user</span></span>

<span data-ttu-id="950e4-175">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="950e4-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="950e4-177">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="950e4-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="950e4-178">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="950e4-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="950e4-180">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="950e4-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="950e4-182">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="950e4-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="950e4-184">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="950e4-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_04.png)

    <span data-ttu-id="950e4-186">a.</span><span class="sxs-lookup"><span data-stu-id="950e4-186">a.</span></span> <span data-ttu-id="950e4-187">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="950e4-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="950e4-188">b.</span><span class="sxs-lookup"><span data-stu-id="950e4-188">b.</span></span> <span data-ttu-id="950e4-189">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="950e4-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="950e4-190">c.</span><span class="sxs-lookup"><span data-stu-id="950e4-190">c.</span></span> <span data-ttu-id="950e4-191">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="950e4-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="950e4-192">d.</span><span class="sxs-lookup"><span data-stu-id="950e4-192">d.</span></span> <span data-ttu-id="950e4-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="950e4-193">Click **Create**.</span></span>
 
### <a name="create-a-easyterritory-test-user"></a><span data-ttu-id="950e4-194">Créer un utilisateur de test EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="950e4-194">Create a EasyTerritory test user</span></span>

<span data-ttu-id="950e4-195">Dans cette section, vous créez un utilisateur appelé Britta Simon dans EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="950e4-195">In this section, you create a user called Britta Simon in EasyTerritory.</span></span> <span data-ttu-id="950e4-196">Collaborez avec [l’équipe du support technique EasyTerritory](mailto:sales@easyterritory.com) pour ajouter les utilisateurs à la plateforme EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="950e4-196">Please work with [EasyTerritory support team](mailto:sales@easyterritory.com) to add the users in the EasyTerritory platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="950e4-197">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="950e4-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="950e4-198">Dans cette section, vous autorisez Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="950e4-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EasyTerritory.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="950e4-200">**Pour affecter Britta Simon à EasyTerritory, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="950e4-200">**To assign Britta Simon to EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="950e4-201">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="950e4-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="950e4-203">Dans la liste des applications, sélectionnez **EasyTerritory**.</span><span class="sxs-lookup"><span data-stu-id="950e4-203">In the applications list, select **EasyTerritory**.</span></span>

    ![Lien EasyTerritory dans la liste des applications](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_app.png)  

3. <span data-ttu-id="950e4-205">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="950e4-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="950e4-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="950e4-207">Click **Add** button.</span></span> <span data-ttu-id="950e4-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="950e4-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="950e4-210">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="950e4-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="950e4-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="950e4-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="950e4-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="950e4-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="950e4-213">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="950e4-213">Test single sign-on</span></span>

<span data-ttu-id="950e4-214">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="950e4-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="950e4-215">Quand vous cliquez sur la vignette EasyTerritory dans le panneau d’accès, vous devez être connecté automatiquement à votre application EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="950e4-215">When you click the EasyTerritory tile in the Access Panel, you should get automatically signed-on to your EasyTerritory application.</span></span>
<span data-ttu-id="950e4-216">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="950e4-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="950e4-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="950e4-217">Additional resources</span></span>

* [<span data-ttu-id="950e4-218">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="950e4-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="950e4-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="950e4-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)




<!--Image references-->

[1]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_203.png

