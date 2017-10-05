---
title: "Didacticiel : Intégration d’Azure Active Directory à SuccessFactors | Microsoft Docs"
description: "Découvrez comment utiliser SuccessFactors avec Azure Active Directory pour activer l’authentification unique, l’approvisionnement automatique et bien plus encore."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e85a38ccbe25263ac42bc76351416b023fb77c87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="56cda-103">Didacticiel : Intégration d’Azure Active Directory à SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="56cda-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="56cda-104">L’objectif de ce didacticiel est de vous montrer comment intégrer SuccessFactors dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="56cda-104">The objective of this tutorial is to show you how to integrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="56cda-105">L’intégration de SuccessFactors dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="56cda-105">Integrating SuccessFactors with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="56cda-106">Dans Azure AD, vous pouvez contrôler qui a accès à SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="56cda-106">You can control in Azure AD who has access to SuccessFactors</span></span>
* <span data-ttu-id="56cda-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à SuccessFactors (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56cda-107">You can enable your users to automatically get signed-on to SuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="56cda-108">Vous pouvez gérer vos comptes à un emplacement central : le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="56cda-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="56cda-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="56cda-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56cda-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="56cda-110">Prerequisites</span></span>
<span data-ttu-id="56cda-111">Pour configurer l’intégration d’Azure AD à SuccessFactors, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="56cda-111">To configure Azure AD integration with SuccessFactors, you need the following items:</span></span>

