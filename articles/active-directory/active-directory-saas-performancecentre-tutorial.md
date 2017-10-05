---
title: "Didacticiel : Intégration d’Azure Active Directory à PerformanceCentre | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et PerformanceCentre."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 65288c32-f7e6-4eb3-a6dc-523c3d748d1c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e86adaf4bd9b4752f2aece8207a8a423ec5590a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-performancecentre"></a><span data-ttu-id="54bd4-103">Didacticiel : Intégration d’Azure Active Directory à PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="54bd4-103">Tutorial: Azure Active Directory integration with PerformanceCentre</span></span>

<span data-ttu-id="54bd4-104">Dans ce didacticiel, vous apprenez à intégrer PerformanceCentre à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="54bd4-104">In this tutorial, you learn how to integrate PerformanceCentre with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="54bd4-105">L’intégration de PerformanceCentre dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="54bd4-105">Integrating PerformanceCentre with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="54bd4-106">Dans Azure AD, vous pouvez contrôler qui a accès à PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="54bd4-106">You can control in Azure AD who has access to PerformanceCentre</span></span>
- <span data-ttu-id="54bd4-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à PerformanceCentre (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54bd4-107">You can enable your users to automatically get signed-on to PerformanceCentre (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="54bd4-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="54bd4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="54bd4-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="54bd4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54bd4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="54bd4-110">Prerequisites</span></span>

<span data-ttu-id="54bd4-111">Pour configurer l’intégration d’Azure AD avec PerformanceCentre, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="54bd4-111">To configure Azure AD integration with PerformanceCentre, you need the following items:</span></span>

- <span data-ttu-id="54bd4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="54bd4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="54bd4-113">Un abonnement PerformanceCentre pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="54bd4-113">A PerformanceCentre single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="54bd4-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="54bd4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="54bd4-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="54bd4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="54bd4-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="54bd4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="54bd4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="54bd4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="54bd4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="54bd4-118">Scenario description</span></span>
<span data-ttu-id="54bd4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="54bd4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="54bd4-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="54bd4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="54bd4-121">Ajout de PerformanceCentre à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="54bd4-121">Adding PerformanceCentre from the gallery</span></span>
2. <span data-ttu-id="54bd4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="54bd4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-performancecentre-from-the-gallery"></a><span data-ttu-id="54bd4-123">Ajout de PerformanceCentre à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="54bd4-123">Adding PerformanceCentre from the gallery</span></span>
<span data-ttu-id="54bd4-124">Pour configurer l’intégration de PerformanceCentre avec Azure AD, vous devez ajouter PerformanceCentre à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="54bd4-124">To configure the integration of PerformanceCentre into Azure AD, you need to add PerformanceCentre from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="54bd4-125">**Pour ajouter PerformanceCentre à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="54bd4-125">**To add PerformanceCentre from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="54bd4-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="54bd4-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="54bd4-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="54bd4-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="54bd4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="54bd4-133">Dans la zone de recherche, entrez **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-133">In the search box, type **PerformanceCentre**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_search.png)

5. <span data-ttu-id="54bd4-135">Dans le volet de résultats, sélectionnez **PerformanceCentre**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="54bd4-135">In the results panel, select **PerformanceCentre**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="54bd4-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="54bd4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="54bd4-138">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec PerformanceCentre au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="54bd4-138">In this section, you configure and test Azure AD single sign-on with PerformanceCentre based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="54bd4-139">Pour que l’authentification unique fonctionne, Azure AD a besoin de savoir qui est l’utilisateur PerformanceCentre équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54bd4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PerformanceCentre is to a user in Azure AD.</span></span> <span data-ttu-id="54bd4-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur PerformanceCentre associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="54bd4-140">In other words, a link relationship between an Azure AD user and the related user in PerformanceCentre needs to be established.</span></span>

<span data-ttu-id="54bd4-141">Dans PerformanceCentre, affectez la valeur du **nom d’utilisateur** indiquée dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="54bd4-141">In PerformanceCentre, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="54bd4-142">Pour configurer et tester l’authentification unique Azure AD avec PerformanceCentre, vous avez besoin de suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="54bd4-142">To configure and test Azure AD single sign-on with PerformanceCentre, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="54bd4-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="54bd4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="54bd4-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54bd4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="54bd4-145">**[Création d’un utilisateur de test PerformanceCentre](#creating-a-performancecentre-test-user)** pour avoir dans PerformanceCentre un équivalent de Britta Simon lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="54bd4-145">**[Creating a PerformanceCentre test user](#creating-a-performancecentre-test-user)** - to have a counterpart of Britta Simon in PerformanceCentre that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="54bd4-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54bd4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="54bd4-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="54bd4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="54bd4-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="54bd4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="54bd4-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="54bd4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PerformanceCentre application.</span></span>

