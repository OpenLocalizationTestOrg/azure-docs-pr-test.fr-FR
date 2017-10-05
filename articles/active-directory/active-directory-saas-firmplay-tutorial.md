---
title: "Didacticiel : Intégration d’Azure Active Directory à FirmPlay - Employee Advocacy for Recruiting | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et FirmPlay - Employee Advocacy for Recruiting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: 3cddd5b9508159089bf344dbb3882d462799747c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a><span data-ttu-id="3521e-103">Didacticiel : Intégration d’Azure Active Directory à FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="3521e-103">Tutorial: Azure Active Directory integration with FirmPlay - Employee Advocacy for Recruiting</span></span>

<span data-ttu-id="3521e-104">Dans ce didacticiel, vous allez apprendre à intégrer FirmPlay - Employee Advocacy for Recruiting à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3521e-104">In this tutorial, you learn how to integrate FirmPlay - Employee Advocacy for Recruiting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3521e-105">L’intégration de FirmPlay - Employee Advocacy for Recruiting dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="3521e-105">Integrating FirmPlay - Employee Advocacy for Recruiting with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3521e-106">Vous pouvez contrôler dans Azure AD qui a accès à FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="3521e-106">You can control in Azure AD who has access to FirmPlay - Employee Advocacy for Recruiting</span></span>
- <span data-ttu-id="3521e-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à FirmPlay - Employee Advocacy for Recruiting (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3521e-107">You can enable your users to automatically get signed-on to FirmPlay - Employee Advocacy for Recruiting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3521e-108">Vous pouvez gérer vos comptes de manière centralisée dans le Portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="3521e-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="3521e-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3521e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3521e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3521e-110">Prerequisites</span></span>

<span data-ttu-id="3521e-111">Pour configurer l’intégration d’Azure AD à FirmPlay - Employee Advocacy for Recruiting, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3521e-111">To configure Azure AD integration with FirmPlay - Employee Advocacy for Recruiting, you need the following items:</span></span>

- <span data-ttu-id="3521e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="3521e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3521e-113">Un abonnement FirmPlay - Employee Advocacy for Recruiting pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="3521e-113">A FirmPlay - Employee Advocacy for Recruiting single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="3521e-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="3521e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="3521e-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3521e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3521e-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="3521e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="3521e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3521e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="3521e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="3521e-118">Scenario description</span></span>
<span data-ttu-id="3521e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="3521e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3521e-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="3521e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3521e-121">Ajout de FirmPlay - Employee Advocacy for Recruiting à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="3521e-121">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
2. <span data-ttu-id="3521e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3521e-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-the-gallery"></a><span data-ttu-id="3521e-123">Ajout de FirmPlay - Employee Advocacy for Recruiting à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="3521e-123">Adding FirmPlay - Employee Advocacy for Recruiting from the gallery</span></span>
<span data-ttu-id="3521e-124">Pour configurer l’intégration de FirmPlay - Employee Advocacy for Recruiting dans Azure AD, vous devez ajouter FirmPlay - Employee Advocacy for Recruiting à partir de la galerie dans votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="3521e-124">To configure the integration of FirmPlay - Employee Advocacy for Recruiting into Azure AD, you need to add FirmPlay - Employee Advocacy for Recruiting from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3521e-125">**Pour ajouter FirmPlay - Employee Advocacy for Recruiting à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3521e-125">**To add FirmPlay - Employee Advocacy for Recruiting from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3521e-126">Dans le **[Portail de gestion Azure](https://portal.azure.com)**, dans le panneau de navigation gauche, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3521e-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3521e-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="3521e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3521e-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3521e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="3521e-131">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="3521e-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="3521e-133">Dans la zone de recherche, tapez **FirmPlay - Employee Advocacy for Recruiting**.</span><span class="sxs-lookup"><span data-stu-id="3521e-133">In the search box, type **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. <span data-ttu-id="3521e-135">Dans le volet de résultats, sélectionnez **FirmPlay - Employee Advocacy for Recruiting**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="3521e-135">In the results panel, select **FirmPlay - Employee Advocacy for Recruiting**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3521e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3521e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3521e-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec FirmPlay - Employee Advocacy for Recruiting avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="3521e-138">In this section, you configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3521e-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur FirmPlay - Employee Advocacy for Recruiting équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3521e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FirmPlay - Employee Advocacy for Recruiting is to a user in Azure AD.</span></span> <span data-ttu-id="3521e-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur FirmPlay - Employee Advocacy for Recruiting associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="3521e-140">In other words, a link relationship between an Azure AD user and the related user in FirmPlay - Employee Advocacy for Recruiting needs to be established.</span></span>

