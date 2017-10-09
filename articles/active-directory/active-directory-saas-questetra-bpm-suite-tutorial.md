---
title: "Didacticiel : Intégration d'Azure Active Directory à Questetra BPM Suite | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Questetra BPM Suite."
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
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a><span data-ttu-id="c2883-103">Didacticiel : Intégration d'Azure Active Directory avec Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="c2883-103">Tutorial: Azure Active Directory integration with Questetra BPM Suite</span></span>
<span data-ttu-id="c2883-104">objectif Hello de ce didacticiel est tooshow vous comment toointegrate Suite de BPM Questetra avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c2883-104">hello objective of this tutorial is tooshow you how toointegrate Questetra BPM Suite with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="c2883-105">Intégration Questetra BPM Suite à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c2883-105">Integrating Questetra BPM Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="c2883-106">Vous pouvez contrôler dans Azure AD qui a accès tooQuestetra Suite BPM</span><span class="sxs-lookup"><span data-stu-id="c2883-106">You can control in Azure AD who has access tooQuestetra BPM Suite</span></span> 
* <span data-ttu-id="c2883-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooQuestetra Suite BPM (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2883-107">You can enable your users tooautomatically get signed-on tooQuestetra BPM Suite (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="c2883-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="c2883-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="c2883-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c2883-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2883-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c2883-110">Prerequisites</span></span>
<span data-ttu-id="c2883-111">tooconfigure intégration d’Azure AD avec Questetra BPM Suite, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c2883-111">tooconfigure Azure AD integration with Questetra BPM Suite, you need hello following items:</span></span>

* <span data-ttu-id="c2883-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2883-112">An Azure AD subscription</span></span>
* <span data-ttu-id="c2883-113">Un abonnement [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="c2883-113">An [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c2883-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c2883-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="c2883-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="c2883-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="c2883-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c2883-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="c2883-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c2883-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="c2883-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c2883-118">Scenario Description</span></span>
<span data-ttu-id="c2883-119">objectif Hello de ce didacticiel est tooenable vous tootest Azure AD l’authentification unique dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c2883-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="c2883-120">scénario Hello décrite dans ce didacticiel se compose de trois blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="c2883-120">hello scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="c2883-121">Ajout de Questetra BPM Suite à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c2883-121">Adding Questetra BPM Suite from hello gallery</span></span> 
2. <span data-ttu-id="c2883-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2883-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a><span data-ttu-id="c2883-123">Ajout de Questetra BPM Suite à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c2883-123">Adding Questetra BPM Suite from hello gallery</span></span>
<span data-ttu-id="c2883-124">intégration de hello tooconfigure de Questetra BPM Suite dans Azure AD, vous devez tooadd Questetra BPM Suite à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c2883-124">tooconfigure hello integration of Questetra BPM Suite into Azure AD, you need tooadd Questetra BPM Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c2883-125">**tooadd Suite BPM de Questetra à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c2883-125">**tooadd Questetra BPM Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2883-126">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c2883-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="c2883-128">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="c2883-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="c2883-129">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="c2883-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="c2883-131">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="c2883-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="c2883-133">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="c2883-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="c2883-135">Dans la zone de recherche de hello, tapez **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="c2883-135">In hello search box, type **Questetra BPM Suite**.</span></span>
   
    ![Applications][5]

7. <span data-ttu-id="c2883-137">Dans le volet de résultats hello, sélectionnez **Questetra BPM Suite**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c2883-137">In hello results pane, select **Questetra BPM Suite**, and then click **Complete** tooadd hello application.</span></span>

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c2883-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2883-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c2883-139">objectif Hello de cette section est tooshow comment tooconfigure et test Azure AD l’authentification unique avec Questetra BPM Suite en fonction d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c2883-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with Questetra BPM Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c2883-140">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello utilisateur de tooan Questetra BPM Suite dans Azure AD est.</span><span class="sxs-lookup"><span data-stu-id="c2883-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Questetra BPM Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="c2883-141">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Questetra BPM Suite doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="c2883-141">In other words, a link relationship between an Azure AD user and hello related user in Questetra BPM Suite needs toobe established.</span></span>  
<span data-ttu-id="c2883-142">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="c2883-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Questetra BPM Suite.</span></span>

<span data-ttu-id="c2883-143">tooconfigure et test Azure AD l’authentification unique avec Questetra BPM Suite, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="c2883-143">tooconfigure and test Azure AD single sign-on with Questetra BPM Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c2883-144">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c2883-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c2883-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c2883-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c2883-146">**[Création d’un utilisateur de test Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)**  -toohave de Britta Simon dans Suite BPM Questetra qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="c2883-146">**[Creating a Questetra BPM Suite test user](#creating-a-questetra-bpm-suite-test-user)** - toohave a counterpart of Britta Simon in Questetra BPM Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="c2883-147">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c2883-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c2883-148">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="c2883-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c2883-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2883-149">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="c2883-150">Hello cette section vise tooenable Azure AD l’authentification unique sur Bonjour portail Azure classic et tooconfigure l’authentification unique dans votre application Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="c2883-150">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your Questetra BPM Suite application.</span></span>

<span data-ttu-id="c2883-151">**tooconfigure Azure AD l’authentification unique avec Questetra BPM Suite, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c2883-151">**tooconfigure Azure AD single sign-on with Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2883-152">Bonjour portail Azure classic sur hello **Questetra BPM Suite** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur**  boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c2883-152">In hello Azure classic portal, on hello **Questetra BPM Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurer l’authentification unique][8]

2. <span data-ttu-id="c2883-154">Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooQuestetra Suite BPM** page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="c2883-154">On hello **How would you like users toosign on tooQuestetra BPM Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Authentification unique Azure AD][9]

3. <span data-ttu-id="c2883-156">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d'entreprise **Questetra BPM Suite** en tant qu'administrateur.</span><span class="sxs-lookup"><span data-stu-id="c2883-156">In a different web browser window, log into your **Questetra BPM Suite** company site as an administrator.</span></span>

4. <span data-ttu-id="c2883-157">Dans le menu hello haut de hello, cliquez sur **paramètres système**.</span><span class="sxs-lookup"><span data-stu-id="c2883-157">In hello menu on hello top, click **System Settings**.</span></span> 
   
    ![Authentification unique Azure AD][10]

5. <span data-ttu-id="c2883-159">tooopen hello **SingleSignOnSAML** , cliquez sur **SSO (SAML)**.</span><span class="sxs-lookup"><span data-stu-id="c2883-159">tooopen hello **SingleSignOnSAML** page, click **SSO (SAML)**.</span></span> 
   
    ![Authentification unique Azure AD][11]

6. <span data-ttu-id="c2883-161">Bonjour portail Azure classic sur hello **configurer les paramètres de l’application** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c2883-161">In hello Azure classic portal, on hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![Configurer les paramètres d’application][13]
   
    <span data-ttu-id="c2883-163">a.</span><span class="sxs-lookup"><span data-stu-id="c2883-163">a.</span></span> <span data-ttu-id="c2883-164">Vous **Questetra BPM Suite** site d’entreprise, Bonjour section d’informations SP, hello de copie **URL ACS**, puis collez-la dans hello **URL de connexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="c2883-164">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="c2883-165">b.</span><span class="sxs-lookup"><span data-stu-id="c2883-165">b.</span></span> <span data-ttu-id="c2883-166">Vous **Questetra BPM Suite** site d’entreprise, Bonjour section d’informations SP, hello de copie **ID d’entité**, puis collez-la dans hello **URL de l’émetteur** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="c2883-166">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **Entity ID**, and then paste it into hello **Issuer URL** textbox.</span></span>
   
    <span data-ttu-id="c2883-167">c.</span><span class="sxs-lookup"><span data-stu-id="c2883-167">c.</span></span> <span data-ttu-id="c2883-168">Vous **Questetra BPM Suite** site d’entreprise, Bonjour section d’informations SP, hello de copie **URL ACS**, puis collez-la dans hello **URL de réponse** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="c2883-168">On you **Questetra BPM Suite** company site, in hello SP Information section, copy hello **ACS URL**, and then paste it into hello **Reply URL** textbox.</span></span>
   
    <span data-ttu-id="c2883-169">d.</span><span class="sxs-lookup"><span data-stu-id="c2883-169">d.</span></span> <span data-ttu-id="c2883-170">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c2883-170">Click **Next**.</span></span>

7. <span data-ttu-id="c2883-171">Sur hello **configurer l’authentification unique à la Suite de BPM Questetra** , cliquez sur **télécharger le certificat**, puis enregistrez le fichier de certificat hello localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c2883-171">On hello **Configure single sign-on at Questetra BPM Suite** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Configurer l’authentification unique][14]

8. <span data-ttu-id="c2883-173">Vous **Questetra BPM Suite** site d’entreprise, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c2883-173">On you **Questetra BPM Suite** company site, perform hello following steps:</span></span> 
   
    ![Configurer l’authentification unique][15]
   
    <span data-ttu-id="c2883-175">a.</span><span class="sxs-lookup"><span data-stu-id="c2883-175">a.</span></span> <span data-ttu-id="c2883-176">Sélectionnez **Activer l'authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c2883-176">Select **Enable Single Sign-On**.</span></span>
   
    <span data-ttu-id="c2883-177">b.</span><span class="sxs-lookup"><span data-stu-id="c2883-177">b.</span></span> <span data-ttu-id="c2883-178">Sur hello portail Azure classic, copiez hello **URL de l’émetteur** valeur, puis collez-le dans hello **ID d’entité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="c2883-178">On hello Azure classic portal, copy hello **Issuer URL** value, and then paste it into hello **Entity ID** textbox.</span></span>
   
    <span data-ttu-id="c2883-179">c.</span><span class="sxs-lookup"><span data-stu-id="c2883-179">c.</span></span> <span data-ttu-id="c2883-180">Sur hello portail Azure classic, copiez hello **-Service URL d’authentification** valeur, puis collez-le dans hello **URL de la page connexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="c2883-180">On hello Azure classic portal, copy hello **Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span>
   
    <span data-ttu-id="c2883-181">d.</span><span class="sxs-lookup"><span data-stu-id="c2883-181">d.</span></span> <span data-ttu-id="c2883-182">Sur hello portail Azure classic, copiez hello **URL de Service de déconnexion unique** valeur, puis collez-le dans hello **URL de la page de déconnexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="c2883-182">On hello Azure classic portal, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>
   
    <span data-ttu-id="c2883-183">e.</span><span class="sxs-lookup"><span data-stu-id="c2883-183">e.</span></span> <span data-ttu-id="c2883-184">Bonjour **NameID format** zone de texte, type **urn : oasis : noms : tc : SAML:1.1:nameid-format : emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="c2883-184">In hello **NameID format** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="c2883-185">f.</span><span class="sxs-lookup"><span data-stu-id="c2883-185">f.</span></span> <span data-ttu-id="c2883-186">Créez un fichier encodé en base 64 à partir du certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="c2883-186">Create a base-64 encoded file from your downloaded certificate.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="c2883-187">Pour plus d’informations, consultez [comment tooconvert un fichier binaire du certificat dans un fichier texte](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="c2883-187">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

    <span data-ttu-id="c2883-188">g.</span><span class="sxs-lookup"><span data-stu-id="c2883-188">g.</span></span> <span data-ttu-id="c2883-189">Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite dans hello **certificat de Validation** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="c2883-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it into hello **Validation certificate** textbox.</span></span> 

    <span data-ttu-id="c2883-190">h.</span><span class="sxs-lookup"><span data-stu-id="c2883-190">h.</span></span> <span data-ttu-id="c2883-191">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c2883-191">Click **Save**.</span></span>

1. <span data-ttu-id="c2883-192">Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="c2883-192">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Qu’est-ce qu’Azure AD Connect ?][17]

2. <span data-ttu-id="c2883-194">Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c2883-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Qu’est-ce qu’Azure AD Connect ?][18]


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c2883-196">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2883-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="c2883-197">objectif Hello de cette section est toocreate un utilisateur de test dans le portail Azure classic appelé Britta Simon de hello.</span><span class="sxs-lookup"><span data-stu-id="c2883-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="c2883-198">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c2883-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2883-199">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c2883-199">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Créer un utilisateur de test Azure AD][100] 

2. <span data-ttu-id="c2883-201">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="c2883-201">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="c2883-202">liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c2883-202">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Créer un utilisateur de test Azure AD][101] 

4. <span data-ttu-id="c2883-204">tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="c2883-204">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Créer un utilisateur de test Azure AD][102] 

