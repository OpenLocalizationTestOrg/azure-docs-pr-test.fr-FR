---
title: "Didacticiel : Intégration d’Azure Active Directory à MaxxPoint | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et MaxxPoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ba026e-96fc-4ae8-b135-0169da810e99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 8a7481b71df5ca407dbed5da3d3cc26991504c82
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-maxxpoint"></a><span data-ttu-id="d6c17-103">Didacticiel : Intégration d’Azure Active Directory à MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="d6c17-103">Tutorial: Azure Active Directory integration with MaxxPoint</span></span>

<span data-ttu-id="d6c17-104">Dans ce didacticiel, vous allez apprendre à intégrer MaxxPoint à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6c17-104">In this tutorial, you learn how to integrate MaxxPoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d6c17-105">L’intégration de MaxxPoint à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d6c17-105">Integrating MaxxPoint with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d6c17-106">Dans Azure AD, vous pouvez contrôler qui a accès à MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d6c17-106">You can control in Azure AD who has access to MaxxPoint</span></span>
- <span data-ttu-id="d6c17-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à MaxxPoint (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6c17-107">You can enable your users to automatically get signed-on to MaxxPoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d6c17-108">Vous pouvez gérer vos comptes depuis un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d6c17-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d6c17-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d6c17-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6c17-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d6c17-110">Prerequisites</span></span>

<span data-ttu-id="d6c17-111">Pour configurer l’intégration d’Azure AD à MaxxPoint, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d6c17-111">To configure Azure AD integration with MaxxPoint, you need the following items:</span></span>

- <span data-ttu-id="d6c17-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6c17-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d6c17-113">Un abonnement MaxxPoint pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d6c17-113">A MaxxPoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d6c17-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d6c17-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d6c17-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="d6c17-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d6c17-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d6c17-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d6c17-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6c17-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d6c17-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d6c17-118">Scenario description</span></span>
<span data-ttu-id="d6c17-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d6c17-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d6c17-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="d6c17-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6c17-121">Ajout de MaxxPoint à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d6c17-121">Adding MaxxPoint from the gallery</span></span>
2. <span data-ttu-id="d6c17-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6c17-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-maxxpoint-from-the-gallery"></a><span data-ttu-id="d6c17-123">Ajout de MaxxPoint à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="d6c17-123">Adding MaxxPoint from the gallery</span></span>
<span data-ttu-id="d6c17-124">Pour configurer l’intégration de MaxxPoint à Azure AD, vous devez ajouter MaxxPoint à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d6c17-124">To configure the integration of MaxxPoint into Azure AD, you need to add MaxxPoint from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d6c17-125">**Pour ajouter MaxxPoint à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d6c17-125">**To add MaxxPoint from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d6c17-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d6c17-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d6c17-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d6c17-131">Pour ajouter la nouvelle application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d6c17-131">Click **New application** button on the top of dialog to add new application.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d6c17-133">Dans la zone de recherche, tapez **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-133">In the search box, type **MaxxPoint**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_001.png)

5. <span data-ttu-id="d6c17-135">Dans le volet des résultats, sélectionnez **MaxxPoint**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="d6c17-135">In the results panel, select **MaxxPoint**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d6c17-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6c17-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d6c17-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec MaxxPoint avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d6c17-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d6c17-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur MaxxPoint équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6c17-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MaxxPoint is to a user in Azure AD.</span></span> <span data-ttu-id="d6c17-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur MaxxPoint associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="d6c17-140">In other words, a link relationship between an Azure AD user and the related user in MaxxPoint needs to be established.</span></span>

<span data-ttu-id="d6c17-141">Pour cela, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** dans MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d6c17-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in MaxxPoint.</span></span>

<span data-ttu-id="d6c17-142">Pour configurer et tester l’authentification unique Azure AD avec MaxxPoint, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="d6c17-142">To configure and test Azure AD single sign-on with MaxxPoint, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d6c17-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d6c17-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d6c17-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6c17-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6c17-145">**[Création d’un utilisateur de test MaxxPoint](#creating-a-maxxpoint-test-user)** pour avoir un équivalent de Britta Simon dans MaxxPoint lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="d6c17-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - to have a counterpart of Britta Simon in MaxxPoint that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d6c17-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6c17-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6c17-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="d6c17-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d6c17-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6c17-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d6c17-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d6c17-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MaxxPoint application.</span></span>

<span data-ttu-id="d6c17-150">**Pour configurer l’authentification unique Azure AD avec MaxxPoint, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d6c17-150">**To configure Azure AD single sign-on with MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="d6c17-151">Dans le portail Azure, sur la page d’intégration de l’application **MaxxPoint**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-151">In the Azure portal, on the **MaxxPoint** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d6c17-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d6c17-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_300.png)

3. <span data-ttu-id="d6c17-155">Dans la section **MaxxPoint Domain and URLs** (Domaines et URL MaxxPoint), si vous souhaitez configurer l’application en **IDP initiated mode** (Mode initié par IDP), vous n’avez aucune opération à effectuer.</span><span class="sxs-lookup"><span data-stu-id="d6c17-155">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, no need to perform any steps.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_02.png)
    