<span data-ttu-id="3521e-141">Pour ce faire, affectez la valeur du champ **nom d’utilisateur** d’Azure AD comme valeur de **nom d’utilisateur** dans FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="3521e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FirmPlay - Employee Advocacy for Recruiting.</span></span>

<span data-ttu-id="3521e-142">Pour configurer et tester l’authentification unique Azure AD avec FirmPlay - Employee Advocacy for Recruiting, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="3521e-142">To configure and test Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3521e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="3521e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3521e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3521e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3521e-145">**[Création d’un utilisateur de test FirmPlay - Employee Advocacy for Recruiting](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** pour disposer d’un équivalent de Britta Simon dans FirmPlay - Employee Advocacy for Recruiting associé à sa représentation Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3521e-145">**[Creating a FirmPlay - Employee Advocacy for Recruiting test user](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)** - to have a counterpart of Britta Simon in FirmPlay: Employee Advocacy for Recruiting that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="3521e-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3521e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3521e-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="3521e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3521e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="3521e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3521e-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail de gestion Azure et configurer l’authentification unique dans votre application FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="3521e-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FirmPlay - Employee Advocacy for Recruiting application.</span></span>

<span data-ttu-id="3521e-150">**Pour configurer l’authentification unique d’Azure AD avec FirmPlay - Employee Advocacy for Recruiting, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3521e-150">**To configure Azure AD single sign-on with FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="3521e-151">Dans le portail de gestion Azure, sur la page d’intégration de l’application **FirmPlay - Employee Advocacy for Recruiting**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="3521e-151">In the Azure Management portal, on the **FirmPlay - Employee Advocacy for Recruiting** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="3521e-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3521e-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. <span data-ttu-id="3521e-155">Dans la section **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** (Domaine et URL FirmPlay - Employee Advocacy for Recruiting), dans la zone de texte **URL de connexion**, entrez une URL respectant le modèle suivant : `https://<your-subdomain>.firmplay.com/`</span><span class="sxs-lookup"><span data-stu-id="3521e-155">On the **FirmPlay - Employee Advocacy for Recruiting Domain and URLs** section, in the **Sign On URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.firmplay.com/`</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > <span data-ttu-id="3521e-157">Notez qu’il ne s’agit pas de la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="3521e-157">Please note that this is not the real value.</span></span> <span data-ttu-id="3521e-158">Vous devez mettre à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="3521e-158">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="3521e-159">Contactez [l’équipe de support de FirmPlay - Employee Advocacy for Recruiting](mailto:engineering@firmplay.com) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="3521e-159">Contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to get this value.</span></span> 

4. <span data-ttu-id="3521e-160">Dans la section **Certificat de signature SAML**, cliquez sur **Créer un certificat**.</span><span class="sxs-lookup"><span data-stu-id="3521e-160">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. <span data-ttu-id="3521e-162">Dans la boîte de dialogue **Créer un certificat**, cliquez sur l’icône de calendrier et sélectionnez une **date d’expiration**.</span><span class="sxs-lookup"><span data-stu-id="3521e-162">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="3521e-163">Ensuite, cliquez sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3521e-163">Then click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="3521e-165">Dans la section **Certificat de signature SAML**, sélectionnez **Activer le nouveau certificat** et cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3521e-165">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. <span data-ttu-id="3521e-167">Dans la fenêtre contextuelle **Certificat de substitution**, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3521e-167">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="3521e-169">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3521e-169">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. <span data-ttu-id="3521e-171">Dans la section **FirmPlay - Employee Advocacy for Recruiting Configuration** (Configuration de FirmPlay - Employee Advocacy for Recruiting), cliquez sur **Configure FirmPlay - Employee Advocacy for Recruiting** (Configurer FirmPlay - Employee Advocacy for Recruiting) pour ouvrir la boîte de dialogue **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="3521e-171">On the **FirmPlay - Employee Advocacy for Recruiting Configuration** section, click **Configure FirmPlay - Employee Advocacy for Recruiting** to open **Configure sign-on** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. <span data-ttu-id="3521e-174">Pour obtenir la configuration de l’authentification unique pour votre application, contactez [l’équipe de support de FirmPlay - Employee Advocacy for Recruiting](mailto:engineering@firmplay.com) et fournissez-lui les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3521e-174">To get SSO configured for your application, contact [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) and provide them with the following:</span></span> 

    <span data-ttu-id="3521e-175">•  Le **fichier de certificat** téléchargé</span><span class="sxs-lookup"><span data-stu-id="3521e-175">•  The downloaded **Certificate file**</span></span>

    <span data-ttu-id="3521e-176">•  L’**URL du service d’authentification unique SAML**</span><span class="sxs-lookup"><span data-stu-id="3521e-176">•  The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="3521e-177">•  L’**ID d’entité SAML**</span><span class="sxs-lookup"><span data-stu-id="3521e-177">•  The **SAML Entity ID**</span></span>

    <span data-ttu-id="3521e-178">•  L’**URL de déconnexion**</span><span class="sxs-lookup"><span data-stu-id="3521e-178">•  The **Sign-Out URL**</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3521e-179">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3521e-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="3521e-180">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le Portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="3521e-180">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="3521e-182">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3521e-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3521e-183">Dans le panneau de navigation gauche du **Portail de gestion Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3521e-183">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3521e-185">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3521e-185">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3521e-187">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="3521e-187">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3521e-189">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3521e-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3521e-191">a.</span><span class="sxs-lookup"><span data-stu-id="3521e-191">a.</span></span> <span data-ttu-id="3521e-192">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3521e-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3521e-193">b.</span><span class="sxs-lookup"><span data-stu-id="3521e-193">b.</span></span> <span data-ttu-id="3521e-194">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3521e-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3521e-195">c.</span><span class="sxs-lookup"><span data-stu-id="3521e-195">c.</span></span> <span data-ttu-id="3521e-196">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="3521e-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3521e-197">d.</span><span class="sxs-lookup"><span data-stu-id="3521e-197">d.</span></span> <span data-ttu-id="3521e-198">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="3521e-198">Click **Create**.</span></span> 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a><span data-ttu-id="3521e-199">Création d’un utilisateur de test FirmPlay - Employee Advocacy for Recruiting</span><span class="sxs-lookup"><span data-stu-id="3521e-199">Creating a FirmPlay - Employee Advocacy for Recruiting test user</span></span>

<span data-ttu-id="3521e-200">Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="3521e-200">In this section, you create a user called Britta Simon in FirmPlay - Employee Advocacy for Recruiting.</span></span> <span data-ttu-id="3521e-201">Contactez [l’équipe de support de FirmPlay - Employee Advocacy for Recruiting](mailto:engineering@firmplay.com) pour ajouter les utilisateurs à la plateforme FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="3521e-201">Please work with [FirmPlay - Employee Advocacy for Recruiting support team](mailto:engineering@firmplay.com) to add the users in the FirmPlay - Employee Advocacy for Recruiting platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3521e-202">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="3521e-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3521e-203">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="3521e-203">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to FirmPlay - Employee Advocacy for Recruiting.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="3521e-205">**Pour affecter Britta Simon à FirmPlay - Employee Advocacy for Recruiting, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="3521e-205">**To assign Britta Simon to FirmPlay - Employee Advocacy for Recruiting, perform the following steps:**</span></span>

1. <span data-ttu-id="3521e-206">Dans le Portail de gestion Azure, ouvrez la vue des applications, accédez à la vue des répertoires, allez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="3521e-206">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="3521e-208">Dans la liste des applications, sélectionnez **FirmPlay - Employee Advocacy for Recruiting**.</span><span class="sxs-lookup"><span data-stu-id="3521e-208">In the applications list, select **FirmPlay - Employee Advocacy for Recruiting**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. <span data-ttu-id="3521e-210">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3521e-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="3521e-212">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3521e-212">Click **Add** button.</span></span> <span data-ttu-id="3521e-213">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3521e-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="3521e-215">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3521e-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3521e-216">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="3521e-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3521e-217">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="3521e-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="3521e-218">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="3521e-218">Testing single sign-on</span></span>

<span data-ttu-id="3521e-219">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="3521e-219">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3521e-220">Lorsque vous cliquez sur la mosaïque FirmPlay - Employee Advocacy for Recruiting dans le volet d’accès, vous devez être connecté automatiquement à votre application FirmPlay - Employee Advocacy for Recruiting.</span><span class="sxs-lookup"><span data-stu-id="3521e-220">When you click the FirmPlay - Employee Advocacy for Recruiting tile in the Access Panel, you should get automatically signed-on to your FirmPlay - Employee Advocacy for Recruiting application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="3521e-221">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3521e-221">Additional resources</span></span>

* [<span data-ttu-id="3521e-222">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3521e-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3521e-223">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="3521e-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png