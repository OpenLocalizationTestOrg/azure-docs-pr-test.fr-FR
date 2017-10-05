---
title: "Didacticiel : Intégration d’Azure Active Directory à Cerner Central | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Cerner Central."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 77b5fb94cdfa5722081198aabc59fbf86229c2b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="7b612-103">Didacticiel : Intégration d’Azure Active Directory à Cerner Central</span><span class="sxs-lookup"><span data-stu-id="7b612-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="7b612-104">Dans ce didacticiel, vous allez apprendre à intégrer Cerner Central à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b612-104">In this tutorial, you learn how to integrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b612-105">L’intégration de Cerner Central à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="7b612-105">Integrating Cerner Central with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7b612-106">Dans Azure AD, vous pouvez contrôler qui a accès à Cerner Central</span><span class="sxs-lookup"><span data-stu-id="7b612-106">You can control in Azure AD who has access to Cerner Central</span></span>
- <span data-ttu-id="7b612-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Cerner Central (via l’authentification unique) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b612-107">You can enable your users to automatically get signed-on to Cerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7b612-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="7b612-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7b612-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7b612-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b612-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="7b612-110">Prerequisites</span></span>

<span data-ttu-id="7b612-111">Pour configurer l’intégration d’Azure AD à Cerner Central, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7b612-111">To configure Azure AD integration with Cerner Central, you need the following items:</span></span>

- <span data-ttu-id="7b612-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b612-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b612-113">Un compte du système Central Cerner approuvé</span><span class="sxs-lookup"><span data-stu-id="7b612-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="7b612-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="7b612-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b612-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7b612-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b612-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7b612-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b612-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b612-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b612-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="7b612-118">Scenario description</span></span>
<span data-ttu-id="7b612-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="7b612-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b612-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="7b612-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b612-121">Ajout de Cerner Central à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="7b612-121">Adding Cerner Central from the gallery</span></span>
2. <span data-ttu-id="7b612-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b612-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-the-gallery"></a><span data-ttu-id="7b612-123">Ajout de Cerner Central à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="7b612-123">Adding Cerner Central from the gallery</span></span>
<span data-ttu-id="7b612-124">Pour configurer l’intégration de Cerner Central à Azure AD, vous devez ajouter Cerner Central à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="7b612-124">To configure the integration of Cerner Central into Azure AD, you need to add Cerner Central from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7b612-125">**Pour ajouter Cerner Central à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="7b612-125">**To add Cerner Central from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7b612-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7b612-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7b612-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="7b612-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7b612-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7b612-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="7b612-131">Pour ajouter une nouvelle application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7b612-131">To add new application, click **New application** button on top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="7b612-133">Dans la zone de recherche, tapez **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="7b612-133">In the search box, type **Cerner Central**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="7b612-135">Dans le volet de résultats, sélectionnez **Cerner Central**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="7b612-135">In the results panel, select **Cerner Central**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7b612-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b612-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7b612-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Cerner Central pour un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="7b612-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7b612-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Cerner Central équivalent à un utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b612-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cerner Central is to a user in Azure AD.</span></span> <span data-ttu-id="7b612-140">En d’autres termes, une relation doit être établie entre un utilisateur Azure AD et l’utilisateur associé dans Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="7b612-140">In other words, a link relationship between an Azure AD user and the related user in Cerner Central needs to be established.</span></span>