5. <span data-ttu-id="c2883-206">Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c2883-206">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Créer un utilisateur de test Azure AD][103]
   
    <span data-ttu-id="c2883-208">a.</span><span class="sxs-lookup"><span data-stu-id="c2883-208">a.</span></span> <span data-ttu-id="c2883-209">Dans **Type d’utilisateur**, sélectionnez **Nouvel utilisateur dans votre organisation**.</span><span class="sxs-lookup"><span data-stu-id="c2883-209">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="c2883-210">b.</span><span class="sxs-lookup"><span data-stu-id="c2883-210">b.</span></span> <span data-ttu-id="c2883-211">Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c2883-211">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="c2883-212">c.</span><span class="sxs-lookup"><span data-stu-id="c2883-212">c.</span></span> <span data-ttu-id="c2883-213">Cliquez sur Suivant.</span><span class="sxs-lookup"><span data-stu-id="c2883-213">Click Next.</span></span>

6. <span data-ttu-id="c2883-214">Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c2883-214">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Créer un utilisateur de test Azure AD][104] 
   
    <span data-ttu-id="c2883-216">a.</span><span class="sxs-lookup"><span data-stu-id="c2883-216">a.</span></span> <span data-ttu-id="c2883-217">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="c2883-217">In hello **First Name** textbox, type **Britta**.</span></span> 
   
    <span data-ttu-id="c2883-218">b.</span><span class="sxs-lookup"><span data-stu-id="c2883-218">b.</span></span> <span data-ttu-id="c2883-219">Bonjour **nom** zone de texte, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c2883-219">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="c2883-220">c.</span><span class="sxs-lookup"><span data-stu-id="c2883-220">c.</span></span> <span data-ttu-id="c2883-221">Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c2883-221">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="c2883-222">d.</span><span class="sxs-lookup"><span data-stu-id="c2883-222">d.</span></span> <span data-ttu-id="c2883-223">Bonjour **rôle** liste, sélectionnez **utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="c2883-223">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="c2883-224">e.</span><span class="sxs-lookup"><span data-stu-id="c2883-224">e.</span></span> <span data-ttu-id="c2883-225">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c2883-225">Click **Next**.</span></span>

