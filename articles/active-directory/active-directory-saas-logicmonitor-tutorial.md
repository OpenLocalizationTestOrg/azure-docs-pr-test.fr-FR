---
title: "Didacticiel : Intégration d’Azure Active Directory avec LogicMonitor | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et LogicMonitor."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: e49960cac868f80af3e9165a9f75e49be87515f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="6aa4a-103">Didacticiel : Intégration d’Azure Active Directory à LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="6aa4a-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="6aa4a-104">Dans ce didacticiel, vous allez apprendre à intégrer LogicMonitor à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-104">In this tutorial, you learn how to integrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6aa4a-105">L’intégration de LogicMonitor à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="6aa4a-105">Integrating LogicMonitor with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6aa4a-106">Dans Azure AD, vous pouvez contrôler qui a accès à LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-106">You can control in Azure AD who has access to LogicMonitor</span></span>
- <span data-ttu-id="6aa4a-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à LogicMonitor (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-107">You can enable your users to automatically get signed-on to LogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6aa4a-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="6aa4a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6aa4a-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6aa4a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6aa4a-110">Prerequisites</span></span>

<span data-ttu-id="6aa4a-111">Pour configurer l’intégration d’Azure AD à LogicMonitor, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6aa4a-111">To configure Azure AD integration with LogicMonitor, you need the following items:</span></span>

- <span data-ttu-id="6aa4a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="6aa4a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6aa4a-113">Un abonnement LogicMonitor pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="6aa4a-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6aa4a-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6aa4a-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="6aa4a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6aa4a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6aa4a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6aa4a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="6aa4a-118">Scenario description</span></span>
<span data-ttu-id="6aa4a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6aa4a-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="6aa4a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6aa4a-121">Ajout de LogicMonitor à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="6aa4a-121">Adding LogicMonitor from the gallery</span></span>
2. <span data-ttu-id="6aa4a-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6aa4a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-the-gallery"></a><span data-ttu-id="6aa4a-123">Ajout de LogicMonitor à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="6aa4a-123">Adding LogicMonitor from the gallery</span></span>
<span data-ttu-id="6aa4a-124">Pour configurer l’intégration de LogicMonitor à Azure AD, vous devez ajouter LogicMonitor, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-124">To configure the integration of LogicMonitor into Azure AD, you need to add LogicMonitor from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6aa4a-125">**Pour ajouter LogicMonitor à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6aa4a-125">**To add LogicMonitor from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6aa4a-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6aa4a-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6aa4a-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="6aa4a-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="6aa4a-133">Dans la zone de recherche, entrez **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-133">In the search box, type **LogicMonitor**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="6aa4a-135">Dans le volet de résultats, sélectionnez **LogicMonitor**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-135">In the results panel, select **LogicMonitor**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6aa4a-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6aa4a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6aa4a-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LogicMonitor, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="6aa4a-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6aa4a-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur LogicMonitor équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LogicMonitor is to a user in Azure AD.</span></span> <span data-ttu-id="6aa4a-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur LogicMonitor associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-140">In other words, a link relationship between an Azure AD user and the related user in LogicMonitor needs to be established.</span></span>

