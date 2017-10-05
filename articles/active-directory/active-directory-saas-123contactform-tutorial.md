---
title: "Didacticiel : Intégration d’Azure Active Directory à 123ContactForm | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et 123ContactForm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3a99f0841c3e0d973168991f5dbee40e54c1d054
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="79bec-103">Didacticiel : Intégration d’Azure Active Directory à 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="79bec-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="79bec-104">Dans ce didacticiel, vous découvrez comment intégrer 123ContactForm à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79bec-104">In this tutorial, you learn how to integrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79bec-105">L’intégration de 123ContactForm à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="79bec-105">Integrating 123ContactForm with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="79bec-106">Dans Azure AD, vous pouvez contrôler qui a accès à 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="79bec-106">You can control in Azure AD who has access to 123ContactForm</span></span>
- <span data-ttu-id="79bec-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à 123ContactForm (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79bec-107">You can enable your users to automatically get signed-on to 123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79bec-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="79bec-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="79bec-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79bec-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79bec-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="79bec-110">Prerequisites</span></span>

<span data-ttu-id="79bec-111">Pour configurer l’intégration d’Azure AD à 123ContactForm, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="79bec-111">To configure Azure AD integration with 123ContactForm, you need the following items:</span></span>

- <span data-ttu-id="79bec-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="79bec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79bec-113">Un abonnement 123ContactForm pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="79bec-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79bec-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="79bec-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79bec-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="79bec-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79bec-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="79bec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79bec-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79bec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79bec-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="79bec-118">Scenario description</span></span>
<span data-ttu-id="79bec-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="79bec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79bec-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="79bec-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79bec-121">Ajout de 123ContactForm à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="79bec-121">Adding 123ContactForm from the gallery</span></span>
2. <span data-ttu-id="79bec-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="79bec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-the-gallery"></a><span data-ttu-id="79bec-123">Ajout de 123ContactForm à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="79bec-123">Adding 123ContactForm from the gallery</span></span>
<span data-ttu-id="79bec-124">Pour configurer l’intégration de 123ContactForm à Azure AD, vous devez ajouter 123ContactForm à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="79bec-124">To configure the integration of 123ContactForm into Azure AD, you need to add 123ContactForm from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="79bec-125">**Pour ajouter 123ContactForm à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="79bec-125">**To add 123ContactForm from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="79bec-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79bec-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="79bec-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="79bec-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="79bec-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="79bec-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="79bec-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="79bec-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="79bec-133">Dans la zone de recherche, tapez **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="79bec-133">In the search box, type **123ContactForm**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="79bec-135">Dans le panneau des résultats, sélectionnez **123ContactForm** puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="79bec-135">In the results panel, select **123ContactForm**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79bec-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="79bec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79bec-138">Dans cette section, vous configurez et vous testez l’authentification unique Azure AD avec 123ContactForm pour un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="79bec-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="79bec-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur 123ContactForm équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79bec-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 123ContactForm is to a user in Azure AD.</span></span> <span data-ttu-id="79bec-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur 123ContactForm associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="79bec-140">In other words, a link relationship between an Azure AD user and the related user in 123ContactForm needs to be established.</span></span>