7. <span data-ttu-id="c2883-226">Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="c2883-226">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Créer un utilisateur de test Azure AD][105]  

8. <span data-ttu-id="c2883-228">Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c2883-228">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Créer un utilisateur de test Azure AD][106]   
   
    <span data-ttu-id="c2883-230">a.</span><span class="sxs-lookup"><span data-stu-id="c2883-230">a.</span></span> <span data-ttu-id="c2883-231">Notez la valeur hello hello **nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c2883-231">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="c2883-232">b.</span><span class="sxs-lookup"><span data-stu-id="c2883-232">b.</span></span> <span data-ttu-id="c2883-233">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="c2883-233">Click **Complete**.</span></span>   

### <a name="creating-a-questetra-bpm-suite-test-user"></a><span data-ttu-id="c2883-234">Création d'un utilisateur de test Questetra BPM Suite</span><span class="sxs-lookup"><span data-stu-id="c2883-234">Creating a Questetra BPM Suite test user</span></span>
<span data-ttu-id="c2883-235">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Questetra BPM Suite.</span><span class="sxs-lookup"><span data-stu-id="c2883-235">hello objective of this section is toocreate a user called Britta Simon in Questetra BPM Suite.</span></span>

<span data-ttu-id="c2883-236">**toocreate un utilisateur appelé Britta Simon Questetra BPM suite effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c2883-236">**toocreate a user called Britta Simon in Questetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2883-237">Site d’entreprise Questetra BPM Suite tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c2883-237">Sign-on tooyour Questetra BPM Suite company site as an administrator.</span></span>
2. <span data-ttu-id="c2883-238">Accédez trop**paramètres système > liste de l’utilisateur > nouvel utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="c2883-238">Go too**System Settings > User List > New User**.</span></span> 
3. <span data-ttu-id="c2883-239">Dans la boîte de dialogue Nouvel utilisateur hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c2883-239">On hello New User dialog, perform hello following steps:</span></span> 
   
    ![Créer un utilisateur de test][300] 
   
    <span data-ttu-id="c2883-241">a.</span><span class="sxs-lookup"><span data-stu-id="c2883-241">a.</span></span> <span data-ttu-id="c2883-242">Bonjour **nom** zone de texte, tapez le nom d’utilisateur de Brian dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2883-242">In hello **Name** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="c2883-243">b.</span><span class="sxs-lookup"><span data-stu-id="c2883-243">b.</span></span> <span data-ttu-id="c2883-244">Bonjour **messagerie** zone de texte, tapez le nom d’utilisateur de Brian dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c2883-244">In hello **Email** textbox, type Britta's user name in Azure AD.</span></span>
   
    <span data-ttu-id="c2883-245">c.</span><span class="sxs-lookup"><span data-stu-id="c2883-245">c.</span></span> <span data-ttu-id="c2883-246">Bonjour **mot de passe** zone de texte, tapez un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="c2883-246">In hello **Password** textbox, type a password.</span></span>

