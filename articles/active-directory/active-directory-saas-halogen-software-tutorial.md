---
title: "Didacticiel : Intégration d’Azure Active Directory à Halogen Software | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Halogen Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: e09fa93038965e4880a23002bac6917ad2a077f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="5fc4c-103">Didacticiel : Intégration d’Azure Active Directory avec Halogen Software</span><span class="sxs-lookup"><span data-stu-id="5fc4c-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="5fc4c-104">Dans ce didacticiel, vous allez apprendre à intégrer Halogen Software à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5fc4c-104">In this tutorial, you learn how to integrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5fc4c-105">L’intégration de Halogen Software dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5fc4c-105">Integrating Halogen Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5fc4c-106">Dans Azure AD, vous pouvez contrôler qui a accès à Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-106">You can control in Azure AD who has access to Halogen Software</span></span>
- <span data-ttu-id="5fc4c-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Halogen Software (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-107">You can enable your users to automatically get signed-on to Halogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5fc4c-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="5fc4c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5fc4c-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5fc4c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5fc4c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5fc4c-110">Prerequisites</span></span>

<span data-ttu-id="5fc4c-111">Pour configurer l’intégration d’Azure AD avec Halogen Software, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5fc4c-111">To configure Azure AD integration with Halogen Software, you need the following items:</span></span>

- <span data-ttu-id="5fc4c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fc4c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5fc4c-113">Un abonnement Halogen Software pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5fc4c-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5fc4c-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5fc4c-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5fc4c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5fc4c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5fc4c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5fc4c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5fc4c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5fc4c-118">Scenario description</span></span>

<span data-ttu-id="5fc4c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5fc4c-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="5fc4c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5fc4c-121">Ajout de Halogen Software à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5fc4c-121">Adding Halogen Software from the gallery</span></span>
2. <span data-ttu-id="5fc4c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fc4c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-the-gallery"></a><span data-ttu-id="5fc4c-123">Ajout de Halogen Software à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5fc4c-123">Adding Halogen Software from the gallery</span></span>

<span data-ttu-id="5fc4c-124">Pour configurer l’intégration de Halogen Software avec Azure AD, vous devez ajouter Halogen Software, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-124">To configure the integration of Halogen Software into Azure AD, you need to add Halogen Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5fc4c-125">**Pour ajouter Halogen Software à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5fc4c-125">**To add Halogen Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5fc4c-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5fc4c-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5fc4c-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5fc4c-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5fc4c-133">Dans la zone de recherche, tapez **Halogen Software**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-133">In the search box, type **Halogen Software**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="5fc4c-135">Dans le panneau de résultats, sélectionnez **Halogen Software**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-135">In the results panel, select **Halogen Software**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5fc4c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fc4c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5fc4c-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Halogen Software à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5fc4c-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5fc4c-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Halogen Software équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Halogen Software is to a user in Azure AD.</span></span> <span data-ttu-id="5fc4c-140">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur Halogen Software associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-140">In other words, a link relationship between an Azure AD user and the related user in Halogen Software needs to be established.</span></span>