<span data-ttu-id="54bd4-150">**Pour configurer l’authentification unique Azure AD avec PerformanceCentre, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="54bd4-150">**To configure Azure AD single sign-on with PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="54bd4-151">Dans le portail Azure, sur la page d’intégration de l’application **PerformanceCentre** , cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-151">In the Azure portal, on the **PerformanceCentre** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="54bd4-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="54bd4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_samlbase.png)

3. <span data-ttu-id="54bd4-155">Dans la section **Domaine et URL PerformanceCentre**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="54bd4-155">On the **PerformanceCentre Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_url.png)

    <span data-ttu-id="54bd4-157">a.</span><span class="sxs-lookup"><span data-stu-id="54bd4-157">a.</span></span> <span data-ttu-id="54bd4-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `http://companyname.performancecentre.com/saml/SSO`</span><span class="sxs-lookup"><span data-stu-id="54bd4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://companyname.performancecentre.com/saml/SSO`</span></span>

    <span data-ttu-id="54bd4-159">b.</span><span class="sxs-lookup"><span data-stu-id="54bd4-159">b.</span></span> <span data-ttu-id="54bd4-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `http://companyname.performancecentre.com`</span><span class="sxs-lookup"><span data-stu-id="54bd4-160">In the **Identifier** textbox, type a URL using the following pattern: `http://companyname.performancecentre.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="54bd4-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="54bd4-161">These values are not real.</span></span> <span data-ttu-id="54bd4-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="54bd4-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="54bd4-163">Pour obtenir ces valeurs, contactez l’[équipe du support technique de PerformanceCentre](https://www.performancecentre.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="54bd4-163">Contact [PerformanceCentre Client support team](https://www.performancecentre.com/contact-us/) to get these values.</span></span> 

4. <span data-ttu-id="54bd4-164">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="54bd4-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_certificate.png) 

5. <span data-ttu-id="54bd4-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="54bd4-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-performancecentre-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="54bd4-168">Dans la section **Configuration PerformanceCentre**, cliquez sur **Configurer PerformanceCentre** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-168">On the **PerformanceCentre Configuration** section, click **Configure PerformanceCentre** to open **Configure sign-on** window.</span></span> <span data-ttu-id="54bd4-169">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_configure.png) 

7. <span data-ttu-id="54bd4-171">Connectez-vous à votre site d’entreprise **PerformanceCentre** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="54bd4-171">Sign-on to your **PerformanceCentre** company site as administrator.</span></span>

8. <span data-ttu-id="54bd4-172">Dans l’onglet sur le côté gauche, cliquez sur **Configure**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-172">In the tab on the left side, click **Configure**.</span></span>
   
    ![Authentification unique Azure AD][10]

9. <span data-ttu-id="54bd4-174">Dans l’onglet sur le côté gauche, cliquez sur **Miscellaneous**, puis cliquez sur **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-174">In the tab on the left side, click **Miscellaneous**, and then click **Single Sign On**.</span></span>
   
    ![Authentification unique Azure AD][11]

10. <span data-ttu-id="54bd4-176">Pour **Protocol**, sélectionnez **SAML**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-176">As **Protocol**, select **SAML**.</span></span>
   
    ![Authentification unique Azure AD][12]

11. <span data-ttu-id="54bd4-178">Ouvrez votre fichier de métadonnées téléchargé dans le Bloc-notes, copiez son contenu, collez-le dans la zone de texte **Identity Provider Metadata**, puis cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-178">Open your downloaded metadata file in notepad, copy the content, paste it into the **Identity Provider Metadata** textbox, and then click **Save**.</span></span>
   
    ![Authentification unique Azure AD][13]

12. <span data-ttu-id="54bd4-180">Vérifiez que les valeurs **Entity Base URL** et **Entity ID URL** sont correctes.</span><span class="sxs-lookup"><span data-stu-id="54bd4-180">Verify that the values for the **Entity Base URL** and **Entity ID URL** are correct.</span></span>
    
     ![Authentification unique Azure AD][14]

> [!TIP]
> <span data-ttu-id="54bd4-182">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="54bd4-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="54bd4-183">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="54bd4-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="54bd4-184">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="54bd4-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="54bd4-185">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="54bd4-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="54bd4-186">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="54bd4-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="54bd4-188">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="54bd4-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="54bd4-189">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="54bd4-191">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="54bd4-193">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="54bd4-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="54bd4-195">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="54bd4-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-performancecentre-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="54bd4-197">a.</span><span class="sxs-lookup"><span data-stu-id="54bd4-197">a.</span></span> <span data-ttu-id="54bd4-198">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="54bd4-199">b.</span><span class="sxs-lookup"><span data-stu-id="54bd4-199">b.</span></span> <span data-ttu-id="54bd4-200">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="54bd4-200">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="54bd4-201">c.</span><span class="sxs-lookup"><span data-stu-id="54bd4-201">c.</span></span> <span data-ttu-id="54bd4-202">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="54bd4-203">d.</span><span class="sxs-lookup"><span data-stu-id="54bd4-203">d.</span></span> <span data-ttu-id="54bd4-204">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-204">Click **Create**.</span></span>
 
### <a name="creating-a-performancecentre-test-user"></a><span data-ttu-id="54bd4-205">Création d’un utilisateur de test PerformanceCentre</span><span class="sxs-lookup"><span data-stu-id="54bd4-205">Creating a PerformanceCentre test user</span></span>

<span data-ttu-id="54bd4-206">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="54bd4-206">The objective of this section is to create a user called Britta Simon in PerformanceCentre.</span></span>

<span data-ttu-id="54bd4-207">**Pour créer un utilisateur appelé Britta Simon dans PerformanceCentre, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="54bd4-207">**To create a user called Britta Simon in PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="54bd4-208">Connectez-vous à votre site d’entreprise PerformanceCentre en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="54bd4-208">Sign on to your PerformanceCentre company site as administrator.</span></span>

2. <span data-ttu-id="54bd4-209">Dans le menu de gauche, cliquez sur **Interrelate**, puis cliquez sur **Create Participant**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-209">In the menu on the left, click **Interrelate**, and then click **Create Participant**.</span></span>
   
    ![Create User][400]

3. <span data-ttu-id="54bd4-211">Dans la boîte de dialogue **Interrelate - Create Participant** , effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="54bd4-211">On the **Interrelate - Create Participant** dialog, perform the following steps:</span></span>
   
    ![Create User][401]
    
    <span data-ttu-id="54bd4-213">a.</span><span class="sxs-lookup"><span data-stu-id="54bd4-213">a.</span></span> <span data-ttu-id="54bd4-214">Entrez les attributs requis pour Britta Simon dans les zones de texte correspondantes.</span><span class="sxs-lookup"><span data-stu-id="54bd4-214">Type the required attributes for Britta Simon into related textboxes.</span></span>
    
    >[!IMPORTANT]
    ><span data-ttu-id="54bd4-215">L’attribut de nom d’utilisateur de Britta dans PerformanceCentre doit être le même que le nom d’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="54bd4-215">Britta's User Name attribute in PerformanceCentre must be the same as the User Name in Azure AD.</span></span>
    
    <span data-ttu-id="54bd4-216">b.</span><span class="sxs-lookup"><span data-stu-id="54bd4-216">b.</span></span> <span data-ttu-id="54bd4-217">Sélectionnez **Client Administrator** pour **Choose Role**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-217">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="54bd4-218">c.</span><span class="sxs-lookup"><span data-stu-id="54bd4-218">c.</span></span> <span data-ttu-id="54bd4-219">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-219">Click **Save**.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="54bd4-220">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="54bd4-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="54bd4-221">Dans cette section, vous autorisez Britta Simon à utiliser l’authentification unique Azure en accordant l’accès à PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="54bd4-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PerformanceCentre.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="54bd4-223">**Pour attribuer Britta Simon à PerformanceCentre, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="54bd4-223">**To assign Britta Simon to PerformanceCentre, perform the following steps:**</span></span>

1. <span data-ttu-id="54bd4-224">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="54bd4-226">Dans la liste des applications, sélectionnez **PerformanceCentre**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-226">In the applications list, select **PerformanceCentre**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_app.png) 

3. <span data-ttu-id="54bd4-228">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="54bd4-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-230">Click **Add** button.</span></span> <span data-ttu-id="54bd4-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="54bd4-233">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="54bd4-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="54bd4-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="54bd4-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="54bd4-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="54bd4-236">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="54bd4-236">Testing single sign-on</span></span>

<span data-ttu-id="54bd4-237">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="54bd4-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="54bd4-238">Lorsque vous cliquez sur la vignette PerformanceCentre dans le volet d’accès, vous devez être connecté automatiquement à votre application PerformanceCentre.</span><span class="sxs-lookup"><span data-stu-id="54bd4-238">When you click the PerformanceCentre tile in the Access Panel, you should get automatically signed-on to your PerformanceCentre application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="54bd4-239">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="54bd4-239">Additional resources</span></span>

* [<span data-ttu-id="54bd4-240">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54bd4-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="54bd4-241">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="54bd4-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_04.png
[10]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_06.png
[11]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_07.png
[12]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_08.png
[13]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_09.png
[14]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_10.png

[100]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_11.png
[401]: ./media/active-directory-saas-performancecentre-tutorial/tutorial_performancecentre_12.png

