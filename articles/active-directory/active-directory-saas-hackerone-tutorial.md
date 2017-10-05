---
title: "Didacticiel : Intégration d’Azure Active Directory avec HackerOne | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et HackerOne."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 657d8d4c98b7b133698a5cda0aa675da7f68c464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="2957f-103">Didacticiel : Intégration d’Azure Active Directory à HackerOne</span><span class="sxs-lookup"><span data-stu-id="2957f-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="2957f-104">Dans ce didacticiel, vous allez apprendre à intégrer HackerOne à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2957f-104">In this tutorial, you learn how to integrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2957f-105">L’intégration de HackerOne à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2957f-105">Integrating HackerOne with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2957f-106">Dans Azure AD, vous pouvez contrôler qui a accès à HackerOne.</span><span class="sxs-lookup"><span data-stu-id="2957f-106">You can control in Azure AD who has access to HackerOne</span></span>
- <span data-ttu-id="2957f-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à HackerOne (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2957f-107">You can enable your users to automatically get signed-on to HackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2957f-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="2957f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2957f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2957f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2957f-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="2957f-110">Prerequisites</span></span>

<span data-ttu-id="2957f-111">Pour configurer l’intégration d’Azure AD à HackerOne, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2957f-111">To configure Azure AD integration with HackerOne, you need the following items:</span></span>

- <span data-ttu-id="2957f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2957f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2957f-113">Un abonnement Hackerone pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2957f-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2957f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2957f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2957f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2957f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2957f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2957f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2957f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2957f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2957f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2957f-118">Scenario description</span></span>
<span data-ttu-id="2957f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2957f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2957f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="2957f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2957f-121">Ajout de HackerOne à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2957f-121">Adding HackerOne from the gallery</span></span>
2. <span data-ttu-id="2957f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2957f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-the-gallery"></a><span data-ttu-id="2957f-123">Ajout de HackerOne à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2957f-123">Adding HackerOne from the gallery</span></span>
<span data-ttu-id="2957f-124">Pour configurer l’intégration de HackerOne à Azure AD, vous devez ajouter HackerOne à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2957f-124">To configure the integration of HackerOne into Azure AD, you need to add HackerOne from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2957f-125">**Pour ajouter HackerOne à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2957f-125">**To add HackerOne from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2957f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2957f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2957f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2957f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2957f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2957f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2957f-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2957f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2957f-133">Dans la zone de recherche, tapez **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="2957f-133">In the search box, type **HackerOne**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="2957f-135">Dans le volet de résultats, sélectionnez **HackerOne**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="2957f-135">In the results panel, select **HackerOne**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2957f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2957f-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="2957f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec HackerOne avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2957f-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2957f-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur HackerOne équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2957f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HackerOne is to a user in Azure AD.</span></span> <span data-ttu-id="2957f-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur HackerOne associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="2957f-140">In other words, a link relationship between an Azure AD user and the related user in HackerOne needs to be established.</span></span>

