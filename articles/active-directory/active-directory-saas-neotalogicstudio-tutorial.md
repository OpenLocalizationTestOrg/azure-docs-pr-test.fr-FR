---
title: "Didacticiel : Intégration d’Azure Active Directory à Neota Logic Studio | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Neota Logic Studio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: 99018277392cab44a6b579ad45b4611739a803d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="9944f-103">Didacticiel : Intégration d’Azure Active Directory à Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="9944f-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="9944f-104">Dans ce didacticiel, vous allez apprendre à intégrer Neota Logic Studio à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9944f-104">In this tutorial, you learn how to integrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9944f-105">L’intégration de Neota Logic Studio à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9944f-105">Integrating Neota Logic Studio with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9944f-106">Dans Azure AD, vous pouvez contrôler qui a accès à Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="9944f-106">You can control in Azure AD who has access to Neota Logic Studio</span></span>
- <span data-ttu-id="9944f-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Neota Logic Studio (via l’authentification unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="9944f-107">You can enable your users to automatically get signed-on to Neota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9944f-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="9944f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9944f-109">Pour en savoir plus sur l’intégration de l’application SaaS avec Azure AD, consultez</span><span class="sxs-lookup"><span data-stu-id="9944f-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="9944f-110">[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9944f-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9944f-111">Prérequis</span><span class="sxs-lookup"><span data-stu-id="9944f-111">Prerequisites</span></span>

<span data-ttu-id="9944f-112">Pour configurer l’intégration d’Azure AD à Neota Logic Studio, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9944f-112">To configure Azure AD integration with Neota Logic Studio, you need the following items:</span></span>

- <span data-ttu-id="9944f-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9944f-113">An Azure AD subscription</span></span>
- <span data-ttu-id="9944f-114">Un abonnement Neota Logic Studio pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9944f-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9944f-115">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9944f-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9944f-116">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9944f-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9944f-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9944f-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9944f-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9944f-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9944f-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9944f-119">Scenario description</span></span>

<span data-ttu-id="9944f-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9944f-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9944f-121">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="9944f-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9944f-122">Ajout de Neota Logic Studio à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9944f-122">Adding Neota Logic Studio from the gallery</span></span>
2. <span data-ttu-id="9944f-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9944f-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-the-gallery"></a><span data-ttu-id="9944f-124">Ajout de Neota Logic Studio à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9944f-124">Adding Neota Logic Studio from the gallery</span></span>

<span data-ttu-id="9944f-125">Pour configurer l’intégration de Neota Logic Studio à Azure AD, vous devez ajouter Neota Logic Studio à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="9944f-125">To configure the integration of Neota Logic Studio into Azure AD, you need to add Neota Logic Studio from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9944f-126">**Pour ajouter Neota Logic Studio à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="9944f-126">**To add Neota Logic Studio from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9944f-127">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9944f-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9944f-129">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9944f-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9944f-130">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9944f-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9944f-132">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9944f-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9944f-134">Dans la zone de recherche, tapez **Neota Logic Studio**.</span><span class="sxs-lookup"><span data-stu-id="9944f-134">In the search box, type **Neota Logic Studio**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

5. <span data-ttu-id="9944f-136">Dans le volet de résultats, sélectionnez **Neota Logic Studio**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="9944f-136">In the results panel, select **Neota Logic Studio**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9944f-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9944f-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="9944f-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Neota Logic Studio pour un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9944f-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9944f-140">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Neota Logic Studio équivalent à un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9944f-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Neota Logic Studio is to a user in Azure AD.</span></span> <span data-ttu-id="9944f-141">En d’autres termes, une relation doit être établie entre un utilisateur Azure AD et l’utilisateur associé dans Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="9944f-141">In other words, a link relationship between an Azure AD user and the related user in Neota Logic Studio needs to be established.</span></span>

<span data-ttu-id="9944f-142">Pour cela, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** dans Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="9944f-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="9944f-143">Pour configurer et tester l’authentification unique Azure AD avec Neota Logic Studio, vous devez effectuer les actions essentielles suivantes :</span><span class="sxs-lookup"><span data-stu-id="9944f-143">To configure and test Azure AD single sign-on with Neota Logic Studio, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9944f-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9944f-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9944f-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9944f-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9944f-146">**[Création d’un utilisateur de test Neota Logic Studio](#creating-a-neota-logic-studio-test-user)** pour avoir un équivalent de Britta Simon dans Neota Logic Studio lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9944f-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - to have a counterpart of Britta Simon in Neota Logic Studio that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9944f-147">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9944f-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9944f-148">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="9944f-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9944f-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9944f-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9944f-150">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="9944f-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="9944f-151">**Pour configurer l’authentification unique Azure AD avec Neota Logic Studio, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="9944f-151">**To configure Azure AD single sign-on with Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="9944f-152">Dans le portail Azure, sur la page d’intégration de l’application **Neota Logic Studio**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9944f-152">In the Azure portal, on the **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9944f-154">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9944f-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

3. <span data-ttu-id="9944f-156">Dans la section **Domaine et URL Neota Logic Studio**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9944f-156">On the **Neota Logic Studio Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="9944f-158">a.</span><span class="sxs-lookup"><span data-stu-id="9944f-158">a.</span></span> <span data-ttu-id="9944f-159">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<sub domain>.neotalogic.com/a/<sub application>`</span><span class="sxs-lookup"><span data-stu-id="9944f-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="9944f-160">b.</span><span class="sxs-lookup"><span data-stu-id="9944f-160">b.</span></span> <span data-ttu-id="9944f-161">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="9944f-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9944f-162">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="9944f-162">These values are not the real.</span></span> <span data-ttu-id="9944f-163">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="9944f-163">Update these values with the actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="9944f-164">Nous vous suggérons d’utiliser ici la valeur de chaîne unique dans l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="9944f-164">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="9944f-165">Pour obtenir ces valeurs, contactez l’[équipe de support technique Neota Logic Studio](https://www.neotalogic.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="9944f-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="9944f-166">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9944f-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

5. <span data-ttu-id="9944f-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9944f-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9944f-170">Pour configurer l’authentification unique (SSO) pour votre application, contactez l’[équipe de support technique Neota Logic Studio](https://www.neotalogic.com/contact-us/) en lui fournissant le fichier **XML de métadonnées** téléchargé.</span><span class="sxs-lookup"><span data-stu-id="9944f-170">To get SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="9944f-171">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="9944f-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9944f-172">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="9944f-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9944f-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9944f-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9944f-174">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9944f-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="9944f-175">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9944f-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9944f-177">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9944f-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9944f-178">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9944f-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9944f-180">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9944f-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9944f-182">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9944f-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9944f-184">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9944f-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9944f-186">a.</span><span class="sxs-lookup"><span data-stu-id="9944f-186">a.</span></span> <span data-ttu-id="9944f-187">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9944f-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9944f-188">b.</span><span class="sxs-lookup"><span data-stu-id="9944f-188">b.</span></span> <span data-ttu-id="9944f-189">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9944f-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9944f-190">c.</span><span class="sxs-lookup"><span data-stu-id="9944f-190">c.</span></span> <span data-ttu-id="9944f-191">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9944f-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9944f-192">d.</span><span class="sxs-lookup"><span data-stu-id="9944f-192">d.</span></span> <span data-ttu-id="9944f-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9944f-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="9944f-194">Création d’un utilisateur de test Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="9944f-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="9944f-195">Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="9944f-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="9944f-196">Collaborez avec l’[équipe de support technique Neota Logic Studio](https://www.neotalogic.com/contact-us/) pour ajouter des utilisateurs dans la plateforme Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="9944f-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add the users in the Neota Logic Studio platform.</span></span> <span data-ttu-id="9944f-197">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9944f-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9944f-198">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9944f-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9944f-199">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en accordant l’accès à Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="9944f-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Neota Logic Studio.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9944f-201">**Pour affecter Britta Simon à Neota Logic Studio, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="9944f-201">**To assign Britta Simon to Neota Logic Studio, perform the following steps:**</span></span>

1. <span data-ttu-id="9944f-202">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9944f-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9944f-204">Dans la liste des applications, sélectionnez **Neota Logic Studio**.</span><span class="sxs-lookup"><span data-stu-id="9944f-204">In the applications list, select **Neota Logic Studio**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

3. <span data-ttu-id="9944f-206">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9944f-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9944f-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9944f-208">Click **Add** button.</span></span> <span data-ttu-id="9944f-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9944f-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9944f-211">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9944f-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9944f-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9944f-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9944f-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9944f-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9944f-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9944f-214">Testing single sign-on</span></span>

<span data-ttu-id="9944f-215">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="9944f-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9944f-216">Cliquez sur la mosaïque Neota Logic Studio dans le volet d’accès. Vous êtres alors redirigé vers la page de connexion à Organization.</span><span class="sxs-lookup"><span data-stu-id="9944f-216">Click the Neota Logic Studio tile in the Access Panel, you will be redirected to Organization sign-on page.</span></span> <span data-ttu-id="9944f-217">Une fois la connexion établie, vous êtes connecté à votre application Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="9944f-217">After successful login, you will be signed-on to your Neota Logic Studio application.</span></span> <span data-ttu-id="9944f-218">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="9944f-218">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

<span data-ttu-id="9944f-219">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="9944f-219">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9944f-220">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9944f-220">Additional resources</span></span>

* [<span data-ttu-id="9944f-221">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9944f-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9944f-222">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9944f-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_203.png

