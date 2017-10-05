---
title: "Didacticiel : Intégration d’Azure Active Directory à LearnUpon | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et LearnUpon."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b11c6315-c79d-4f34-9610-bd17070ab7c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: b6ac8acc244e9029be01ede5e0865c280171217d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learnupon"></a><span data-ttu-id="a98c4-103">Didacticiel : intégration d’Azure Active Directory à LearnUpon</span><span class="sxs-lookup"><span data-stu-id="a98c4-103">Tutorial: Azure Active Directory integration with LearnUpon</span></span>

<span data-ttu-id="a98c4-104">Dans ce didacticiel, vous allez apprendre à intégrer LearnUpon à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a98c4-104">In this tutorial, you learn how to integrate LearnUpon with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a98c4-105">L’intégration de LearnUpon à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a98c4-105">Integrating LearnUpon with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a98c4-106">Dans Azure AD, vous pouvez contrôler qui a accès à LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="a98c4-106">You can control in Azure AD who has access to LearnUpon</span></span>
- <span data-ttu-id="a98c4-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à LearnUpon (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a98c4-107">You can enable your users to automatically get signed-on to LearnUpon (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a98c4-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="a98c4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a98c4-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a98c4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a98c4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a98c4-110">Prerequisites</span></span>

<span data-ttu-id="a98c4-111">Pour configurer l’intégration d’Azure AD à LearnUpon, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a98c4-111">To configure Azure AD integration with LearnUpon, you need the following items:</span></span>

- <span data-ttu-id="a98c4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98c4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a98c4-113">Un abonnement LearnUpon pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a98c4-113">A LearnUpon single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a98c4-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a98c4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a98c4-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a98c4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a98c4-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a98c4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a98c4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a98c4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a98c4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a98c4-118">Scenario description</span></span>
<span data-ttu-id="a98c4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a98c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a98c4-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="a98c4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a98c4-121">Ajout de LearnUpon à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a98c4-121">Adding LearnUpon from the gallery</span></span>
2. <span data-ttu-id="a98c4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98c4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learnupon-from-the-gallery"></a><span data-ttu-id="a98c4-123">Ajout de LearnUpon à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a98c4-123">Adding LearnUpon from the gallery</span></span>
<span data-ttu-id="a98c4-124">Pour configurer l’intégration de LearnUpon à Azure AD, vous devez ajouter LearnUpon de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a98c4-124">To configure the integration of LearnUpon into Azure AD, you need to add LearnUpon from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a98c4-125">**Pour ajouter LearnUpon à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a98c4-125">**To add LearnUpon from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a98c4-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a98c4-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a98c4-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a98c4-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a98c4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a98c4-133">Dans la zone de recherche, saisissez **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-133">In the search box, type **LearnUpon**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_search.png)

5. <span data-ttu-id="a98c4-135">Dans le panneau de résultats, sélectionnez **LearnUpon**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="a98c4-135">In the results panel, select **LearnUpon**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a98c4-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98c4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a98c4-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LearnUpon à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a98c4-138">In this section, you configure and test Azure AD single sign-on with LearnUpon based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a98c4-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur LearnUpon équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a98c4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LearnUpon is to a user in Azure AD.</span></span> <span data-ttu-id="a98c4-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur de LearnUpon associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="a98c4-140">In other words, a link relationship between an Azure AD user and the related user in LearnUpon needs to be established.</span></span>

<span data-ttu-id="a98c4-141">Dans LearnUpon, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="a98c4-141">In LearnUpon, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a98c4-142">Pour configurer et tester l’authentification unique avec Azure AD avec LearnUpon, vous devez compléter les blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="a98c4-142">To configure and test Azure AD single sign-on with LearnUpon, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a98c4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a98c4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a98c4-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a98c4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a98c4-145">**[Création d’un utilisateur de test LearnUpon](#creating-a-learnupon-test-user)** pour avoir un équivalent de Britta Simon dans LearnUpon lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a98c4-145">**[Creating a LearnUpon test user](#creating-a-learnupon-test-user)** - to have a counterpart of Britta Simon in LearnUpon that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a98c4-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a98c4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a98c4-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a98c4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a98c4-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98c4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a98c4-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="a98c4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LearnUpon application.</span></span>

<span data-ttu-id="a98c4-150">**Pour configurer l’authentification unique Azure AD avec LearnUpon, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a98c4-150">**To configure Azure AD single sign-on with LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="a98c4-151">Dans le portail Azure, sur la page d’intégration de l’application **LearnUpon**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-151">In the Azure portal, on the **LearnUpon** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a98c4-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a98c4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_samlbase.png)

3. <span data-ttu-id="a98c4-155">Dans la section **LearnUpon Domain and URLs** (Domaine et URL LearnUpon), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a98c4-155">On the **LearnUpon Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_url.png)

    <span data-ttu-id="a98c4-157">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<companyname>.learnupon.com/saml/consumer`</span><span class="sxs-lookup"><span data-stu-id="a98c4-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.learnupon.com/saml/consumer`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a98c4-158">Notez qu’il ne s’agit pas de la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="a98c4-158">Please note that this is not the real value.</span></span> <span data-ttu-id="a98c4-159">Vous devez mettre à jour cette valeur avec l’URL de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="a98c4-159">you have to update this value with the actual Reply URL.</span></span> <span data-ttu-id="a98c4-160">Pour l’obtenir, contactez [l’équipe de support technique LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="a98c4-160">To get this value Contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span>



4. <span data-ttu-id="a98c4-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (brut)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a98c4-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_certificate.png) 

5. <span data-ttu-id="a98c4-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a98c4-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a98c4-165">Dans la section **LearnUpon Configuration** (Configuration de LearnUpon), cliquez sur **Configure LearnUpon** (Configurer LearnUpon) pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-165">On the **LearnUpon Configuration** section, click **Configure LearnUpon** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a98c4-166">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="a98c4-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_configure.png) 

7. <span data-ttu-id="a98c4-168">Ouvrez une autre instance du navigateur et connectez-vous à LearnUpon avec un compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a98c4-168">Open another browser instance and login into LearnUpon with an administrator account.</span></span> 

8. <span data-ttu-id="a98c4-169">Cliquez sur l’onglet **Paramètres** .</span><span class="sxs-lookup"><span data-stu-id="a98c4-169">Click the **settings** tab.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_06.png)

