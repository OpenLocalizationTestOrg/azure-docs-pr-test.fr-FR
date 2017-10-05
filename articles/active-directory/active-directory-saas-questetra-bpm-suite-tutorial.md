---
title: "Didacticiel : Intégration d'Azure Active Directory à Questetra BPM Suite | Microsoft Docs"
description: "Découvrez comment configurer l'authentification unique entre Azure Active Directory et Questetra BPM Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 7ae75446c9d19ce15a82caa9604658a528ab9941
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="dc2c5-103">Didacticiel : Intégration d'Azure Active Directory avec Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="dc2c5-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="dc2c5-104">L’objectif de ce didacticiel est de vous montrer comment intégrer Questetra BPM Suite à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc2c5-104">The objective of this tutorial is to show you how to integrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="dc2c5-105">L’intégration de Questetra BPM Suite à Azure AD offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="dc2c5-105">Integrating Questetra BPM Suite with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="dc2c5-106">Dans Azure AD, vous pouvez contrôler qui a accès à Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-106">You can control in Azure AD who has access to Questetra BPM Suite</span></span> 
* <span data-ttu-id="dc2c5-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Questetra BPM Suite (via l'authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-107">You can enable your users to automatically get signed-on to Questetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="dc2c5-108">Vous pouvez gérer vos comptes à un emplacement central : le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="dc2c5-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dc2c5-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc2c5-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dc2c5-110">Prerequisites</span></span>
<span data-ttu-id="dc2c5-111">Pour configurer l'intégration d'Azure AD avec Questetra BPM Suite, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="dc2c5-111">To configure Azure AD integration with Questetra BPM Suite, you need the following items:</span></span>