<span data-ttu-id="7b612-141">Pour configurer et tester l’authentification unique Azure AD avec Cerner Central, vous devez effectuer les actions essentielles suivantes :</span><span class="sxs-lookup"><span data-stu-id="7b612-141">To configure and test Azure AD single sign-on with Cerner Central, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7b612-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="7b612-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7b612-143">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b612-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b612-144">**[Création d’un utilisateur de test Cerner Central](#creating-a-cerner-central-test-user)** pour avoir un équivalent de Britta Simon dans Cerner Central lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7b612-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - to have a counterpart of Britta Simon in Cerner Central that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="7b612-145">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b612-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b612-146">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="7b612-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7b612-147">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b612-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7b612-148">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="7b612-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="7b612-149">**Pour configurer l’authentification unique Azure AD avec Cerner Central, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="7b612-149">**To configure Azure AD single sign-on with Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="7b612-150">Dans le Portail Azure, sur la page d’intégration de l’application **Cerner Central**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="7b612-150">In the Azure portal, on the **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="7b612-152">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="7b612-152">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="7b612-154">Dans la section **Domaine et URL Cerner Central**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="7b612-154">On the **Cerner Central Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="7b612-156">a.</span><span class="sxs-lookup"><span data-stu-id="7b612-156">a.</span></span> <span data-ttu-id="7b612-157">Dans la zone de texte **Identificateur**, tapez la valeur au format suivant :</span><span class="sxs-lookup"><span data-stu-id="7b612-157">In the **Identifier** textbox, type the value using the following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="7b612-158">b.</span><span class="sxs-lookup"><span data-stu-id="7b612-158">b.</span></span> <span data-ttu-id="7b612-159">Dans la zone de texte **URL de réponse** , tapez une URL en respectant les formats suivants :</span><span class="sxs-lookup"><span data-stu-id="7b612-159">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="7b612-160">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="7b612-160">These values are not the real.</span></span> <span data-ttu-id="7b612-161">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="7b612-161">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="7b612-162">Pour obtenir ces valeurs, contactez l’[équipe de support technique Cerner Central](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="7b612-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) to get these values.</span></span>
 
4. <span data-ttu-id="7b612-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="7b612-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="7b612-165">Pour générer l’URL des **métadonnées**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="7b612-165">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="7b612-166">a.</span><span class="sxs-lookup"><span data-stu-id="7b612-166">a.</span></span> <span data-ttu-id="7b612-167">Cliquez sur **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="7b612-167">Click **App registrations**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="7b612-169">b.</span><span class="sxs-lookup"><span data-stu-id="7b612-169">b.</span></span> <span data-ttu-id="7b612-170">Cliquez sur **Points de terminaison** pour ouvrir la boîte de dialogue **Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="7b612-170">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="7b612-172">c.</span><span class="sxs-lookup"><span data-stu-id="7b612-172">c.</span></span> <span data-ttu-id="7b612-173">Cliquez sur le bouton Copier pour copier l’URL du document de métadonnées de fédération (**FEDERATION METADATA DOCUMENT**), puis collez-la dans le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="7b612-173">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="7b612-175">d.</span><span class="sxs-lookup"><span data-stu-id="7b612-175">d.</span></span> <span data-ttu-id="7b612-176">Accédez maintenant à la page de propriétés de **Cerner Central**, puis copiez l’**ID d’application** à l’aide du bouton **Copier** et collez-le dans le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="7b612-176">Now go to the property page of **Cerner Central** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="7b612-178">e.</span><span class="sxs-lookup"><span data-stu-id="7b612-178">e.</span></span> <span data-ttu-id="7b612-179">Générez l’**URL des métadonnées** en utilisant le format suivant : `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="7b612-179">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="7b612-180">Pour configurer l’authentification unique côté **Cerner Central**, vous devez envoyer l’**URL des métadonnées** au [support technique Cerner Central](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="7b612-180">To configure single sign-on on **Cerner Central** side, you need to send the **Metadata URL** to [Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="7b612-181">Il configure l’authentification unique (SSO) côté application pour terminer l’intégration.</span><span class="sxs-lookup"><span data-stu-id="7b612-181">They configure the SSO on application side to complete the integration.</span></span>

> [!TIP]
> <span data-ttu-id="7b612-182">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="7b612-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7b612-183">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="7b612-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7b612-184">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7b612-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7b612-185">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b612-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="7b612-186">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7b612-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span> 

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="7b612-188">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="7b612-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7b612-189">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7b612-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7b612-191">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="7b612-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7b612-193">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7b612-193">To open the **User** dialog, click **Add**.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7b612-195">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7b612-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7b612-197">a.</span><span class="sxs-lookup"><span data-stu-id="7b612-197">a.</span></span> <span data-ttu-id="7b612-198">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7b612-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b612-199">b.</span><span class="sxs-lookup"><span data-stu-id="7b612-199">b.</span></span> <span data-ttu-id="7b612-200">Dans la zone de texte **Nom d’utilisateur** , tapez l’**adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7b612-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="7b612-201">c.</span><span class="sxs-lookup"><span data-stu-id="7b612-201">c.</span></span> <span data-ttu-id="7b612-202">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7b612-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7b612-203">d.</span><span class="sxs-lookup"><span data-stu-id="7b612-203">d.</span></span> <span data-ttu-id="7b612-204">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b612-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="7b612-205">Création d’un utilisateur de test Cerner Central</span><span class="sxs-lookup"><span data-stu-id="7b612-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="7b612-206">L’application **Cerner Central** permet l’authentification à partir de n’importe quel fournisseur d’identité fédérée.</span><span class="sxs-lookup"><span data-stu-id="7b612-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="7b612-207">Si un utilisateur peut se connecter à la page d’accueil de l’application, il est fédéré et n’a besoin d’aucun approvisionnement manuel.</span><span class="sxs-lookup"><span data-stu-id="7b612-207">If a user is able to log in to the application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7b612-208">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b612-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7b612-209">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en accordant l’accès à Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="7b612-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cerner Central.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="7b612-211">**Pour affecter Britta Simon à Cerner Central, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="7b612-211">**To assign Britta Simon to Cerner Central, perform the following steps:**</span></span>

1. <span data-ttu-id="7b612-212">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="7b612-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="7b612-214">Dans la liste des applications, sélectionnez **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="7b612-214">In the applications list, select **Cerner Central**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="7b612-216">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7b612-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="7b612-218">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7b612-218">Click **Add** button.</span></span> <span data-ttu-id="7b612-219">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7b612-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="7b612-221">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7b612-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7b612-222">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7b612-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b612-223">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="7b612-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7b612-224">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="7b612-224">Testing single sign-on</span></span>

<span data-ttu-id="7b612-225">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="7b612-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7b612-226">Quand vous cliquez sur la mosaïque Cerner Central dans le volet d’accès, vous devez être automatiquement connecté à votre application Cerner Central.</span><span class="sxs-lookup"><span data-stu-id="7b612-226">When you click the Cerner Central tile in the Access Panel, you should get automatically signed-on to your Cerner Central application.</span></span> <span data-ttu-id="7b612-227">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7b612-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7b612-228">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7b612-228">Additional resources</span></span>

* [<span data-ttu-id="7b612-229">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b612-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b612-230">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="7b612-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