9. <span data-ttu-id="a98c4-171">Cliquez sur **Authentification unique - SAML**, puis cliquez sur **Paramètres généraux** pour configurer les paramètres SAML.</span><span class="sxs-lookup"><span data-stu-id="a98c4-171">Click **Single Sign On - SAML**, and then click **General Settings** to configure SAML settings.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_07.png) 

10. <span data-ttu-id="a98c4-173">Dans la section **Paramètres généraux** procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a98c4-173">In the **General Settings** section, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_08.png)  
  
    <span data-ttu-id="a98c4-175">a.</span><span class="sxs-lookup"><span data-stu-id="a98c4-175">a.</span></span> <span data-ttu-id="a98c4-176">Sélectionnez **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-176">Select **Enabled**.</span></span>

    <span data-ttu-id="a98c4-177">b.</span><span class="sxs-lookup"><span data-stu-id="a98c4-177">b.</span></span> <span data-ttu-id="a98c4-178">Sélectionnez **2.0** pour **Version**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-178">Select **Version** as **2.0**.</span></span>

    <span data-ttu-id="a98c4-179">c.</span><span class="sxs-lookup"><span data-stu-id="a98c4-179">c.</span></span> <span data-ttu-id="a98c4-180">Sélectionnez **Non** pour **Skip conditions** (Ignorer les conditions).</span><span class="sxs-lookup"><span data-stu-id="a98c4-180">Select **Skip conditions** as **No**.</span></span>

    <span data-ttu-id="a98c4-181">d.</span><span class="sxs-lookup"><span data-stu-id="a98c4-181">d.</span></span> <span data-ttu-id="a98c4-182">Dans la zone de texte **SAML Token POST param name** (Nom de paramètre POST du jeton SAML), entrez le nom du paramètre de publication de demande correspondant à l’URL de consommateur SAML indiquée ci-dessus, qui contient l’assertion SAML à vérifier et à authentifier. Par exemple, **SAMLResponse**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-182">In the **SAML Token Post param name** textbox, type the name of request post parameter to the SAML consumer URL indicated above that contains the SAML Assertion to be verified and authenticated - for example **SAMLResponse**.</span></span>

    <span data-ttu-id="a98c4-183">e.</span><span class="sxs-lookup"><span data-stu-id="a98c4-183">e.</span></span> <span data-ttu-id="a98c4-184">Dans la zone de texte **Format de l’identificateur du nom**, entrez la valeur indiquant à quel emplacement dans votre assertion SAML réside l’identificateur de l’utilisateur (adresse e-mail), par exemple, **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-184">In the **Name Identifier Format** textbox, type the value that indicates where in your SAML Assertion the users identifier (Email address) resides - for example **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>
  
    <span data-ttu-id="a98c4-185">f.</span><span class="sxs-lookup"><span data-stu-id="a98c4-185">f.</span></span> <span data-ttu-id="a98c4-186">Dans la zone de texte **Identify Provider Location** (Identifier l’emplacement du fournisseur), entrez la valeur indiquant l’emplacement vers lequel sont envoyés les utilisateurs lorsqu’ils cliquent sur l’icône de téléchargement à partir de l’écran de connexion au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a98c4-186">In the **Identify Provider Location** textbox, type the value that indicates where the users are sent to if they click on your uploaded icon from your Azure portal login screen.</span></span>
  
    <span data-ttu-id="a98c4-187">g.</span><span class="sxs-lookup"><span data-stu-id="a98c4-187">g.</span></span> <span data-ttu-id="a98c4-188">Dans la zone de texte **URL de déconnexion**, collez **l’URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a98c4-188">In the **Sign out URL** textbox, paste the **Sign-Out URL** which you have copied from the Azure portal.</span></span>
    
    <span data-ttu-id="a98c4-189">h.</span><span class="sxs-lookup"><span data-stu-id="a98c4-189">h.</span></span> <span data-ttu-id="a98c4-190">Cliquez sur **Manage finger prints**(Gérer les empreintes), puis téléchargez l’empreinte du certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="a98c4-190">Click **Manage finger prints**, and then upload the finger print of your downloaded certificate.</span></span>

