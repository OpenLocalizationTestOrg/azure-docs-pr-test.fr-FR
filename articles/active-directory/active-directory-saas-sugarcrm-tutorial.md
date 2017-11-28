---
title: "Didacticiel : Intégration d’Azure Active Directory avec Sugar CRM | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Sugar CRM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: c27aef24e859522b8001ecb747906abdca14d87a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="3cead-103">Didacticiel : Intégration d’Azure AD avec Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="3cead-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="3cead-104">Dans ce didacticiel, vous allez apprendre à intégrer Sugar CRM avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3cead-104">In this tutorial, you learn how to integrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3cead-105">L’intégration de Sugar CRM dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="3cead-105">Integrating Sugar CRM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3cead-106">Dans Azure AD, vous pouvez contrôler qui a accès à Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="3cead-106">You can control in Azure AD who has access to Sugar CRM</span></span>
- <span data-ttu-id="3cead-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Sugar CRM (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cead-107">You can enable your users to automatically get signed-on to Sugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3cead-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="3cead-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3cead-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3cead-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cead-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3cead-110">Prerequisites</span></span>

<span data-ttu-id="3cead-111">Pour configurer l’intégration d’Azure AD à Sugar CRM, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3cead-111">To configure Azure AD integration with Sugar CRM, you need the following items:</span></span>

- <span data-ttu-id="3cead-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cead-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3cead-113">Un abonnement Sugar CRM pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="3cead-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3cead-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="3cead-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3cead-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3cead-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3cead-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3cead-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3cead-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3cead-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3cead-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="3cead-118">Scenario description</span></span>
<span data-ttu-id="3cead-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="3cead-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3cead-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="3cead-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3cead-121">Ajout de Sugar CRM à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="3cead-121">Adding Sugar CRM from the gallery</span></span>
2. <span data-ttu-id="3cead-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cead-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-the-gallery"></a><span data-ttu-id="3cead-123">Ajout de Sugar CRM à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="3cead-123">Adding Sugar CRM from the gallery</span></span>
<span data-ttu-id="3cead-124">Pour configurer l’intégration de Sugar CRM à Azure AD, vous devez ajouter Sugar CRM à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="3cead-124">To configure the integration of Sugar CRM into Azure AD, you need to add Sugar CRM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3cead-125">**Pour ajouter Sugar CRM à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3cead-125">**To add Sugar CRM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3cead-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3cead-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3cead-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="3cead-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3cead-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3cead-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="3cead-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3cead-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="3cead-133">Dans la zone de recherche, entrez **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="3cead-133">In the search box, type **Sugar CRM**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. <span data-ttu-id="3cead-135">Dans le volet de résultats, sélectionnez **Sugar CRM**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="3cead-135">In the results panel, select **Sugar CRM**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3cead-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cead-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3cead-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Sugar CRM avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="3cead-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3cead-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Sugar CRM correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cead-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sugar CRM is to a user in Azure AD.</span></span> <span data-ttu-id="3cead-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Sugar CRM associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="3cead-140">In other words, a link relationship between an Azure AD user and the related user in Sugar CRM needs to be established.</span></span>