<span data-ttu-id="5fc4c-141">Dans Halogen Software, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-141">In Halogen Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5fc4c-142">Pour configurer et tester l’authentification unique Azure AD avec Halogen Software, vous avez besoin de suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="5fc4c-142">To configure and test Azure AD single sign-on with Halogen Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5fc4c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5fc4c-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5fc4c-145">**[Création d’un utilisateur de test Halogen Software](#creating-a-halogen-software-test-user)** pour avoir un équivalent de Britta Simon dans Halogen Software lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in Halogen Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5fc4c-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5fc4c-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5fc4c-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fc4c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5fc4c-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="5fc4c-150">**Pour configurer l’authentification unique Azure AD avec Halogen Software, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5fc4c-150">**To configure Azure AD single sign-on with Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="5fc4c-151">Dans le portail Azure, sur la page d’intégration de l’application **Halogen Software**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-151">In the Azure portal, on the **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5fc4c-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="5fc4c-155">Dans la section **Halogen Software Domain and URLs** (Domaine et URL Halogen Software), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5fc4c-155">On the **Halogen Software Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="5fc4c-157">a.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-157">a.</span></span> <span data-ttu-id="5fc4c-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="5fc4c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="5fc4c-159">b.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-159">b.</span></span> <span data-ttu-id="5fc4c-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="5fc4c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5fc4c-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-161">These values are not real.</span></span> <span data-ttu-id="5fc4c-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5fc4c-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique Halogen Software](https://support.halogensoftware.com/).</span><span class="sxs-lookup"><span data-stu-id="5fc4c-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) to get these values.</span></span> 
 


4. <span data-ttu-id="5fc4c-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="5fc4c-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5fc4c-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5fc4c-168">Dans une autre fenêtre de navigateur, connectez-vous à votre application **Halogen Software** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-168">In a different browser window, sign-on to your **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="5fc4c-169">Cliquez sur l’onglet **Options** .</span><span class="sxs-lookup"><span data-stu-id="5fc4c-169">Click the **Options** tab.</span></span> 
   
    ![Qu’est-ce qu’Azure AD Connect ?][12]

8. <span data-ttu-id="5fc4c-171">Dans le volet de navigation de gauche, cliquez sur **SAML Configuration**(Configuration SAML).</span><span class="sxs-lookup"><span data-stu-id="5fc4c-171">In the left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![Qu’est-ce qu’Azure AD Connect ?][13]

9. <span data-ttu-id="5fc4c-173">Dans la page **SAML Configuration** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5fc4c-173">On the **SAML Configuration** page, perform the following steps:</span></span> 

    ![Qu’est-ce qu’Azure AD Connect ?][14]

     <span data-ttu-id="5fc4c-175">a.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-175">a.</span></span> <span data-ttu-id="5fc4c-176">Dans **Unique Identifier** (Identificateur unique), sélectionnez **NameID**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="5fc4c-177">b.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-177">b.</span></span> <span data-ttu-id="5fc4c-178">Dans **Unique Identifier Maps To** (l’identificateur unique mappe vers), sélectionnez **Username** (Nom d’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="5fc4c-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="5fc4c-179">c.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-179">c.</span></span> <span data-ttu-id="5fc4c-180">Pour charger votre fichier de métadonnées téléchargé, cliquez sur **Browse** (Parcourir) pour sélectionner le fichier, puis sur **Upload File** (Charger le fichier).</span><span class="sxs-lookup"><span data-stu-id="5fc4c-180">To upload your downloaded metadata file, click **Browse** to select the file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="5fc4c-181">d.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-181">d.</span></span> <span data-ttu-id="5fc4c-182">Pour tester la configuration, cliquez sur **Run Test**(Exécuter le test).</span><span class="sxs-lookup"><span data-stu-id="5fc4c-182">To test the configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="5fc4c-183">Vous devez attendre que le message « *The SAML test is complete. Please close this window* » s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-183">You need to wait for the message "*The SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="5fc4c-184">Ensuite, fermez la fenêtre du navigateur.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-184">Then, close the opened browser window.</span></span> <span data-ttu-id="5fc4c-185">La case à cocher **Enable SAML** (Activer SAML) est sélectionnée uniquement si le test a été effectué.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-185">The **Enable SAML** checkbox is only enabled if the test has been completed.</span></span> 
     
     <span data-ttu-id="5fc4c-186">e.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-186">e.</span></span> <span data-ttu-id="5fc4c-187">Sélectionnez **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="5fc4c-188">f.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-188">f.</span></span> <span data-ttu-id="5fc4c-189">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="5fc4c-190">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5fc4c-191">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5fc4c-192">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5fc4c-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5fc4c-193">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fc4c-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="5fc4c-194">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5fc4c-196">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5fc4c-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5fc4c-197">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5fc4c-199">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5fc4c-201">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5fc4c-203">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5fc4c-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5fc4c-205">a.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-205">a.</span></span> <span data-ttu-id="5fc4c-206">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-206">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="5fc4c-207">b.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-207">b.</span></span> <span data-ttu-id="5fc4c-208">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5fc4c-209">c.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-209">c.</span></span> <span data-ttu-id="5fc4c-210">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5fc4c-211">d.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-211">d.</span></span> <span data-ttu-id="5fc4c-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="5fc4c-213">Création d’un utilisateur de test Halogen Software</span><span class="sxs-lookup"><span data-stu-id="5fc4c-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="5fc4c-214">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-214">The objective of this section is to create a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="5fc4c-215">**Pour créer un utilisateur appelé Britta Simon dans Halogen Software, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5fc4c-215">**To create a user called Britta Simon in Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="5fc4c-216">Connectez-vous à votre application **Halogen Software** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-216">Sign on to your **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="5fc4c-217">Cliquez sur l’onglet **User Center** (Centre utilisateur), puis sur **Create User** (Créer un utilisateur).</span><span class="sxs-lookup"><span data-stu-id="5fc4c-217">Click the **User Center** tab, and then click **Create User**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][300]  

3. <span data-ttu-id="5fc4c-219">Dans la boîte de dialogue **New User** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5fc4c-219">On the **New User** dialog page, perform the following steps:</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][301]

    <span data-ttu-id="5fc4c-221">a.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-221">a.</span></span> <span data-ttu-id="5fc4c-222">Dans la zone de texte **Prénom**, entrez le prénom de l’utilisateur, par exemple **Britta**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-222">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>
    
    <span data-ttu-id="5fc4c-223">b.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-223">b.</span></span> <span data-ttu-id="5fc4c-224">Dans la zone de texte **Nom**, entrez le nom de l’utilisateur, par exemple **Simon**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-224">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span> 

    <span data-ttu-id="5fc4c-225">c.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-225">c.</span></span> <span data-ttu-id="5fc4c-226">Dans la zone de texte **Nom d’utilisateur**, entrez **Britta Simon**, le nom d’utilisateur du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-226">In the **Username** textbox, type **Britta Simon**, the user name as in the Azure portal.</span></span>

    <span data-ttu-id="5fc4c-227">d.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-227">d.</span></span> <span data-ttu-id="5fc4c-228">Dans la zone **Password** , entrez un mot de passe pour Britta.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-228">In the **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="5fc4c-229">e.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-229">e.</span></span> <span data-ttu-id="5fc4c-230">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-230">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5fc4c-231">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5fc4c-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5fc4c-232">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Halogen Software.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5fc4c-234">**Pour attribuer Britta Simon à Halogen Software, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5fc4c-234">**To assign Britta Simon to Halogen Software, perform the following steps:**</span></span>

1. <span data-ttu-id="5fc4c-235">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5fc4c-237">Dans la liste des applications, sélectionnez **Halogen Software**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-237">In the applications list, select **Halogen Software**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="5fc4c-239">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5fc4c-241">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-241">Click **Add** button.</span></span> <span data-ttu-id="5fc4c-242">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5fc4c-244">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5fc4c-245">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5fc4c-246">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5fc4c-247">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5fc4c-247">Testing single sign-on</span></span>

<span data-ttu-id="5fc4c-248">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-248">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="5fc4c-249">Lorsque vous cliquez sur la vignette Halogen Software dans le volet d’accès, vous devez être connecté automatiquement à votre application Halogen Software.</span><span class="sxs-lookup"><span data-stu-id="5fc4c-249">When you click the Halogen Software tile in the Access Panel, you should get automatically signed-on to your Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5fc4c-250">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5fc4c-250">Additional resources</span></span>

* [<span data-ttu-id="5fc4c-251">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5fc4c-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5fc4c-252">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5fc4c-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