11. <span data-ttu-id="a98c4-191">Cliquez sur **Paramètres utilisateur**, puis procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a98c4-191">Click **User Settings**, and then perform the following steps:</span></span>
   
     ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_11.png)  
 
    <span data-ttu-id="a98c4-193">a.</span><span class="sxs-lookup"><span data-stu-id="a98c4-193">a.</span></span> <span data-ttu-id="a98c4-194">Dans la zone de texte **First Name Identifier Format** (Format de l’identificateur du prénom), entrez la valeur indiquant à quel emplacement dans votre assertion SAML réside le prénom des utilisateurs, par exemple, **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-194">In the **First Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users firstname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>
  
    <span data-ttu-id="a98c4-195">b.</span><span class="sxs-lookup"><span data-stu-id="a98c4-195">b.</span></span> <span data-ttu-id="a98c4-196">Dans la zone de texte **Last Name Identifier Format** (Format de l’identificateur du nom), entrez la valeur indiquant à quel emplacement dans votre assertion SAML réside le nom des utilisateurs, par exemple, **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-196">In the **Last Name Identifier Format** textbox, type the value that tells us where in your SAML Assertion the users lastname resides - for example: **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

> [!TIP]
> <span data-ttu-id="a98c4-197">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="a98c4-197">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a98c4-198">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="a98c4-198">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a98c4-199">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a98c4-199">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a98c4-200">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98c4-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="a98c4-201">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a98c4-201">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a98c4-203">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a98c4-203">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a98c4-204">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-204">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a98c4-206">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-206">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a98c4-208">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a98c4-208">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a98c4-210">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a98c4-210">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-learnupon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a98c4-212">a.</span><span class="sxs-lookup"><span data-stu-id="a98c4-212">a.</span></span> <span data-ttu-id="a98c4-213">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-213">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a98c4-214">b.</span><span class="sxs-lookup"><span data-stu-id="a98c4-214">b.</span></span> <span data-ttu-id="a98c4-215">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a98c4-215">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a98c4-216">c.</span><span class="sxs-lookup"><span data-stu-id="a98c4-216">c.</span></span> <span data-ttu-id="a98c4-217">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-217">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a98c4-218">d.</span><span class="sxs-lookup"><span data-stu-id="a98c4-218">d.</span></span> <span data-ttu-id="a98c4-219">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-219">Click **Create**.</span></span>
 