4. <span data-ttu-id="d6c17-157">Dans la section **MaxxPoint Domain and URLs** (Domaines et URL MaxxPoint), si vous souhaitez configurer l’application en **SP initiated mode** (Mode initié par SP), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d6c17-157">On the **MaxxPoint Domain and URLs** section, If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_03.png)

    <span data-ttu-id="d6c17-159">a.</span><span class="sxs-lookup"><span data-stu-id="d6c17-159">a.</span></span> <span data-ttu-id="d6c17-160">Cliquez sur l’option **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-160">Click **Show advanced URL settings** option</span></span>

    <span data-ttu-id="d6c17-161">b.</span><span class="sxs-lookup"><span data-stu-id="d6c17-161">b.</span></span> <span data-ttu-id="d6c17-162">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span><span class="sxs-lookup"><span data-stu-id="d6c17-162">In the **Sign On URL** textbox, type a URL using the following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d6c17-163">Notez qu’il ne s’agit pas de la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="d6c17-163">Please note that this is not the real value.</span></span> <span data-ttu-id="d6c17-164">Vous devez mettre à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="d6c17-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="d6c17-165">Appelez l’équipe MaxxPoint au **888-728-0950** pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="d6c17-165">Call MaxxPoint team on **888-728-0950** to get this value.</span></span>

5. <span data-ttu-id="d6c17-166">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d6c17-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_06.png) 

6. <span data-ttu-id="d6c17-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d6c17-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d6c17-170">Pour configurer SSO en fonction de votre application, appelez l’équipe d’assistance de MaxxPoint au **888-728-0950**. Elle vous expliquera comment procéder pour envoyer le fichier **Metadonnées XML** téléchargé.</span><span class="sxs-lookup"><span data-stu-id="d6c17-170">To get SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how to provide them the downloaded **Metadata XML** file.</span></span> 

> [!TIP]
> <span data-ttu-id="d6c17-171">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="d6c17-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d6c17-172">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée via la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="d6c17-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d6c17-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d6c17-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d6c17-174">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6c17-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="d6c17-175">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d6c17-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d6c17-177">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d6c17-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d6c17-178">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d6c17-180">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d6c17-180">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d6c17-182">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-182">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d6c17-184">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d6c17-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d6c17-186">a.</span><span class="sxs-lookup"><span data-stu-id="d6c17-186">a.</span></span> <span data-ttu-id="d6c17-187">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d6c17-188">b.</span><span class="sxs-lookup"><span data-stu-id="d6c17-188">b.</span></span> <span data-ttu-id="d6c17-189">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6c17-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d6c17-190">c.</span><span class="sxs-lookup"><span data-stu-id="d6c17-190">c.</span></span> <span data-ttu-id="d6c17-191">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d6c17-192">d.</span><span class="sxs-lookup"><span data-stu-id="d6c17-192">d.</span></span> <span data-ttu-id="d6c17-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-193">Click **Create**.</span></span> 

### <a name="creating-a-maxxpoint-test-user"></a><span data-ttu-id="d6c17-194">Création d’un utilisateur de test MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="d6c17-194">Creating a MaxxPoint test user</span></span>

<span data-ttu-id="d6c17-195">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d6c17-195">In this section, you create a user called Britta Simon in MaxxPoint.</span></span> <span data-ttu-id="d6c17-196">Contactez l’équipe d’assistance au **888-728-0950** pour ajouter des utilisateurs dans l’application MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d6c17-196">Please call MaxxPoint support team on **888-728-0950** to add the users in the MaxxPoint application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d6c17-197">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6c17-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d6c17-198">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d6c17-198">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to MaxxPoint.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d6c17-200">**Pour affecter Britta Simon à MaxxPoint, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d6c17-200">**To assign Britta Simon to MaxxPoint, perform the following steps:**</span></span>

1. <span data-ttu-id="d6c17-201">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d6c17-203">Dans la liste des applications, sélectionnez **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-203">In the applications list, select **MaxxPoint**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_50.png) 

3. <span data-ttu-id="d6c17-205">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d6c17-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-207">Click **Add** button.</span></span> <span data-ttu-id="d6c17-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d6c17-210">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d6c17-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d6c17-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d6c17-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d6c17-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d6c17-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d6c17-213">Testing single sign-on</span></span>

<span data-ttu-id="d6c17-214">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="d6c17-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d6c17-215">Lorsque vous cliquez sur la mosaïque MaxxPoint dans le volet d’accès, vous devez être connecté automatiquement à votre application MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d6c17-215">When you click the MaxxPoint tile in the Access Panel, you should get automatically signed-on to your MaxxPoint application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d6c17-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d6c17-216">Additional resources</span></span>

* [<span data-ttu-id="d6c17-217">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6c17-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6c17-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d6c17-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_203.png