4. <span data-ttu-id="c2883-247">Cliquez sur **Ajouter un nouvel utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="c2883-247">Click **Add new user**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c2883-248">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2883-248">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="c2883-249">objectif Hello de cette section est tooenabling toouse Britta Simon Azure l’authentification unique en accordant son tooQuestetra accès Suite BPM.</span><span class="sxs-lookup"><span data-stu-id="c2883-249">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooQuestetra BPM Suite.</span></span>

![Qu’est-ce qu’Azure AD Connect ?][200]

<span data-ttu-id="c2883-251">**tooassign Britta Simon tooQuestetra Suite BPM, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c2883-251">**tooassign Britta Simon tooQuestetra BPM Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2883-252">Dans hello Azure portail classique, la vue applications hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="c2883-252">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][201]
2. <span data-ttu-id="c2883-254">Dans la liste des applications hello, sélectionnez **Questetra BPM Suite**.</span><span class="sxs-lookup"><span data-stu-id="c2883-254">In hello applications list, select **Questetra BPM Suite**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][205]
3. <span data-ttu-id="c2883-256">Dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c2883-256">In hello menu on hello top, click **Users**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][202]
4. <span data-ttu-id="c2883-258">Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c2883-258">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][203]
5. <span data-ttu-id="c2883-260">Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.</span><span class="sxs-lookup"><span data-stu-id="c2883-260">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][204]

### <a name="testing-single-sign-on"></a><span data-ttu-id="c2883-262">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c2883-262">Testing Single Sign-On</span></span>
<span data-ttu-id="c2883-263">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c2883-263">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="c2883-264">Lorsque vous cliquez sur mosaïque Questetra BPM Suite hello hello volet d’accès, vous devez obtenir l’application de Questetra BPM Suite automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="c2883-264">When you click hello Questetra BPM Suite tile in hello Access Panel, you should get automatically signed-on tooyour Questetra BPM Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c2883-265">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c2883-265">Additional Resources</span></span>
* [<span data-ttu-id="c2883-266">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c2883-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c2883-267">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c2883-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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