### <a name="creating-a-learnupon-test-user"></a><span data-ttu-id="a98c4-220">Création d’un utilisateur de test LearnUpon</span><span class="sxs-lookup"><span data-stu-id="a98c4-220">Creating a LearnUpon test user</span></span>

<span data-ttu-id="a98c4-221">L’objectif de cette section est de créer l’utilisateur Britta Simon dans LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="a98c4-221">The objective of this section is to create a user called Britta Simon in LearnUpon.</span></span> <span data-ttu-id="a98c4-222">LearnUpon prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="a98c4-222">LearnUpon supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a98c4-223">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="a98c4-223">There is no action item for you in this section.</span></span> <span data-ttu-id="a98c4-224">Un utilisateur est créé au moment d’une tentative d’accès à LearnUpon s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="a98c4-224">A new user will be created during an attempt to access LearnUpon if it doesn't exist yet.</span></span> <span data-ttu-id="a98c4-225">[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="a98c4-225">[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on).</span></span>

>[!NOTE]
><span data-ttu-id="a98c4-226">Si vous devez créer un utilisateur manuellement, contactez [l’équipe de support technique LearnUpon](https://www.learnupon.com/features/support/).</span><span class="sxs-lookup"><span data-stu-id="a98c4-226">If you need to create an user manually, you need to contact [LearnUpon support team](https://www.learnupon.com/features/support/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a98c4-227">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a98c4-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a98c4-228">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="a98c4-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LearnUpon.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a98c4-230">**Pour affecter Britta Simon à LearnUpon, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a98c4-230">**To assign Britta Simon to LearnUpon, perform the following steps:**</span></span>

1. <span data-ttu-id="a98c4-231">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a98c4-233">Dans la liste des applications, sélectionnez **LearnUpon**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-233">In the applications list, select **LearnUpon**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-learnupon-tutorial/tutorial_learnupon_app.png) 

3. <span data-ttu-id="a98c4-235">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-235">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a98c4-237">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-237">Click **Add** button.</span></span> <span data-ttu-id="a98c4-238">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a98c4-240">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a98c4-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a98c4-241">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a98c4-242">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a98c4-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a98c4-243">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a98c4-243">Testing single sign-on</span></span>

<span data-ttu-id="a98c4-244">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="a98c4-244">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a98c4-245">Quand vous cliquez sur la vignette LearnUpon dans le volet d’accès, vous devez être connecté automatiquement à votre application LearnUpon.</span><span class="sxs-lookup"><span data-stu-id="a98c4-245">When you click the LearnUpon tile in the Access Panel, you should get automatically signed-on to your LearnUpon application.</span></span>
<span data-ttu-id="a98c4-246">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a98c4-246">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a98c4-247">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a98c4-247">Additional resources</span></span>

* [<span data-ttu-id="a98c4-248">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a98c4-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a98c4-249">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a98c4-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnupon-tutorial/tutorial_general_203.png