<span data-ttu-id="79bec-141">Dans 123ContactForm, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="79bec-141">In 123ContactForm, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="79bec-142">Pour configurer et tester l’authentification unique Azure AD avec 123ContactForm, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="79bec-142">To configure and test Azure AD single sign-on with 123ContactForm, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="79bec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="79bec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="79bec-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79bec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79bec-145">**[Création d’un utilisateur de test 123ContactForm](#creating-a-123contactform-test-user)** : pour avoir un équivalent de Britta Simon dans 123ContactForm lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="79bec-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - to have a counterpart of Britta Simon in 123ContactForm that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="79bec-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79bec-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79bec-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="79bec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79bec-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="79bec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79bec-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et vous configurez l’authentification unique dans votre application 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="79bec-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="79bec-150">**Pour configurer l’authentification unique Azure AD avec 123ContactForm, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="79bec-150">**To configure Azure AD single sign-on with 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="79bec-151">Dans le portail Azure, sur la page d’intégration de l’application **123ContactForm**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="79bec-151">In the Azure portal, on the **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="79bec-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="79bec-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="79bec-155">Dans la section **Domaines et URL 123ContactForm**, si vous voulez configurer l’application en **mode lancé par le fournisseur d’identité**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="79bec-155">On the **123ContactForm Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="79bec-157">a.</span><span class="sxs-lookup"><span data-stu-id="79bec-157">a.</span></span> <span data-ttu-id="79bec-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="79bec-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="79bec-159">b.</span><span class="sxs-lookup"><span data-stu-id="79bec-159">b.</span></span> <span data-ttu-id="79bec-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span><span class="sxs-lookup"><span data-stu-id="79bec-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="79bec-161">Si vous voulez configurer l’application en **mode lancé par le fournisseur de service**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="79bec-161">If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="79bec-163">a.</span><span class="sxs-lookup"><span data-stu-id="79bec-163">a.</span></span> <span data-ttu-id="79bec-164">Cliquez sur l’option **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="79bec-164">Click the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="79bec-165">b.</span><span class="sxs-lookup"><span data-stu-id="79bec-165">b.</span></span> <span data-ttu-id="79bec-166">Dans la zone de texte **URL d’authentification**, entrez l’URL comme ceci : `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span><span class="sxs-lookup"><span data-stu-id="79bec-166">In the **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79bec-167">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="79bec-167">These values are not real.</span></span> <span data-ttu-id="79bec-168">Vous devez changer cette valeur pour les URL et l’identificateur réels. Ceci est expliqué plus loin dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="79bec-168">You'll need to update these value from actual URLs and Identifier which is explained later in the tutorial.</span></span>
    
5. <span data-ttu-id="79bec-169">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="79bec-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="79bec-171">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="79bec-171">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="79bec-173">Pour configurer l’authentification unique du côté **123ContactForm**, accédez à [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) et effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="79bec-173">To configure single sign-on on **123ContactForm** side, go to [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="79bec-175">a.</span><span class="sxs-lookup"><span data-stu-id="79bec-175">a.</span></span> <span data-ttu-id="79bec-176">Dans la zone de texte **E-mail**, entrez l’e-mail de l’utilisateur, c’est-à-dire</span><span class="sxs-lookup"><span data-stu-id="79bec-176">In the **Email** textbox, type the email of the user i.e</span></span> <span data-ttu-id="79bec-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="79bec-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="79bec-178">b.</span><span class="sxs-lookup"><span data-stu-id="79bec-178">b.</span></span> <span data-ttu-id="79bec-179">Cliquez sur **Charger** et accédez au fichier XML de métadonnées que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="79bec-179">Click **Upload** and browse the Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="79bec-180">c.</span><span class="sxs-lookup"><span data-stu-id="79bec-180">c.</span></span> <span data-ttu-id="79bec-181">Cliquez sur **Envoyer le formulaire**.</span><span class="sxs-lookup"><span data-stu-id="79bec-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="79bec-182">Dans **Microsoft Azure AD - Authentification unique - Configurer les paramètres de l’application**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="79bec-182">On the **Microsoft Azure AD - Single sign-on - Configure App Settings** perform the following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="79bec-184">a.</span><span class="sxs-lookup"><span data-stu-id="79bec-184">a.</span></span> <span data-ttu-id="79bec-185">Si vous voulez configurer l’application en **mode lancé par le fournisseur d’identité**, copiez la valeur de **IDENTIFICATEUR** pour votre instance et collez-la dans la zone de texte **Identificateur** de la section **Domaine et URL 123ContactForm** sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="79bec-185">If you wish to configure the application in **IDP initiated mode**, copy the **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="79bec-186">b.</span><span class="sxs-lookup"><span data-stu-id="79bec-186">b.</span></span> <span data-ttu-id="79bec-187">Si vous voulez configurer l’application en **mode lancé par le fournisseur d’identité**, copiez la valeur de **URL DE RÉPONSE** pour votre instance et collez-la dans la zone de texte **URL de réponse** de la section **Domaine et URL 123ContactForm** sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="79bec-187">If you wish to configure the application in **IDP initiated mode**, copy the **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="79bec-188">c.</span><span class="sxs-lookup"><span data-stu-id="79bec-188">c.</span></span> <span data-ttu-id="79bec-189">Si vous voulez configurer l’application en **mode lancé par le fournisseur de service**, copiez la valeur de **URL DE CONNEXION** pour votre instance et collez-la dans la zone de texte **URL de connexion** de la section **Domaine et URL 123ContactForm** sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="79bec-189">If you wish to configure the application in **SP initiated mode**, copy the **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="79bec-190">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="79bec-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="79bec-191">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="79bec-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="79bec-192">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79bec-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79bec-193">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="79bec-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="79bec-194">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="79bec-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="79bec-196">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="79bec-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="79bec-197">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79bec-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79bec-199">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="79bec-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79bec-201">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="79bec-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79bec-203">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="79bec-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79bec-205">a.</span><span class="sxs-lookup"><span data-stu-id="79bec-205">a.</span></span> <span data-ttu-id="79bec-206">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79bec-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79bec-207">b.</span><span class="sxs-lookup"><span data-stu-id="79bec-207">b.</span></span> <span data-ttu-id="79bec-208">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79bec-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79bec-209">c.</span><span class="sxs-lookup"><span data-stu-id="79bec-209">c.</span></span> <span data-ttu-id="79bec-210">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="79bec-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="79bec-211">d.</span><span class="sxs-lookup"><span data-stu-id="79bec-211">d.</span></span> <span data-ttu-id="79bec-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="79bec-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="79bec-213">Création d’un utilisateur de test 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="79bec-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="79bec-214">L’application prend en charge la configuration d’utilisateur juste-à-temps, et après authentification, les utilisateurs sont créés automatiquement dans l’application.</span><span class="sxs-lookup"><span data-stu-id="79bec-214">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="79bec-215">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="79bec-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="79bec-216">Dans cette section, vous autorisez Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="79bec-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 123ContactForm.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="79bec-218">**Pour affecter Britta Simon à 123ContactForm, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="79bec-218">**To assign Britta Simon to 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="79bec-219">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="79bec-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="79bec-221">Dans la liste des applications, sélectionnez **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="79bec-221">In the applications list, select **123ContactForm**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="79bec-223">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="79bec-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="79bec-225">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="79bec-225">Click **Add** button.</span></span> <span data-ttu-id="79bec-226">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="79bec-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="79bec-228">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="79bec-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="79bec-229">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="79bec-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79bec-230">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="79bec-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="79bec-231">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="79bec-231">Testing single sign-on</span></span>

<span data-ttu-id="79bec-232">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="79bec-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="79bec-233">Quand vous cliquez sur la vignette 123ContactForm dans le panneau d’accès, vous devez être connecté automatiquement à votre application 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="79bec-233">When you click the 123ContactForm tile in the Access Panel, you should get automatically signed-on to your 123ContactForm application.</span></span>
<span data-ttu-id="79bec-234">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="79bec-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79bec-235">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="79bec-235">Additional resources</span></span>

* [<span data-ttu-id="79bec-236">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79bec-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79bec-237">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="79bec-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