<span data-ttu-id="3cead-141">Dans Sugar CRM, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="3cead-141">In Sugar CRM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3cead-142">Pour configurer et tester l’authentification unique Azure AD avec Sugar CRM, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="3cead-142">To configure and test Azure AD single sign-on with Sugar CRM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3cead-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3cead-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3cead-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cead-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3cead-145">**[Création d’un utilisateur de test Sugar CRM](#creating-a-sugar-crm-test-user)** pour avoir un équivalent de Britta Simon dans Sugar CRM, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="3cead-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - to have a counterpart of Britta Simon in Sugar CRM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3cead-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3cead-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3cead-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="3cead-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3cead-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cead-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3cead-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="3cead-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="3cead-150">**Pour configurer l’authentification unique Azure AD avec Sugar CRM, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3cead-150">**To configure Azure AD single sign-on with Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="3cead-151">Dans le portail Azure, sur la page d’intégration de l’application **Sugar CRM**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="3cead-151">In the Azure portal, on the **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="3cead-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3cead-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. <span data-ttu-id="3cead-155">Dans la section **Domaine et URL Sugar CRM**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3cead-155">On the **Sugar CRM Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="3cead-157">Dans la zone de texte **URL de connexion**, saisissez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="3cead-157">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="3cead-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="3cead-158">The value is not real.</span></span> <span data-ttu-id="3cead-159">Mettez à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="3cead-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="3cead-160">Pour obtenir cette valeur, contactez l’[équipe du support technique Sugar CRM](https://support.sugarcrm.com/).</span><span class="sxs-lookup"><span data-stu-id="3cead-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="3cead-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3cead-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. <span data-ttu-id="3cead-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="3cead-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3cead-165">Dans la section **Configuration de Sugar CRM**, cliquez sur **Configurer Sugar CRM** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="3cead-165">On the **Sugar CRM Configuration** section, click **Configure Sugar CRM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3cead-166">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="3cead-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. <span data-ttu-id="3cead-168">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Sugar CRM en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="3cead-168">In a different web browser window, log in to your Sugar CRM company site as an administrator.</span></span>

8. <span data-ttu-id="3cead-169">Accédez à **Admin**.</span><span class="sxs-lookup"><span data-stu-id="3cead-169">Go to **Admin**.</span></span>
   
    <span data-ttu-id="3cead-170">![Administrateur](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="3cead-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

9. <span data-ttu-id="3cead-171">Dans la section **Administration**, cliquez sur **Password Management (Gestion des mots de passe)**.</span><span class="sxs-lookup"><span data-stu-id="3cead-171">In the **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="3cead-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="3cead-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span></span>

10. <span data-ttu-id="3cead-173">Sélectionnez **Enable SAML Authentication**.</span><span class="sxs-lookup"><span data-stu-id="3cead-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="3cead-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="3cead-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span></span>

11. <span data-ttu-id="3cead-175">Dans la section **SAML Authentication** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3cead-175">In the **SAML Authentication** section, perform the following steps:</span></span>
   
    <span data-ttu-id="3cead-176">![Authentification SAML](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "Authentification SAML")</span><span class="sxs-lookup"><span data-stu-id="3cead-176">![SAML Authentication](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="3cead-177">a.</span><span class="sxs-lookup"><span data-stu-id="3cead-177">a.</span></span> <span data-ttu-id="3cead-178">Dans la zone de texte **URL de connexion**, collez la valeur de l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3cead-178">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="3cead-179">b.</span><span class="sxs-lookup"><span data-stu-id="3cead-179">b.</span></span> <span data-ttu-id="3cead-180">Dans la zone de texte **URL de déconnexion unique**, collez la valeur **URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3cead-180">In the **SLO URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="3cead-181">c.</span><span class="sxs-lookup"><span data-stu-id="3cead-181">c.</span></span> <span data-ttu-id="3cead-182">Ouvrez votre certificat codé en base 64 dans le bloc-notes, copiez son contenu dans le Presse-papiers et collez-le dans la zone de texte **X.509 Certificate** .</span><span class="sxs-lookup"><span data-stu-id="3cead-182">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="3cead-183">d.</span><span class="sxs-lookup"><span data-stu-id="3cead-183">d.</span></span> <span data-ttu-id="3cead-184">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="3cead-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3cead-185">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="3cead-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3cead-186">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="3cead-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3cead-187">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3cead-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3cead-188">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cead-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="3cead-189">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3cead-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="3cead-191">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3cead-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3cead-192">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3cead-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3cead-194">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="3cead-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3cead-196">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3cead-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3cead-198">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3cead-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3cead-200">a.</span><span class="sxs-lookup"><span data-stu-id="3cead-200">a.</span></span> <span data-ttu-id="3cead-201">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3cead-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3cead-202">b.</span><span class="sxs-lookup"><span data-stu-id="3cead-202">b.</span></span> <span data-ttu-id="3cead-203">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3cead-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3cead-204">c.</span><span class="sxs-lookup"><span data-stu-id="3cead-204">c.</span></span> <span data-ttu-id="3cead-205">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="3cead-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3cead-206">d.</span><span class="sxs-lookup"><span data-stu-id="3cead-206">d.</span></span> <span data-ttu-id="3cead-207">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3cead-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="3cead-208">Création d’un utilisateur de test Sugar CRM</span><span class="sxs-lookup"><span data-stu-id="3cead-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="3cead-209">Pour se connecter à Sugar CRM, les utilisateurs d’Azure AD doivent être approvisionnés dans Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="3cead-209">In order to enable Azure AD users to log in to Sugar CRM, they must be provisioned to Sugar CRM.</span></span>

<span data-ttu-id="3cead-210">Dans le cas de Sugar CRM, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="3cead-210">In the case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="3cead-211">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3cead-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="3cead-212">Connectez-vous à votre site d’entreprise **Sugar CRM** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="3cead-212">Log in to your **Sugar CRM** company site as administrator.</span></span>

2. <span data-ttu-id="3cead-213">Accédez à **Admin**.</span><span class="sxs-lookup"><span data-stu-id="3cead-213">Go to **Admin**.</span></span>
   
    <span data-ttu-id="3cead-214">![Administrateur](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="3cead-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

3. <span data-ttu-id="3cead-215">Dans la section **Administration**, cliquez sur **User Management (Gestion des utilisateurs)**.</span><span class="sxs-lookup"><span data-stu-id="3cead-215">In the **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="3cead-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="3cead-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span></span>

4. <span data-ttu-id="3cead-217">Accédez à **Users (Utilisateurs) \> Create New User (Créer un utilisateur)**.</span><span class="sxs-lookup"><span data-stu-id="3cead-217">Go to **Users \> Create New User**.</span></span>
   
    <span data-ttu-id="3cead-218">![Créer un nouvel utilisateur](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Créer un nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="3cead-218">![Create New User](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

5. <span data-ttu-id="3cead-219">Dans l’onglet **User Profile** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3cead-219">On the **User Profile** tab, perform the following steps:</span></span>
   
    <span data-ttu-id="3cead-220">![Nouvel utilisateur](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="3cead-220">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="3cead-221">a.</span><span class="sxs-lookup"><span data-stu-id="3cead-221">a.</span></span> <span data-ttu-id="3cead-222">Indiquez le **prénom**, le **nom** et l’**adresse de messagerie** du compte Azure AD valide que vous souhaitez approvisionner, dans les zones de texte correspondantes.</span><span class="sxs-lookup"><span data-stu-id="3cead-222">Type the **user name**, **last name**, and **email address** of a valid Azure Active Directory user into the related textboxes.</span></span>
  
6. <span data-ttu-id="3cead-223">Dans **Status**, sélectionnez **Active**.</span><span class="sxs-lookup"><span data-stu-id="3cead-223">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="3cead-224">Dans l’onglet Password, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3cead-224">On the Password tab, perform the following steps:</span></span>
   
    <span data-ttu-id="3cead-225">![Nouvel utilisateur](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="3cead-225">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="3cead-226">a.</span><span class="sxs-lookup"><span data-stu-id="3cead-226">a.</span></span> <span data-ttu-id="3cead-227">Tapez le mot de passe dans la zone de texte correspondante.</span><span class="sxs-lookup"><span data-stu-id="3cead-227">Type the password into the related textbox.</span></span>

    <span data-ttu-id="3cead-228">b.</span><span class="sxs-lookup"><span data-stu-id="3cead-228">b.</span></span> <span data-ttu-id="3cead-229">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3cead-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="3cead-230">Vous pouvez utiliser n’importe quel outil ou API de création de compte utilisateur, fourni par Sugar CRM, pour approvisionner des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="3cead-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3cead-231">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3cead-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3cead-232">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="3cead-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sugar CRM.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="3cead-234">**Pour affecter Britta Simon à Sugar CRM, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3cead-234">**To assign Britta Simon to Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="3cead-235">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3cead-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="3cead-237">Dans la liste des applications, sélectionnez **Sugar CRM**.</span><span class="sxs-lookup"><span data-stu-id="3cead-237">In the applications list, select **Sugar CRM**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. <span data-ttu-id="3cead-239">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3cead-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="3cead-241">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3cead-241">Click **Add** button.</span></span> <span data-ttu-id="3cead-242">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3cead-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="3cead-244">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3cead-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3cead-245">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3cead-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3cead-246">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3cead-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3cead-247">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="3cead-247">Testing single sign-on</span></span>

<span data-ttu-id="3cead-248">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="3cead-248">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3cead-249">Quand vous cliquez sur la vignette Sugar CRM dans le volet d’accès, vous devez être connecté automatiquement à votre application Sugar CRM.</span><span class="sxs-lookup"><span data-stu-id="3cead-249">When you click the Sugar CRM tile in the Access Panel, you should get automatically signed-on to your Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3cead-250">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3cead-250">Additional resources</span></span>

* [<span data-ttu-id="3cead-251">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3cead-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3cead-252">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="3cead-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