<span data-ttu-id="2957f-141">Dans HackerOne, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="2957f-141">In HackerOne, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2957f-142">Pour configurer et tester l’authentification unique Azure AD avec HackerOne, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="2957f-142">To configure and test Azure AD single sign-on with HackerOne, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2957f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2957f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2957f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2957f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2957f-145">**[Création d’un utilisateur de test HackerOne](#creating-a-hackerone-test-user)** pour avoir un équivalent de Britta Simon dans HackerOne lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="2957f-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - to have a counterpart of Britta Simon in HackerOne that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2957f-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2957f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2957f-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="2957f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2957f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2957f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2957f-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application HackerOne.</span><span class="sxs-lookup"><span data-stu-id="2957f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="2957f-150">**Pour configurer l’authentification unique Azure AD avec HackerOne, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2957f-150">**To configure Azure AD single sign-on with HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="2957f-151">Dans le portail Azure, dans la page d’intégration de l’application **HackerOne**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2957f-151">In the Azure portal, on the **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="2957f-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2957f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="2957f-155">Dans la section **URL et identificateur d’authentification unique HackerOne**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2957f-155">On the **HackerOne Single sign-on URL and Identifier** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="2957f-157">a.</span><span class="sxs-lookup"><span data-stu-id="2957f-157">a.</span></span> <span data-ttu-id="2957f-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="2957f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="2957f-159">b.</span><span class="sxs-lookup"><span data-stu-id="2957f-159">b.</span></span> <span data-ttu-id="2957f-160">Dans la zone de texte **Identificateur**, entrez une URL telle que celle-ci : `https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="2957f-160">In the **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="2957f-161">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="2957f-161">This value is not real.</span></span> <span data-ttu-id="2957f-162">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="2957f-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="2957f-163">Contactez [l’équipe de support technique de HackerOne](mailto:support@hackerone.com) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="2957f-163">Contact [HackerOne support team](mailto:support@hackerone.com) to get this value.</span></span> 
 
4. <span data-ttu-id="2957f-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2957f-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="2957f-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="2957f-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2957f-168">Dans la section **Configuration de HackerOne**, cliquez sur **Configurer HackerOne** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="2957f-168">On the **HackerOne Configuration** section, click **Configure HackerOne** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2957f-169">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="2957f-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="2957f-171">Connectez-vous à votre locataire HackerOne en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2957f-171">Sign On to your HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="2957f-172">Dans le menu situé en haut, cliquez sur « **Settings** ».</span><span class="sxs-lookup"><span data-stu-id="2957f-172">In the menu on the top, click the "**Settings**."</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="2957f-174">Accédez à « **Authentication** » et cliquez sur « **Add SAML settings** ».</span><span class="sxs-lookup"><span data-stu-id="2957f-174">Navigate to "**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="2957f-176">Dans la boîte de dialogue **SAML Settings** (Paramètres SAML), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2957f-176">On the **SAML Settings** dialog, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="2957f-178">a.</span><span class="sxs-lookup"><span data-stu-id="2957f-178">a.</span></span> <span data-ttu-id="2957f-179">Dans la zone de texte **Email Domain** , entrez un domaine enregistré.</span><span class="sxs-lookup"><span data-stu-id="2957f-179">In the **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="2957f-180">b.</span><span class="sxs-lookup"><span data-stu-id="2957f-180">b.</span></span> <span data-ttu-id="2957f-181">Dans la zone de texte **Single Sign On URL**, collez la valeur de l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2957f-181">In  **Single Sign On URL** textboxes, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2957f-182">c.</span><span class="sxs-lookup"><span data-stu-id="2957f-182">c.</span></span> <span data-ttu-id="2957f-183">Ouvrez dans le Bloc-notes votre **Fichier de certificat** téléchargé à partir du portail Azure, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Certificat X509**.</span><span class="sxs-lookup"><span data-stu-id="2957f-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="2957f-184">d.</span><span class="sxs-lookup"><span data-stu-id="2957f-184">d.</span></span> <span data-ttu-id="2957f-185">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2957f-185">Click **Save**.</span></span>

11. <span data-ttu-id="2957f-186">Dans la boîte de dialogue Authentication Settings, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2957f-186">On the Authentication Settings dialog, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="2957f-188">a.</span><span class="sxs-lookup"><span data-stu-id="2957f-188">a.</span></span> <span data-ttu-id="2957f-189">Cliquez sur **Run test**.</span><span class="sxs-lookup"><span data-stu-id="2957f-189">Click **Run test**.</span></span>

    <span data-ttu-id="2957f-190">b.</span><span class="sxs-lookup"><span data-stu-id="2957f-190">b.</span></span> <span data-ttu-id="2957f-191">Si la valeur du champ **Status** est égale à **Last test status: created**, contactez l’[équipe de support technique HackerOne](mailto:support@hackerone.com) pour demander une révision de votre configuration.</span><span class="sxs-lookup"><span data-stu-id="2957f-191">If the value of the **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) to request a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="2957f-192">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="2957f-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2957f-193">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="2957f-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2957f-194">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2957f-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2957f-195">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2957f-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="2957f-196">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2957f-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="2957f-198">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2957f-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2957f-199">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2957f-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2957f-201">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2957f-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2957f-203">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2957f-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2957f-205">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2957f-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2957f-207">a.</span><span class="sxs-lookup"><span data-stu-id="2957f-207">a.</span></span> <span data-ttu-id="2957f-208">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2957f-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2957f-209">b.</span><span class="sxs-lookup"><span data-stu-id="2957f-209">b.</span></span> <span data-ttu-id="2957f-210">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2957f-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2957f-211">c.</span><span class="sxs-lookup"><span data-stu-id="2957f-211">c.</span></span> <span data-ttu-id="2957f-212">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2957f-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2957f-213">d.</span><span class="sxs-lookup"><span data-stu-id="2957f-213">d.</span></span> <span data-ttu-id="2957f-214">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2957f-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="2957f-215">Création d'un utilisateur de test HackerOne</span><span class="sxs-lookup"><span data-stu-id="2957f-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="2957f-216">Vous allez maintenant créer un utilisateur nommé Britta Simon dans HackerOne.</span><span class="sxs-lookup"><span data-stu-id="2957f-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="2957f-217">HackerOne prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="2957f-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="2957f-218">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="2957f-218">There is no action item for you in this section.</span></span> <span data-ttu-id="2957f-219">Lorsque vous accédez à HackerOne, un nouvel utilisateur est créé s'il n'existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="2957f-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="2957f-220">Si vous devez créer un utilisateur manuellement, contactez l’équipe du support technique Certify.</span><span class="sxs-lookup"><span data-stu-id="2957f-220">If you need to create a user manually, you need to contact the Certify support team.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2957f-221">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2957f-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2957f-222">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à HackerOne.</span><span class="sxs-lookup"><span data-stu-id="2957f-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HackerOne.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="2957f-224">**Pour affecter Britta Simon à HackerOne, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2957f-224">**To assign Britta Simon to HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="2957f-225">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2957f-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2957f-227">Dans la liste des applications, sélectionnez **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="2957f-227">In the applications list, select **HackerOne**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="2957f-229">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2957f-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="2957f-231">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2957f-231">Click **Add** button.</span></span> <span data-ttu-id="2957f-232">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2957f-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="2957f-234">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2957f-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2957f-235">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2957f-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2957f-236">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2957f-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2957f-237">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2957f-237">Testing single sign-on</span></span>

<span data-ttu-id="2957f-238">Pour terminer, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="2957f-238">Finally, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="2957f-239">Quand vous cliquez sur la vignette HackerOne dans le volet d’accès, vous devez être connecté automatiquement à votre application HackerOne.</span><span class="sxs-lookup"><span data-stu-id="2957f-239">When you click the HackerOne tile in the Access Panel, you should get automatically signed-on to your HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2957f-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2957f-240">Additional resources</span></span>

* [<span data-ttu-id="2957f-241">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2957f-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2957f-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2957f-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

