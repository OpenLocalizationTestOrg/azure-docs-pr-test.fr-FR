---
title: "Didacticiel : Intégration d’Azure Active Directory à SilkRoad Life Suite | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et SilkRoad vie Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a><span data-ttu-id="29d2c-103">Didacticiel : Intégration d’Azure Active Directory à SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="29d2c-103">Tutorial: Azure Active Directory integration with SilkRoad Life Suite</span></span>
<span data-ttu-id="29d2c-104">objectif Hello de ce didacticiel est tooshow vous comment toointegrate Suite de durée de vie SilkRoad avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="29d2c-104">hello objective of this tutorial is tooshow you how toointegrate SilkRoad Life Suite with Azure Active Directory (Azure AD).</span></span> 

<span data-ttu-id="29d2c-105">Intégration SilkRoad vie Suite à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="29d2c-105">Integrating SilkRoad Life Suite with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="29d2c-106">Vous pouvez contrôler dans Azure AD qui a accès tooSilkRoad Suite de la durée de vie</span><span class="sxs-lookup"><span data-stu-id="29d2c-106">You can control in Azure AD who has access tooSilkRoad Life Suite</span></span> 
* <span data-ttu-id="29d2c-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSilkRoad vie Suite-session unique (SSO) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="29d2c-107">You can enable your users tooautomatically get signed-on tooSilkRoad Life Suite single sign-on (SSO) with their Azure AD accounts</span></span>

<span data-ttu-id="29d2c-108">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29d2c-108">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29d2c-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="29d2c-109">Prerequisites</span></span>
<span data-ttu-id="29d2c-110">tooconfigure intégration d’Azure AD avec SilkRoad vie Suite, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="29d2c-110">tooconfigure Azure AD integration with SilkRoad Life Suite, you need hello following items:</span></span>

* <span data-ttu-id="29d2c-111">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="29d2c-111">An Azure AD subscription</span></span>
* <span data-ttu-id="29d2c-112">Un abonnement SilkRoad Life Suite pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="29d2c-112">A SilkRoad Life Suite SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="29d2c-113">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="29d2c-113">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="29d2c-114">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="29d2c-114">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="29d2c-115">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="29d2c-115">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="29d2c-116">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29d2c-116">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="29d2c-117">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="29d2c-117">Scenario Description</span></span>
<span data-ttu-id="29d2c-118">objectif Hello de ce didacticiel est tooenable vous tootest Azure AD SSO dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="29d2c-118">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="29d2c-119">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="29d2c-119">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29d2c-120">Ajout de SilkRoad vie Suite à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="29d2c-120">Adding SilkRoad Life Suite from hello gallery</span></span> 
2. <span data-ttu-id="29d2c-121">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="29d2c-121">Configuring and testing Azure AD SSO</span></span>

## <a name="add-silkroad-life-suite-from-hello-gallery"></a><span data-ttu-id="29d2c-122">Ajouter SilkRoad vie Suite à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="29d2c-122">Add SilkRoad Life Suite from hello gallery</span></span>
<span data-ttu-id="29d2c-123">tooconfigure hello intégration de la Suite de durée de vie SilkRoad dans Azure AD, vous devez tooadd SilkRoad vie Suite à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="29d2c-123">tooconfigure hello integration of SilkRoad Life Suite into Azure AD, you need tooadd SilkRoad Life Suite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="29d2c-124">**tooadd SilkRoad Suite de durée de vie à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29d2c-124">**tooadd SilkRoad Life Suite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="29d2c-125">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-125">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="29d2c-127">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="29d2c-127">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="29d2c-128">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="29d2c-128">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="29d2c-130">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="29d2c-130">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="29d2c-132">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-132">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="29d2c-134">Dans la zone de recherche de hello, tapez **SilkRoad vie Suite**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-134">In hello search box, type **SilkRoad Life Suite**.</span></span>
   
    ![Applications][5]