<span data-ttu-id="6aa4a-141">Dans LogicMonitor, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-141">In LogicMonitor, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6aa4a-142">Pour configurer et tester l’authentification unique Azure AD avec LogicMonitor, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="6aa4a-142">To configure and test Azure AD single sign-on with LogicMonitor, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6aa4a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6aa4a-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6aa4a-145">**[Création d’un utilisateur de test LogicMonitor](#creating-a-logicmonitor-test-user)** pour avoir un équivalent de Britta Simon dans LogicMonitor lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - to have a counterpart of Britta Simon in LogicMonitor that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6aa4a-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6aa4a-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6aa4a-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6aa4a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6aa4a-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="6aa4a-150">**Pour configurer l’authentification unique Azure AD avec LogicMonitor, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6aa4a-150">**To configure Azure AD single sign-on with LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="6aa4a-151">Dans le portail Azure, dans la page d’intégration de l’application **LogicMonitor**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-151">In the Azure portal, on the **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="6aa4a-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="6aa4a-155">Dans la section **Domaine et URL LogicMonitor**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6aa4a-155">On the **LogicMonitor Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="6aa4a-157">a.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-157">a.</span></span> <span data-ttu-id="6aa4a-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="6aa4a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="6aa4a-159">b.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-159">b.</span></span> <span data-ttu-id="6aa4a-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="6aa4a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6aa4a-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-161">These values are not real.</span></span> <span data-ttu-id="6aa4a-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6aa4a-163">Pour obtenir ces valeurs, contactez [l’équipe du support client LogicMonitor](https://www.logicmonitor.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) to get these values.</span></span> 
 


4. <span data-ttu-id="6aa4a-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="6aa4a-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="6aa4a-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6aa4a-168">Connectez-vous au site d’entreprise **LogicMonitor** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-168">Log in to your **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="6aa4a-169">Dans le menu situé en haut, cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-169">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="6aa4a-170">![Paramètres](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="6aa4a-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="6aa4a-171">Dans la barre de navigation située à gauche, cliquez sur **Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="6aa4a-171">In the navigation bat on the left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="6aa4a-172">![Authentification unique](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="6aa4a-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="6aa4a-173">Dans la section **Single Sign-On SSO settings** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6aa4a-173">In the **Single Sign-on (SSO) settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="6aa4a-174">![Paramètres d’authentification unique](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="6aa4a-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="6aa4a-175">a.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-175">a.</span></span> <span data-ttu-id="6aa4a-176">Sélectionnez **Enable Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="6aa4a-177">b.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-177">b.</span></span> <span data-ttu-id="6aa4a-178">Pour **Default Role Assignment**, sélectionnez **readonly**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="6aa4a-179">c.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-179">c.</span></span> <span data-ttu-id="6aa4a-180">Ouvrez le fichier de métadonnées téléchargé dans le Bloc-notes, puis collez le contenu dans la zone de texte **Identity Provider Metadata** .</span><span class="sxs-lookup"><span data-stu-id="6aa4a-180">Open the downloaded metadata file in notepad, and then paste content of the file into the **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="6aa4a-181">d.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-181">d.</span></span> <span data-ttu-id="6aa4a-182">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="6aa4a-183">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6aa4a-184">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6aa4a-185">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6aa4a-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6aa4a-186">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6aa4a-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="6aa4a-187">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="6aa4a-189">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6aa4a-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6aa4a-190">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6aa4a-192">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6aa4a-194">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6aa4a-196">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6aa4a-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6aa4a-198">a.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-198">a.</span></span> <span data-ttu-id="6aa4a-199">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6aa4a-200">b.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-200">b.</span></span> <span data-ttu-id="6aa4a-201">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6aa4a-202">c.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-202">c.</span></span> <span data-ttu-id="6aa4a-203">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6aa4a-204">d.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-204">d.</span></span> <span data-ttu-id="6aa4a-205">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="6aa4a-206">Création d’un utilisateur de test de LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="6aa4a-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="6aa4a-207">Pour AAD les utilisateurs puissent se connecter, ils doivent être approvisionnés dans l’application LogicMonitorà l’aide de leurs noms d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-207">For AAD users to be able to sign in, they must be provisioned to the LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="6aa4a-208">**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6aa4a-208">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="6aa4a-209">Connectez-vous au site d’entreprise LogicMonitor en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-209">Log in to your LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="6aa4a-210">Dans le menu situé en haut, cliquez sur **Settings**, puis sur **Roles and Users**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-210">In the menu on the top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="6aa4a-211">![Rôles et utilisateurs](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Rôles et utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="6aa4a-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="6aa4a-212">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-212">Click **Add**.</span></span>

4. <span data-ttu-id="6aa4a-213">Dans la section **Add an account** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6aa4a-213">In the **Add an account** section, perform the following steps:</span></span>
   
   <span data-ttu-id="6aa4a-214">![Ajouter un compte](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Ajouter un compte")</span><span class="sxs-lookup"><span data-stu-id="6aa4a-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="6aa4a-215">a.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-215">a.</span></span> <span data-ttu-id="6aa4a-216">Entrez les valeurs appropriées dans les champs **Nom d’utilisateur**, **Adresse de messagerie**, **Mot de passe** et **Confirmer le mot de passe** pour l’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-216">Type the **Username**, **Email**, **Password**, and **Retype password** values of the Azure Active Directory user you want to provision into the related textboxes.</span></span>
   
   <span data-ttu-id="6aa4a-217">b.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-217">b.</span></span> <span data-ttu-id="6aa4a-218">Sélectionnez **Rôles**, **Afficher les autorisations** et **État**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-218">Select **Roles**, **View Permissions**, and the **Status**.</span></span>
   
   <span data-ttu-id="6aa4a-219">c.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-219">c.</span></span> <span data-ttu-id="6aa4a-220">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="6aa4a-221">Vous pouvez utiliser n’importe quel outil ou API de création de compte utilisateur, fourni par LogicMonitor, pour approvisionner des comptes utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6aa4a-222">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6aa4a-222">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6aa4a-223">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-223">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LogicMonitor.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="6aa4a-225">**Pour affecter Britta Simon à LogicMonitor, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6aa4a-225">**To assign Britta Simon to LogicMonitor, perform the following steps:**</span></span>

1. <span data-ttu-id="6aa4a-226">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-226">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="6aa4a-228">Dans la liste des applications, sélectionnez **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-228">In the applications list, select **LogicMonitor**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="6aa4a-230">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-230">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="6aa4a-232">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-232">Click **Add** button.</span></span> <span data-ttu-id="6aa4a-233">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="6aa4a-235">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-235">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6aa4a-236">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6aa4a-237">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6aa4a-238">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="6aa4a-238">Testing single sign-on</span></span>

<span data-ttu-id="6aa4a-239">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-239">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="6aa4a-240">Lorsque vous cliquez sur la vignette LogicMonitor dans le volet d’accès, vous devez être connecté automatiquement à votre application LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="6aa4a-240">When you click the LogicMonitor tile in the Access Panel, you should get automatically signed-on to your LogicMonitor application.</span></span>
<span data-ttu-id="6aa4a-241">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6aa4a-241">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6aa4a-242">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6aa4a-242">Additional resources</span></span>

* [<span data-ttu-id="6aa4a-243">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6aa4a-243">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6aa4a-244">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="6aa4a-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