* <span data-ttu-id="dc2c5-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc2c5-112">An Azure AD subscription</span></span>
* <span data-ttu-id="dc2c5-113">Un abonnement [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="dc2c5-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc2c5-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="dc2c5-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="dc2c5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="dc2c5-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="dc2c5-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc2c5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="dc2c5-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="dc2c5-118">Scenario Description</span></span>
<span data-ttu-id="dc2c5-119">Ce didacticiel vise à vous permettre de tester l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="dc2c5-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="dc2c5-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="dc2c5-121">Ajout de Questetra BPM Suite à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="dc2c5-121">Adding Questetra BPM Suite from the gallery</span></span> 
2. <span data-ttu-id="dc2c5-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc2c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-the-gallery"></a><span data-ttu-id="dc2c5-123">Ajout de Questetra BPM Suite à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="dc2c5-123">Adding Questetra BPM Suite from the gallery</span></span>
<span data-ttu-id="dc2c5-124">Pour configurer l'intégration de Questetra BPM Suite avec Azure AD, vous devez ajouter Questetra BPM Suite, disponible dans la galerie, à votre liste d'applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-124">To configure the integration of Questetra BPM Suite into Azure AD, you need to add Questetra BPM Suite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dc2c5-125">**Pour ajouter Questetra BPM Suite à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dc2c5-125">**To add Questetra BPM Suite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dc2c5-126">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="dc2c5-128">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="dc2c5-129">Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="dc2c5-131">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="dc2c5-133">Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="dc2c5-135">Dans la zone de recherche, tapez **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-135">In the search box, type **Questetra BPM Suite**.</span></span>
   
    ![Applications][5]

7. <span data-ttu-id="dc2c5-137">Dans le volet de résultats, sélectionnez **Questetra BPM Suite**, puis cliquez sur **Terminer** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-137">In the results pane, select **Questetra BPM Suite**, and then click **Complete** to add the application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dc2c5-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc2c5-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dc2c5-139">L'objectif de cette section est de vous montrer comment configurer et tester l'authentification unique Azure AD avec Questetra BPM Suite avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="dc2c5-139">The objective of this section is to show you how to configure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dc2c5-140">Pour que l'authentification unique fonctionne, Azure AD a besoin de savoir qui est l'utilisateur Questetra BPM Suite équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Questetra BPM Suite to an user in Azure AD is.</span></span> <span data-ttu-id="dc2c5-141">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur Questetra BPM Suite associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-141">In other words, a link relationship between an Azure AD user and the related user in Questetra BPM Suite needs to be established.</span></span>  
<span data-ttu-id="dc2c5-142">Pour cela, affectez la valeur de **nom d'utilisateur** dans Azure AD en tant que valeur du **nom d'utilisateur** dans Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="dc2c5-143">Pour configurer et tester l'authentification unique Azure AD avec Questetra BPM Suite, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="dc2c5-143">To configure and test Azure AD single sign-on with Questetra BPM Suite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dc2c5-144">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dc2c5-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l'authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dc2c5-146">**[Création d'un utilisateur de test Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)** pour avoir un équivalent de Britta Simon dans Questetra BPM Suite qui soit lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - to have a counterpart of Britta Simon in Questetra BPM Suite that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="dc2c5-147">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d'utiliser l'authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dc2c5-148">**[Test de l’authentification unique](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dc2c5-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc2c5-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="dc2c5-150">L’objectif de cette section est d’activer l’authentification unique Azure AD dans le portail Azure Classic et de configurer l’authentification unique dans votre application Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-150">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="dc2c5-151">**Pour configurer l'authentification unique Azure AD avec Questetra BPM Suite, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dc2c5-151">**To configure Azure AD single sign-on with Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="dc2c5-152">Dans le portail Azure Classic, dans la page d’intégration d’application **Questetra BPM Suite**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-152">In the Azure classic portal, on the **Questetra BPM Suite** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurer l’authentification unique][8]

2. <span data-ttu-id="dc2c5-154">Dans la page **Comment voulez-vous que les utilisateurs se connectent à Questetra BPM Suite ?**, sélectionnez **Authentification unique Azure AD**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-154">On the **How would you like users to sign on to Questetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Authentification unique Azure AD][9]

3. <span data-ttu-id="dc2c5-156">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d'entreprise **Questetra BPM Suite** en tant qu'administrateur.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="dc2c5-157">Dans le menu situé en haut, cliquez sur **Paramètres système**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-157">In the menu on the top, click **System Settings**.</span></span> 
   
    ![Authentification unique Azure AD][10]

5. <span data-ttu-id="dc2c5-159">Pour ouvrir la page **SingleSignOnSAML**, cliquez sur **SSO (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-159">To open the **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Authentification unique Azure AD][11]

6. <span data-ttu-id="dc2c5-161">Dans la page **Configurer les paramètres de l’application** du portail Azure Classic, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc2c5-161">In the Azure classic portal, on the **Configure App Settings** dialog page, perform the following steps:</span></span> 
   
    ![Configurer les paramètres de l’application][13]
   
    <span data-ttu-id="dc2c5-163">a.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-163">a.</span></span> <span data-ttu-id="dc2c5-164">Sur votre site d'entreprise **Questetra BPM Suite**, dans la section des informations SP, copiez **l'URL ACS** et collez-la dans la zone de texte **Sign On URL**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-164">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="dc2c5-165">b.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-165">b.</span></span> <span data-ttu-id="dc2c5-166">Sur votre site d'entreprise **Questetra BPM Suite**, dans la section des informations SP, copiez **l'ID d'entité** et collez-le dans la zone de texte **URL de l'émetteur**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-166">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **Entity ID**, and then paste it into the **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="dc2c5-167">c.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-167">c.</span></span> <span data-ttu-id="dc2c5-168">Sur votre site d'entreprise **Questetra BPM Suite**, dans la section des informations SP, copiez **l'URL ACS** et collez-la dans la zone de texte **Reply URL**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-168">On you **Questetra BPM Suite** company site, in the SP Information section, copy the **ACS URL**, and then paste it into the **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="dc2c5-169">d.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-169">d.</span></span> <span data-ttu-id="dc2c5-170">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-170">Click **Next**.</span></span>

7. <span data-ttu-id="dc2c5-171">Dans la page **Configurer l’authentification unique à Questetra BPM Suite**, cliquez sur **Télécharger le certificat**, puis enregistrez le fichier de certificat localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-171">On the **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Configurer l’authentification unique][14]

8. <span data-ttu-id="dc2c5-173">Sur votre site d’entreprise **Questetra BPM Suite** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc2c5-173">On you **Questetra BPM Suite** company site, perform the following steps:</span></span> 
   
    ![Configurer l’authentification unique][15]
   
    <span data-ttu-id="dc2c5-175">a.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-175">a.</span></span> <span data-ttu-id="dc2c5-176">Sélectionnez **Activer l'authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="dc2c5-177">b.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-177">b.</span></span> <span data-ttu-id="dc2c5-178">Dans le portail Azure Classic, copiez la valeur **URL de l’émetteur** et collez-la dans la zone de texte **Entity ID**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-178">On the Azure classic portal, copy the **Issuer URL** value, and then paste it into the **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="dc2c5-179">c.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-179">c.</span></span> <span data-ttu-id="dc2c5-180">Dans le portail Azure Classic, copiez la valeur **URL du service d’authentification unique**, puis collez-la dans la zone de texte **Sign-in page URL**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-180">On the Azure classic portal, copy the **Single Sign-On Service URL** value, and then paste it into the **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="dc2c5-181">d.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-181">d.</span></span> <span data-ttu-id="dc2c5-182">Dans le portail Azure Classic, copiez la valeur **URL du service de déconnexion unique**, puis collez-la dans la zone de texte **Sign-out page URL**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-182">On the Azure classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="dc2c5-183">e.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-183">e.</span></span> <span data-ttu-id="dc2c5-184">Dans la zone de texte **Format NameID**, entrez **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-184">In the **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="dc2c5-185">f.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-185">f.</span></span> <span data-ttu-id="dc2c5-186">Créez un fichier encodé en base 64 à partir du certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="dc2c5-187">Pour plus d'informations, consultez [Comment convertir un certificat binaire en fichier texte](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="dc2c5-187">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="dc2c5-188">g.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-188">g.</span></span> <span data-ttu-id="dc2c5-189">Ouvrez votre certificat encodé en base 64 dans le Bloc-notes, copiez son contenu dans le Presse-papiers et collez-le dans la zone de texte **Certificat de validation** .</span><span class="sxs-lookup"><span data-stu-id="dc2c5-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it into the **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="dc2c5-190">h.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-190">h.</span></span> <span data-ttu-id="dc2c5-191">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-191">Click **Save**.</span></span>

1. <span data-ttu-id="dc2c5-192">Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-192">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Qu’est-ce qu’Azure AD Connect ?][17]

2. <span data-ttu-id="dc2c5-194">Sur la page **Confirmation de l’authentification unique**, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-194">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Qu’est-ce qu’Azure AD Connect ?][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dc2c5-196">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc2c5-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="dc2c5-197">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-197">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="dc2c5-198">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dc2c5-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dc2c5-199">Dans le volet de navigation gauche du **portail Azure Classic**, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-199">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Créer un utilisateur de test Azure AD][100] 

2. <span data-ttu-id="dc2c5-201">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-201">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="dc2c5-202">Pour afficher la liste des utilisateurs, dans le menu du haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-202">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Créer un utilisateur de test Azure AD][101] 

4. <span data-ttu-id="dc2c5-204">Pour ouvrir la boîte de dialogue **Ajouter un utilisateur**, cliquez sur l’option **Ajouter un utilisateur** figurant dans la barre d’outils du bas.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-204">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Créer un utilisateur de test Azure AD][102] 

5. <span data-ttu-id="dc2c5-206">Sur la page de boîte de dialogue **Dites-nous en plus sur cet utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc2c5-206">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Créer un utilisateur de test Azure AD][103]
   
    <span data-ttu-id="dc2c5-208">a.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-208">a.</span></span> <span data-ttu-id="dc2c5-209">Dans **Type d’utilisateur**, sélectionnez **Nouvel utilisateur dans votre organisation**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="dc2c5-210">b.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-210">b.</span></span> <span data-ttu-id="dc2c5-211">Dans la zone de texte **Nom d’utilisateur**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-211">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="dc2c5-212">c.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-212">c.</span></span> <span data-ttu-id="dc2c5-213">Cliquez sur Suivant.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-213">Click Next.</span></span>

6. <span data-ttu-id="dc2c5-214">Sur la page **Profil utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc2c5-214">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Créer un utilisateur de test Azure AD][104] 
   
    <span data-ttu-id="dc2c5-216">a.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-216">a.</span></span> <span data-ttu-id="dc2c5-217">Dans la zone de texte **First Name**, tapez **Britta**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-217">In the **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="dc2c5-218">b.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-218">b.</span></span> <span data-ttu-id="dc2c5-219">Dans la zone de texte **Last Name**, tapez **Simon**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-219">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="dc2c5-220">c.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-220">c.</span></span> <span data-ttu-id="dc2c5-221">Dans la zone de texte **Nom d’affichage**, entrez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-221">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="dc2c5-222">d.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-222">d.</span></span> <span data-ttu-id="dc2c5-223">Dans la liste **Rôle**, sélectionnez **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-223">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="dc2c5-224">e.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-224">e.</span></span> <span data-ttu-id="dc2c5-225">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-225">Click **Next**.</span></span>

7. <span data-ttu-id="dc2c5-226">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire**, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-226">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Créer un utilisateur de test Azure AD][105]  

8. <span data-ttu-id="dc2c5-228">Sur la page de boîte de dialogue **Obtenir un mot de passe temporaire** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc2c5-228">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Créer un utilisateur de test Azure AD][106]   
   
    <span data-ttu-id="dc2c5-230">a.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-230">a.</span></span> <span data-ttu-id="dc2c5-231">Notez la valeur du **Nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-231">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="dc2c5-232">b.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-232">b.</span></span> <span data-ttu-id="dc2c5-233">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="dc2c5-234">Création d'un utilisateur de test Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="dc2c5-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="dc2c5-235">L'objectif de cette section est de créer un utilisateur appelé Britta Simon dans Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-235">The objective of this section is to create a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="dc2c5-236">**Pour créer un utilisateur appelé Britta Simon dans Questetra BPM Suite, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dc2c5-236">**To create a user called Britta Simon in Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="dc2c5-237">Connectez-vous à votre site d'entreprise Questetra BPM Suite en tant qu'administrateur.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-237">Sign-on to your Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="dc2c5-238">Accédez à **Paramètres système > Liste des utilisateurs > Nouvel utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-238">Go to **System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="dc2c5-239">Dans la boîte de dialogue Nouvel utilisateur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc2c5-239">On the New User dialog, perform the following steps:</span></span> 
   
    ![Créer un utilisateur de test][300] 
   
    <span data-ttu-id="dc2c5-241">a.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-241">a.</span></span> <span data-ttu-id="dc2c5-242">Dans la zone de texte **Nom** , entrez le nom d'utilisateur de Britta dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-242">In the **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="dc2c5-243">b.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-243">b.</span></span> <span data-ttu-id="dc2c5-244">Dans la zone de texte **Adresse de messagerie** , entrez le nom d'utilisateur de Britta dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-244">In the **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="dc2c5-245">c.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-245">c.</span></span> <span data-ttu-id="dc2c5-246">Dans la zone de texte **Mot de passe** , entrez un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-246">In the **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="dc2c5-247">Cliquez sur **Ajouter un nouvel utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-247">Click **Add new user**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dc2c5-248">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc2c5-248">Assigning the Azure AD test user</span></span>
<span data-ttu-id="dc2c5-249">L’objectif de cette section est de permettre à Britta Simon d’utiliser l’authentification unique Azure en lui accordant l’accès à Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-249">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Questetra BPM Suite.</span></span>

![Qu’est-ce qu’Azure AD Connect ?][200]

<span data-ttu-id="dc2c5-251">**Pour attribuer Britta Simon à Questetra BPM Suite, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dc2c5-251">**To assign Britta Simon to Questetra BPM Suite, perform the following steps:**</span></span>

1. <span data-ttu-id="dc2c5-252">Pour ouvrir la vue des applications dans le portail Azure Classic, cliquez dans la vue de répertoire sur **Applications** dans le menu du haut.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-252">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][201]
2. <span data-ttu-id="dc2c5-254">Dans la liste des applications, sélectionnez **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-254">In the applications list, select **Questetra BPM Suite**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][205]
3. <span data-ttu-id="dc2c5-256">Dans le menu situé en haut, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-256">In the menu on the top, click **Users**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][202]
4. <span data-ttu-id="dc2c5-258">Dans la liste Utilisateurs, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-258">In the Users list, select **Britta Simon**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][203]
5. <span data-ttu-id="dc2c5-260">Dans la barre d’outils située en bas, cliquez sur **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-260">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="dc2c5-262">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="dc2c5-262">Testing Single Sign-On</span></span>
<span data-ttu-id="dc2c5-263">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-263">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="dc2c5-264">Lorsque vous cliquez sur la vignette Questetra BPM Suite dans le volet d'accès, vous devez être connecté automatiquement à votre application Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="dc2c5-264">When you click the Questetra BPM Suite tile in the Access Panel, you should get automatically signed-on to your Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dc2c5-265">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="dc2c5-265">Additional Resources</span></span>
* [<span data-ttu-id="dc2c5-266">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc2c5-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dc2c5-267">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="dc2c5-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