* <span data-ttu-id="56cda-112">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="56cda-112">A valid Azure subscription</span></span>
* <span data-ttu-id="56cda-113">Un locataire SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="56cda-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="56cda-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="56cda-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="56cda-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="56cda-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="56cda-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="56cda-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="56cda-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56cda-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56cda-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="56cda-118">Scenario description</span></span>
<span data-ttu-id="56cda-119">Ce didacticiel vise à vous permettre de tester l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="56cda-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="56cda-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="56cda-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56cda-121">Ajout de SuccessFactors à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="56cda-121">Adding SuccessFactors from the gallery</span></span>
2. <span data-ttu-id="56cda-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="56cda-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-the-gallery"></a><span data-ttu-id="56cda-123">Ajout de SuccessFactors à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="56cda-123">Adding SuccessFactors from the gallery</span></span>
<span data-ttu-id="56cda-124">Pour configurer l’intégration de SuccessFactors à Azure AD, vous devez ajouter SuccessFactors à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="56cda-124">To configure the integration of SuccessFactors into Azure AD, you need to add SuccessFactors from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="56cda-125">**Pour ajouter SuccessFactors à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="56cda-125">**To add SuccessFactors from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="56cda-126">Dans le volet de navigation gauche du portail Azure Classic, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="56cda-126">In the Azure classic portal, on the left navigation panel, click **Active Directory**.</span></span>
   
    ![Configuration de l'authentification unique][1]
2. <span data-ttu-id="56cda-128">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="56cda-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="56cda-129">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="56cda-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Configuration de l'authentification unique][2]
4. <span data-ttu-id="56cda-131">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="56cda-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="56cda-133">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="56cda-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Configuration de l'authentification unique][4]
6. <span data-ttu-id="56cda-135">Dans la **zone de recherche**, tapez **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="56cda-135">In the **search box**, type **SuccessFactors**.</span></span>
   
    ![Configuration de l'authentification unique][5]
7. <span data-ttu-id="56cda-137">Dans le volet des résultats, sélectionnez **SuccessFactors**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="56cda-137">In the results panel, select **SuccessFactors**, and then click **Complete** to add the application.</span></span>
   
    ![Configuration de l'authentification unique][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="56cda-139">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="56cda-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="56cda-140">L’objectif de cette section est de vous montrer comment configurer et tester l’authentification unique Azure AD avec SuccessFactors avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="56cda-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="56cda-141">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur SuccessFactors équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56cda-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SuccessFactors to an user in Azure AD is.</span></span> <span data-ttu-id="56cda-142">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur SuccessFactors associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="56cda-142">In other words, a link relationship between an Azure AD user and the related user in SuccessFactors needs to be established.</span></span>

<span data-ttu-id="56cda-143">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="56cda-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SuccessFactors.</span></span>

<span data-ttu-id="56cda-144">Pour configurer et tester l’authentification unique Azure AD avec SuccessFactors, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="56cda-144">To configure and test Azure AD single sign-on with SuccessFactors, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="56cda-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="56cda-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="56cda-146">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="56cda-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56cda-147">**[Création d’un utilisateur de test SuccessFactors](#creating-a-successfactors-test-user)** pour avoir un équivalent de Britta Simon dans SuccessFactors lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="56cda-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - to have a counterpart of Britta Simon in SuccessFactors that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="56cda-148">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56cda-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56cda-149">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="56cda-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="56cda-150">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="56cda-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="56cda-151">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure Classic et configurer l’authentification unique dans votre application SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="56cda-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="56cda-152">**Pour configurer l’authentification unique Azure AD avec SuccessFactors, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="56cda-152">**To configure Azure AD single sign-on with SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="56cda-153">Sur la page d’intégration d’application **SuccessFactors** du portail Azure Classic, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="56cda-153">In the Azure classic portal, on the **SuccessFactors** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    ![Configuration de l'authentification unique][7]
2. <span data-ttu-id="56cda-155">Dans la page **Comment voulez-vous que les utilisateurs se connectent à SuccessFactors**, sélectionnez **Authentification unique avec Microsoft Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="56cda-155">On the **How would you like users to sign on to SuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configuration de l'authentification unique][8]
3. <span data-ttu-id="56cda-157">Dans la page **Configurer l’URL de l’application**, procédez comme suit, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="56cda-157">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    ![Configuration de l'authentification unique][9]
   
    <span data-ttu-id="56cda-159">a.</span><span class="sxs-lookup"><span data-stu-id="56cda-159">a.</span></span> <span data-ttu-id="56cda-160">Dans la zone de texte **URL de connexion** , tapez une URL en respectant l’un des formats suivants :</span><span class="sxs-lookup"><span data-stu-id="56cda-160">In the **Sign On URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="56cda-161">b.</span><span class="sxs-lookup"><span data-stu-id="56cda-161">b.</span></span> <span data-ttu-id="56cda-162">Dans la zone de texte **URL de réponse** , tapez une URL en respectant l’un des formats suivants :</span><span class="sxs-lookup"><span data-stu-id="56cda-162">In the **Reply URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="56cda-163">c.</span><span class="sxs-lookup"><span data-stu-id="56cda-163">c.</span></span> <span data-ttu-id="56cda-164">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="56cda-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="56cda-165">Notez qu’il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="56cda-165">Please note that these are not the real values.</span></span> <span data-ttu-id="56cda-166">Vous devez mettre à jour ces valeurs avec l’URL de connexion et l’URL de réponse réelles.</span><span class="sxs-lookup"><span data-stu-id="56cda-166">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="56cda-167">Pour obtenir ces valeurs, contactez [l’équipe du support technique SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="56cda-167">To get these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="56cda-168">Dans la page **Configurer l’authentification unique sur SuccessFactors**, cliquez sur **Télécharger le certificat**, puis enregistrez le fichier de certificat en local sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="56cda-168">On the **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Configuration de l'authentification unique][10]

2. <span data-ttu-id="56cda-170">Dans une autre fenêtre de navigateur web, connectez-vous à votre **portail d’administration SuccessFactors** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="56cda-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="56cda-171">Dans **Application Security** (Sécurité des applications), accédez à la **fonctionnalité d’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="56cda-171">Visit **Application Security** and native to **Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="56cda-172">Indiquez une valeur dans le champ **Reset Token** (Réinitialiser le jeton), puis cliquez sur **Save Token** (Enregistrer le jeton) pour activer l’authentification unique SAML.</span><span class="sxs-lookup"><span data-stu-id="56cda-172">Place any value in the **Reset Token** and click **Save Token** to enable SAML SSO.</span></span>
   
    ![Configuration de l’authentification unique côté application][11]

    > [!NOTE] 
    > <span data-ttu-id="56cda-174">Cette valeur est uniquement utilisée en tant que commutateur marche/arrêt.</span><span class="sxs-lookup"><span data-stu-id="56cda-174">This value is just used as the on/off switch.</span></span> <span data-ttu-id="56cda-175">Si une valeur est enregistrée, l’authentification unique SAML est activée.</span><span class="sxs-lookup"><span data-stu-id="56cda-175">If any value is saved, the SAML SSO is ON.</span></span> <span data-ttu-id="56cda-176">Si aucune valeur n’est enregistrée, l’authentification unique SAML est désactivée.</span><span class="sxs-lookup"><span data-stu-id="56cda-176">If a blank value is saved the SAML SSO is OFF.</span></span>

1. <span data-ttu-id="56cda-177">Accédez à la capture d’écran ci-dessous et effectuez les actions suivantes.</span><span class="sxs-lookup"><span data-stu-id="56cda-177">Native to below screenshot and perform the following actions.</span></span>
   
    ![Configuration de l’authentification unique côté application][12]
   
    <span data-ttu-id="56cda-179">a.</span><span class="sxs-lookup"><span data-stu-id="56cda-179">a.</span></span> <span data-ttu-id="56cda-180">Sélectionnez la case d’option **SAML v2 SSO** .</span><span class="sxs-lookup"><span data-stu-id="56cda-180">Select the **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="56cda-181">b.</span><span class="sxs-lookup"><span data-stu-id="56cda-181">b.</span></span> <span data-ttu-id="56cda-182">Définissez le nom de partie de confiance SAML (par exemple, émetteur SAML + nom de l’entreprise).</span><span class="sxs-lookup"><span data-stu-id="56cda-182">Set the SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="56cda-183">c.</span><span class="sxs-lookup"><span data-stu-id="56cda-183">c.</span></span> <span data-ttu-id="56cda-184">Dans la zone de texte **SAML Issuer** (Émetteur SAML), copiez la valeur de **l’URL de l’émetteur** indiquée dans l’Assistant Configuration de l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56cda-184">In the **SAML Issuer** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="56cda-185">d.</span><span class="sxs-lookup"><span data-stu-id="56cda-185">d.</span></span> <span data-ttu-id="56cda-186">Sélectionnez **Response(Customer Generated/IdP/AP)** (Réponse (générée par le client/fournisseur d’identité/point d’accès)) pour **Require Mandatory Signature** (Exiger une signature obligatoire).</span><span class="sxs-lookup"><span data-stu-id="56cda-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="56cda-187">e.</span><span class="sxs-lookup"><span data-stu-id="56cda-187">e.</span></span> <span data-ttu-id="56cda-188">Sélectionnez **Enabled** (Activé) dans le champ **Enable SAML Flag** (Activer l’indicateur SAML).</span><span class="sxs-lookup"><span data-stu-id="56cda-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="56cda-189">f.</span><span class="sxs-lookup"><span data-stu-id="56cda-189">f.</span></span> <span data-ttu-id="56cda-190">Sélectionnez **No** (Non) dans le champ **Login Request Signature(SF Generated/SP/RP)** (Signature de la demande de connexion (générée par SF/fournisseur de services/fournisseur de ressources)).</span><span class="sxs-lookup"><span data-stu-id="56cda-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="56cda-191">g.</span><span class="sxs-lookup"><span data-stu-id="56cda-191">g.</span></span> <span data-ttu-id="56cda-192">Sélectionnez **Browser/Post Profile** (Navigateur/Post-profilage) en tant que **profil SAML**.</span><span class="sxs-lookup"><span data-stu-id="56cda-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="56cda-193">h.</span><span class="sxs-lookup"><span data-stu-id="56cda-193">h.</span></span> <span data-ttu-id="56cda-194">Sélectionnez **No** (Non) dans le champ **Enforce Certificate Valid Period** (Appliquer la période valide du certificat).</span><span class="sxs-lookup"><span data-stu-id="56cda-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="56cda-195">i.</span><span class="sxs-lookup"><span data-stu-id="56cda-195">i.</span></span> <span data-ttu-id="56cda-196">Copiez le contenu du fichier de certificat téléchargé, puis collez-le dans la zone de texte **SAML Verifying Certificate** (Certificat de vérification SAML).</span><span class="sxs-lookup"><span data-stu-id="56cda-196">Copy the content of the downloaded certificate file, and then paste it into the **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="56cda-197">Le contenu du certificat doit comporter des balises de début et de fin de certificat.</span><span class="sxs-lookup"><span data-stu-id="56cda-197">The certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="56cda-198">Accédez à SAML V2, puis procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="56cda-198">Navigate to SAML V2, and then perform the following steps:</span></span>
   
    ![Configuration de l’authentification unique côté application][13]
   
    <span data-ttu-id="56cda-200">a.</span><span class="sxs-lookup"><span data-stu-id="56cda-200">a.</span></span> <span data-ttu-id="56cda-201">Sélectionnez **Yes** (Oui) dans **Support SP-initiated Global Logout** (Prendre en charge la déconnexion globale initiée par le fournisseur de services).</span><span class="sxs-lookup"><span data-stu-id="56cda-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="56cda-202">b.</span><span class="sxs-lookup"><span data-stu-id="56cda-202">b.</span></span> <span data-ttu-id="56cda-203">Dans la zone de texte **Global Logout Service URL (LogoutRequest destination)** (URL de service de déconnexion globale (destination LogoutRequest)), copiez la valeur de **l’URL de déconnexion distante** indiquée dans l’Assistant Configuration de l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56cda-203">In the **Global Logout Service URL (LogoutRequest destination)** textbox put the value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="56cda-204">c.</span><span class="sxs-lookup"><span data-stu-id="56cda-204">c.</span></span> <span data-ttu-id="56cda-205">Sélectionnez **No** (Non) dans **Require sp must encrypt all NameID element** (Exiger que le fournisseur de services chiffre tous les éléments NameID).</span><span class="sxs-lookup"><span data-stu-id="56cda-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="56cda-206">d.</span><span class="sxs-lookup"><span data-stu-id="56cda-206">d.</span></span> <span data-ttu-id="56cda-207">Sélectionnez **unspecified** (non spécifié) dans **NameID Format** (Format NameID).</span><span class="sxs-lookup"><span data-stu-id="56cda-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="56cda-208">e.</span><span class="sxs-lookup"><span data-stu-id="56cda-208">e.</span></span> <span data-ttu-id="56cda-209">Sélectionnez **Yes** (Oui) dans **Enable sp initiated login (AuthnRequest)** (Activer la connexion initiée par le fournisseur de services (AuthnRequest)).</span><span class="sxs-lookup"><span data-stu-id="56cda-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="56cda-210">f.</span><span class="sxs-lookup"><span data-stu-id="56cda-210">f.</span></span> <span data-ttu-id="56cda-211">Dans la zone de texte **Send request as Company-Wide issuer** (Envoyer la demande en tant qu’émetteur au niveau de l’entreprise), copiez la valeur de **l’URL de connexion distante** indiquée dans l’Assistant Configuration de l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56cda-211">In the **Send request as Company-Wide issuer** textbox put the value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="56cda-212">Procédez comme suit si vous souhaitez que les noms d’utilisateur de connexion ne respectent pas la casse :</span><span class="sxs-lookup"><span data-stu-id="56cda-212">Perform these steps if you want to make the login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="56cda-213">a.</span><span class="sxs-lookup"><span data-stu-id="56cda-213">a.</span></span> <span data-ttu-id="56cda-214">Accédez à **Company Settings** (Paramètres de l’entreprise) (en bas).</span><span class="sxs-lookup"><span data-stu-id="56cda-214">Visit **Company Settings**(near the bottom).</span></span>
   
    <span data-ttu-id="56cda-215">b.</span><span class="sxs-lookup"><span data-stu-id="56cda-215">b.</span></span> <span data-ttu-id="56cda-216">Sélectionnez la case à cocher près de **Enable Non-Case-Sensitive Username**(Activer le non-respect de la casse pour les noms d’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="56cda-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="56cda-217">c. Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="56cda-217">c.Click **Save**.</span></span>
   
    ![Configurer l’authentification unique][29]

    > [!NOTE] 
    > <span data-ttu-id="56cda-219">Si vous essayez d’activer cette option, le système vérifie si un nom de connexion SAML est créé en double.</span><span class="sxs-lookup"><span data-stu-id="56cda-219">If you try to enable this, the system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="56cda-220">Par exemple, si le client possède les noms d’utilisateur User1 et user1.</span><span class="sxs-lookup"><span data-stu-id="56cda-220">For example if the customer has usernames User1 and user1.</span></span> <span data-ttu-id="56cda-221">Si vous désactivez le respect de la casse, ces noms deviennent des doublons.</span><span class="sxs-lookup"><span data-stu-id="56cda-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="56cda-222">Le système vous transmettra un message d’erreur et n’activera pas la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="56cda-222">The system will give you an error message and will not enable the feature.</span></span> <span data-ttu-id="56cda-223">Le client devra modifier l’un des noms d’utilisateur afin qu’il soit orthographié différemment.</span><span class="sxs-lookup"><span data-stu-id="56cda-223">The customer will need to change one of the usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="56cda-224">Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Terminer** pour fermer la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="56cda-224">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    ![Applications][14]
2. <span data-ttu-id="56cda-226">Sur la page **Confirmation de l’authentification unique**, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="56cda-226">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Applications][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="56cda-228">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="56cda-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="56cda-229">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail classique.</span><span class="sxs-lookup"><span data-stu-id="56cda-229">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][16]

<span data-ttu-id="56cda-231">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="56cda-231">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="56cda-232">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="56cda-232">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD][17]
2. <span data-ttu-id="56cda-234">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="56cda-234">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="56cda-235">Pour afficher la liste des utilisateurs, dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="56cda-235">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD][18]
4. <span data-ttu-id="56cda-237">Pour ouvrir la boîte de dialogue **Ajouter un utilisateur**, cliquez sur l’option **Ajouter un utilisateur** figurant dans la barre d’outils du bas.</span><span class="sxs-lookup"><span data-stu-id="56cda-237">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD][19]
5. <span data-ttu-id="56cda-239">Sur la page de boîte de dialogue **Dites-nous en plus sur cet utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="56cda-239">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD][20]
   
    <span data-ttu-id="56cda-241">a.</span><span class="sxs-lookup"><span data-stu-id="56cda-241">a.</span></span> <span data-ttu-id="56cda-242">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="56cda-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="56cda-243">b.</span><span class="sxs-lookup"><span data-stu-id="56cda-243">b.</span></span> <span data-ttu-id="56cda-244">Dans la zone de texte **Nom d’utilisateur**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="56cda-244">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="56cda-245">c.</span><span class="sxs-lookup"><span data-stu-id="56cda-245">c.</span></span> <span data-ttu-id="56cda-246">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="56cda-246">Click **Next**.</span></span>
6. <span data-ttu-id="56cda-247">Sur la page de boîte de dialogue **Profil utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="56cda-247">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD][21]
   
    <span data-ttu-id="56cda-249">a.</span><span class="sxs-lookup"><span data-stu-id="56cda-249">a.</span></span> <span data-ttu-id="56cda-250">Dans la zone de texte **First Name**, tapez **Britta**.</span><span class="sxs-lookup"><span data-stu-id="56cda-250">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="56cda-251">b.</span><span class="sxs-lookup"><span data-stu-id="56cda-251">b.</span></span> <span data-ttu-id="56cda-252">Dans la zone de texte **Last Name**, tapez **Simon**.</span><span class="sxs-lookup"><span data-stu-id="56cda-252">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="56cda-253">c.</span><span class="sxs-lookup"><span data-stu-id="56cda-253">c.</span></span> <span data-ttu-id="56cda-254">Dans la zone de texte **Nom d’affichage**, entrez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="56cda-254">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="56cda-255">d.</span><span class="sxs-lookup"><span data-stu-id="56cda-255">d.</span></span> <span data-ttu-id="56cda-256">Dans la liste **Rôle**, sélectionnez **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="56cda-256">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="56cda-257">e.</span><span class="sxs-lookup"><span data-stu-id="56cda-257">e.</span></span> <span data-ttu-id="56cda-258">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="56cda-258">Click **Next**.</span></span>
7. <span data-ttu-id="56cda-259">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire**, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="56cda-259">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD][22]
8. <span data-ttu-id="56cda-261">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="56cda-261">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD][23]
   
    <span data-ttu-id="56cda-263">a.</span><span class="sxs-lookup"><span data-stu-id="56cda-263">a.</span></span> <span data-ttu-id="56cda-264">Notez la valeur du **Nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="56cda-264">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="56cda-265">b.</span><span class="sxs-lookup"><span data-stu-id="56cda-265">b.</span></span> <span data-ttu-id="56cda-266">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="56cda-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="56cda-267">Création d’un utilisateur de test SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="56cda-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="56cda-268">Pour se connecter à SuccessFactors, les utilisateurs d’Azure AD doivent être approvisionnés dans SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="56cda-268">In order to enable Azure AD users to log into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="56cda-269">Dans le cas de SuccessFactors, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="56cda-269">In the case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="56cda-270">Pour créer des utilisateurs dans SuccessFactors, vous devez contacter [l’équipe de support technique SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="56cda-270">To get users created in SuccessFactors, you need to contact the [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="56cda-271">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="56cda-271">Assigning the Azure AD test user</span></span>
<span data-ttu-id="56cda-272">L’objectif de cette section est de permettre à Britta Simon d’utiliser l’authentification unique Azure en lui accordant l’accès à SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="56cda-272">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SuccessFactors.</span></span>

![Affecter des utilisateurs][24]

<span data-ttu-id="56cda-274">**Pour affecter Britta Simon à SuccessFactors, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="56cda-274">**To assign Britta Simon to SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="56cda-275">Pour ouvrir l’affichage des applications dans le portail Classic, dans l’affichage de l’annuaire, cliquez sur l’option **Applications** figurant dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="56cda-275">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Affecter des utilisateurs][25]
2. <span data-ttu-id="56cda-277">Dans la liste des applications, sélectionnez **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="56cda-277">In the applications list, select **SuccessFactors**.</span></span>
   
    ![Configurer l’authentification unique][26]
3. <span data-ttu-id="56cda-279">Dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="56cda-279">In the menu on the top, click **Users**.</span></span>
   
    ![Affecter des utilisateurs][27]
4. <span data-ttu-id="56cda-281">Dans la liste Utilisateurs, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="56cda-281">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="56cda-282">Dans la barre d’outils située en bas, cliquez sur **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="56cda-282">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Affecter des utilisateurs][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="56cda-284">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="56cda-284">Testing single sign-on</span></span>
<span data-ttu-id="56cda-285">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="56cda-285">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="56cda-286">Lorsque vous cliquez sur la mosaïque SuccessFactors dans le volet d’accès, vous devez être connecté automatiquement à votre application SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="56cda-286">When you click the SuccessFactors tile in the Access Panel, you should get automatically signed-on to your SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="56cda-287">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="56cda-287">Additional resources</span></span>
* [<span data-ttu-id="56cda-288">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="56cda-288">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56cda-289">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="56cda-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