7. <span data-ttu-id="29d2c-136">Dans le volet de résultats hello, sélectionnez **SilkRoad vie Suite**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="29d2c-136">In hello results pane, select **SilkRoad Life Suite**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Applications][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="29d2c-138">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="29d2c-138">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="29d2c-139">objectif Hello de cette section est tooshow comment tooconfigure et l’authentification unique d’Azure AD avec SilkRoad vie Suite de tests en fonction d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="29d2c-139">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with SilkRoad Life Suite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="29d2c-140">Pour l’authentification unique toowork, Azure AD doit tooknow quel utilisateur d’équivalent hello utilisateur de tooan SilkRoad vie Suite dans Azure AD est.</span><span class="sxs-lookup"><span data-stu-id="29d2c-140">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SilkRoad Life Suite tooan user in Azure AD is.</span></span> <span data-ttu-id="29d2c-141">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans la Suite de durée de vie SilkRoad hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="29d2c-141">In other words, a link relationship between an Azure AD user and hello related user in SilkRoad Life Suite needs toobe established.</span></span>

<span data-ttu-id="29d2c-142">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans SilkRoad vie Suite.</span><span class="sxs-lookup"><span data-stu-id="29d2c-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SilkRoad Life Suite.</span></span>

<span data-ttu-id="29d2c-143">tooconfigure et test Azure AD l’authentification unique avec SilkRoad vie Suite, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="29d2c-143">tooconfigure and test Azure AD single sign-on with SilkRoad Life Suite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="29d2c-144">**[Configuration d’Azure AD l’authentification unique sur](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="29d2c-144">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="29d2c-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29d2c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29d2c-146">**[Création d’un utilisateur de test SilkRoad vie Suite](#creating-a-silkroad-life-suite-test-user)**  -toohave un équivalent de Britta Simon dans la Suite de durée de vie SilkRoad de sa représentation sous forme de toohello lié Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29d2c-146">**[Creating a SilkRoad Life Suite test user](#creating-a-silkroad-life-suite-test-user)** - toohave a counterpart of Britta Simon in SilkRoad Life Suite that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="29d2c-147">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="29d2c-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29d2c-148">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="29d2c-148">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="29d2c-149">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="29d2c-149">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="29d2c-150">Hello cette section vise tooenable Azure AD SSO Bonjour portail Azure classic et tooconfigure l’authentification unique dans votre application SilkRoad vie Suite.</span><span class="sxs-lookup"><span data-stu-id="29d2c-150">hello objective of this section is tooenable Azure AD SSO in hello Azure classic portal and tooconfigure SSO in your SilkRoad Life Suite application.</span></span>

<span data-ttu-id="29d2c-151">**tooconfigure Azure AD l’authentification unique avec SilkRoad vie Suite, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29d2c-151">**tooconfigure Azure AD single sign-on with SilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="29d2c-152">Site d’entreprise SilkRoad tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="29d2c-152">Sign-on tooyour SilkRoad company site as administrator.</span></span> 

  >[!NOTE] 
  > <span data-ttu-id="29d2c-153">tooobtain accès toohello application Suite d’authentification de la durée de vie SilkRoad pour configurer la fédération avec Microsoft Azure AD, contactez votre prise en charge SilkRoad ou SilkRoad Services.</span><span class="sxs-lookup"><span data-stu-id="29d2c-153">tooobtain access toohello SilkRoad Life Suite Authentication application for configuring federation with Microsoft Azure AD, please contact SilkRoad Support or your SilkRoad Services representative.</span></span>
  > 

2. <span data-ttu-id="29d2c-154">Accédez trop**fournisseur de services**, puis cliquez sur **détails de la fédération**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-154">Go too**Service Provider**, and then click **Federation Details**.</span></span> 
   
    ![Authentification unique Azure AD][10] 

3. <span data-ttu-id="29d2c-156">Cliquez sur **télécharger les métadonnées de fédération**, puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="29d2c-156">Click **Download Federation Metadata**, and then save hello metadata file on your computer.</span></span>
   
    ![Authentification unique Azure AD][11] 

4. <span data-ttu-id="29d2c-158">Bonjour portail Azure classic sur hello **SilkRoad vie Suite** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur**  boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="29d2c-158">In hello Azure classic portal, on hello **SilkRoad Life Suite** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurer l’authentification unique][6] 

5. <span data-ttu-id="29d2c-160">Sur hello **Comment souhaitez-vous toosign les utilisateurs sur la Suite de la durée de vie de tooSilkRoad** page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-160">On hello **How would you like users toosign on tooSilkRoad Life Suite** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Authentification unique Azure AD][7] 

6. <span data-ttu-id="29d2c-162">Sur hello **configurer les paramètres de l’application** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29d2c-162">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span>
   
    ![Authentification unique Azure AD][8]   
 1. <span data-ttu-id="29d2c-164">Bonjour **URL de connexion** zone de texte, tapez l’URL hello utilisée par votre site de Suite de durée de vie de SilkRoad tooyour toosign sur les utilisateurs (par exemple : *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span><span class="sxs-lookup"><span data-stu-id="29d2c-164">In hello **Sign On URL** textbox, type hello URL used by your users toosign-on tooyour SilkRoad Life Suite site (e.g.: *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).</span></span>  
 2. <span data-ttu-id="29d2c-165">Ouvrez hello téléchargé **Silkroad** fichier de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="29d2c-165">Open hello downloaded **Silkroad** metadata file.</span></span> 
 3. <span data-ttu-id="29d2c-166">Recherchez hello **AssertionConsumerService** balise, puis hello de copie **emplacement** attribut.</span><span class="sxs-lookup"><span data-stu-id="29d2c-166">Locate hello **AssertionConsumerService** tag, and then copy hello **Location** attribute.</span></span>         
   
    ![Authentification unique Azure AD][21] 
 4. <span data-ttu-id="29d2c-168">Collez la valeur de hello hello **URL de réponse** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="29d2c-168">Paste hello value into hello **Reply URL** textbox.</span></span>  
 5. <span data-ttu-id="29d2c-169">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-169">Click **Next**.</span></span>

6. <span data-ttu-id="29d2c-170">Sur hello **configurer l’authentification unique à la Suite de durée de vie SilkRoad** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29d2c-170">On hello **Configure single sign-on at SilkRoad Life Suite** page, perform hello following steps:</span></span>
   
    ![Authentification unique Azure AD][9]  
 1. <span data-ttu-id="29d2c-172">Cliquez sur Télécharger le certificat, puis enregistrez le fichier hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="29d2c-172">Click Download certificate, and then save hello file on your computer.</span></span>  
 2. <span data-ttu-id="29d2c-173">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-173">Click **Next**.</span></span>

7. <span data-ttu-id="29d2c-174">Dans votre application **SilkRoad**, cliquez sur **Authentication Sources** (Sources d’authentification).</span><span class="sxs-lookup"><span data-stu-id="29d2c-174">In your **SilkRoad** application, click **Authentication Sources**.</span></span>
   
    ![Authentification unique Azure AD][12] 

8. <span data-ttu-id="29d2c-176">Cliquez sur **Add Authentication Source**(Ajouter une source d’authentification).</span><span class="sxs-lookup"><span data-stu-id="29d2c-176">Click **Add Authentication Source**.</span></span> 
   
    ![Authentification unique Azure AD][13] 

9. <span data-ttu-id="29d2c-178">Bonjour **ajouter une Source de l’authentification** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29d2c-178">In hello **Add Authentication Source** section, perform hello following steps:</span></span> 
   
    ![Authentification unique Azure AD][14]  
 1. <span data-ttu-id="29d2c-180">Sous **Option 2 - fichier de métadonnées**, cliquez sur **Parcourir** hello de tooupload téléchargé le fichier de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="29d2c-180">Under **Option 2 - Metadata File**, click **Browse** tooupload hello downloaded metadata file.</span></span>  
 2. <span data-ttu-id="29d2c-181">Cliquez sur **Create Identity Provider using File Data**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-181">Click **Create Identity Provider using File Data**.</span></span>

10. <span data-ttu-id="29d2c-182">Bonjour **Sources d’authentification** , cliquez sur **modifier**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-182">In hello **Authentication Sources** section, click **Edit**.</span></span> 
    
     ![Authentification unique Azure AD][15] 

11. <span data-ttu-id="29d2c-184">Sur hello **modifier la Source de l’authentification** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29d2c-184">On hello **Edit Authentication Source** dialog, perform hello following steps:</span></span> 
    
     ![Authentification unique Azure AD][16] 
 1. <span data-ttu-id="29d2c-186">Pour l’option **Enabled**, sélectionnez **Yes**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-186">As **Enabled**, select **Yes**.</span></span>   
 2. <span data-ttu-id="29d2c-187">Bonjour **IdP Description** zone de texte, tapez une description pour votre configuration (par exemple : *Azure AD SSO*).</span><span class="sxs-lookup"><span data-stu-id="29d2c-187">In hello **IdP Description** textbox, type a description for your configuration (e.g.: *Azure AD SSO*).</span></span>  
 3. <span data-ttu-id="29d2c-188">Bonjour **IdP nom** zone de texte, tapez un nom de configuration de tooyour spécifique (par exemple : *Azure SP*).</span><span class="sxs-lookup"><span data-stu-id="29d2c-188">In hello **IdP Name** textbox, type a name that is specific tooyour configuration (e.g.: *Azure SP*).</span></span>  
 4. <span data-ttu-id="29d2c-189">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-189">Click **Save**.</span></span>

12. <span data-ttu-id="29d2c-190">Désactivez toutes les autres sources d’authentification.</span><span class="sxs-lookup"><span data-stu-id="29d2c-190">Disable all other authentication sources.</span></span> 
    
     ![Authentification unique Azure AD][17]

13. <span data-ttu-id="29d2c-192">Bonjour portail Azure classic sur hello **Single sign-on confirmation** , cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-192">In hello Azure classic portal, on hello **Single sign-on confirmation** page, click **Next**.</span></span>  
    
     ![Authentification unique Azure AD][18]

14. <span data-ttu-id="29d2c-194">Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-194">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
    
     ![Authentification unique Azure AD][19]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="29d2c-196">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="29d2c-196">Create an Azure AD test user</span></span>
<span data-ttu-id="29d2c-197">objectif Hello de cette section est toocreate un utilisateur de test dans le portail Azure classic appelé Britta Simon de hello.</span><span class="sxs-lookup"><span data-stu-id="29d2c-197">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][20]

<span data-ttu-id="29d2c-199">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29d2c-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="29d2c-200">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-200">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. <span data-ttu-id="29d2c-202">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="29d2c-202">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="29d2c-203">liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-203">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="29d2c-205">tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-205">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="29d2c-207">Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29d2c-207">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span> 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. <span data-ttu-id="29d2c-209">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="29d2c-209">As Type Of User, select New user in your organization.</span></span>  
 2. <span data-ttu-id="29d2c-210">Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-210">In hello User Name **textbox**, type **BrittaSimon**.</span></span> 
 3. <span data-ttu-id="29d2c-211">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-211">Click **Next**.</span></span>

6. <span data-ttu-id="29d2c-212">Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29d2c-212">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. <span data-ttu-id="29d2c-214">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-214">In hello **First Name** textbox, type **Britta**.</span></span>    
 2. <span data-ttu-id="29d2c-215">Bonjour **nom** zone de texte, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-215">In hello **Last Name** textbox, type, **Simon**.</span></span> 
 3. <span data-ttu-id="29d2c-216">Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-216">In hello **Display Name** textbox, type **Britta Simon**.</span></span> 
 4. <span data-ttu-id="29d2c-217">Bonjour **rôle** liste, sélectionnez **utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-217">In hello **Role** list, select **User**.</span></span>
 5. <span data-ttu-id="29d2c-218">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-218">Click **Next**.</span></span>

7. <span data-ttu-id="29d2c-219">Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-219">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="29d2c-221">Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="29d2c-221">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. <span data-ttu-id="29d2c-223">Notez la valeur hello hello **nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-223">Write down hello value of hello **New Password**.</span></span> 
 2. <span data-ttu-id="29d2c-224">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-224">Click **Complete**.</span></span>   

### <a name="create-a-silkroad-life-suite-test-user"></a><span data-ttu-id="29d2c-225">Créer un utilisateur de test SilkRoad Life Suite</span><span class="sxs-lookup"><span data-stu-id="29d2c-225">Create a SilkRoad Life Suite test user</span></span>
<span data-ttu-id="29d2c-226">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans SilkRoad vie Suite.</span><span class="sxs-lookup"><span data-stu-id="29d2c-226">hello objective of this section is toocreate a user called Britta Simon in SilkRoad Life Suite.</span></span> <span data-ttu-id="29d2c-227">Brian doit avoir un ID de l’authentification unique (parfois appelée tooas un *AuthParam*) qui correspond à de Brian **emailaddress** dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29d2c-227">Britta's must have an SSO ID (sometimes referred tooas an *AuthParam*) that matches Britta's **emailaddress** in Azure AD.</span></span>

<span data-ttu-id="29d2c-228">**toocreate un utilisateur appelé Britta Simon SilkRoad vie suite effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29d2c-228">**toocreate a user called Britta Simon in SilkRoad Life Suite, perform hello following steps:**</span></span>

- <span data-ttu-id="29d2c-229">Demandez à votre toocreate équipe de support SilkRoad vie Suite à un utilisateur qui a comme **ID de l’authentification unique** hello attribut même valeur que hello **emailaddress** de Britta Simon dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29d2c-229">Ask your SilkRoad Life Suite support team toocreate a user that has as **SSO ID** attribute hello same value as hello **emailaddress** of Britta Simon in Azure AD.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="29d2c-230">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="29d2c-230">Assign hello Azure AD test user</span></span>
<span data-ttu-id="29d2c-231">objectif Hello de cette section est tooenable Britta Simon toouse Azure SSO en accordant son tooSilkRoad accès Suite de la durée de vie.</span><span class="sxs-lookup"><span data-stu-id="29d2c-231">hello objective of this section is tooenable Britta Simon toouse Azure SSO by granting her access tooSilkRoad Life Suite.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="29d2c-233">**tooassign Britta Simon tooSilkRoad Suite de la durée de vie, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="29d2c-233">**tooassign Britta Simon tooSilkRoad Life Suite, perform hello following steps:**</span></span>

1. <span data-ttu-id="29d2c-234">Dans hello Azure portail classique, la vue applications hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="29d2c-234">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="29d2c-236">Dans la liste des applications hello, sélectionnez **SilkRoad vie Suite**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-236">In hello applications list, select **SilkRoad Life Suite**.</span></span>
   
    ![Affecter des utilisateurs][202] 

3. <span data-ttu-id="29d2c-238">Dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-238">In hello menu on hello top, click **Users**.</span></span>
   
    ![Affecter des utilisateurs][203] 

4. <span data-ttu-id="29d2c-240">Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-240">In hello Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="29d2c-241">Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.</span><span class="sxs-lookup"><span data-stu-id="29d2c-241">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Affecter des utilisateurs][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="29d2c-243">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="29d2c-243">Test single sign-on</span></span>
<span data-ttu-id="29d2c-244">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="29d2c-244">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="29d2c-245">Lorsque vous cliquez sur mosaïque SilkRoad vie Suite hello hello volet d’accès, vous devez obtenir l’application de Suite de durée de vie de SilkRoad automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="29d2c-245">When you click hello SilkRoad Life Suite tile in hello Access Panel, you should get automatically signed-on tooyour SilkRoad Life Suite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="29d2c-246">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="29d2c-246">Additional Resources</span></span>
* [<span data-ttu-id="29d2c-247">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29d2c-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29d2c-248">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="29d2c-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





