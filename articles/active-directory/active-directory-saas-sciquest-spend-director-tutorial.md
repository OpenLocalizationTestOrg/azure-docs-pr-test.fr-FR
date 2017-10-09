---
title: "Didacticiel : intégration d’Azure Active Directory à SciQuest Spend Director| Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et le directeur de dépenses SciQuest."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a><span data-ttu-id="9af51-103">Didacticiel : Intégration d’Azure Active Directory avec SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="9af51-103">Tutorial: Azure Active Directory integration with SciQuest Spend Director</span></span>
<span data-ttu-id="9af51-104">objectif Hello de ce didacticiel est tooshow vous comment toointegrate SciQuest dépenses directeur avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9af51-104">hello objective of this tutorial is tooshow you how toointegrate SciQuest Spend Director with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="9af51-105">Intégration du directeur de dépenses SciQuest à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9af51-105">Integrating SciQuest Spend Director with Azure AD provides you with hello following benefits:</span></span> 

* <span data-ttu-id="9af51-106">Vous pouvez contrôler dans Azure AD qui a accès tooSciQuest directeur de dépense</span><span class="sxs-lookup"><span data-stu-id="9af51-106">You can control in Azure AD who has access tooSciQuest Spend Director</span></span> 
* <span data-ttu-id="9af51-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSciQuest directeur dépense (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="9af51-107">You can enable your users tooautomatically get signed-on tooSciQuest Spend Director (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="9af51-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="9af51-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="9af51-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9af51-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9af51-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9af51-110">Prerequisites</span></span>
<span data-ttu-id="9af51-111">tooconfigure intégration d’Azure AD avec le directeur de dépenses SciQuest, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9af51-111">tooconfigure Azure AD integration with SciQuest Spend Director, you need hello following items:</span></span>

* <span data-ttu-id="9af51-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9af51-112">An Azure AD subscription</span></span>
* <span data-ttu-id="9af51-113">Un abonnement SciQuest Spend Director pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9af51-113">A SciQuest Spend Director single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9af51-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9af51-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="9af51-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="9af51-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="9af51-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9af51-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="9af51-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9af51-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="9af51-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9af51-118">Scenario Description</span></span>
<span data-ttu-id="9af51-119">objectif Hello de ce didacticiel est tooenable vous tootest Azure AD l’authentification unique dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9af51-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="9af51-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="9af51-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9af51-121">Ajout du directeur de dépenses SciQuest à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9af51-121">Adding SciQuest Spend Director from hello gallery</span></span> 
2. <span data-ttu-id="9af51-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9af51-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a><span data-ttu-id="9af51-123">Ajout du directeur de dépenses SciQuest à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="9af51-123">Adding SciQuest Spend Director from hello gallery</span></span>
<span data-ttu-id="9af51-124">intégration de hello tooconfigure du directeur de dépenses SciQuest dans Azure AD, vous devez tooadd directeur de dépenses SciQuest à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="9af51-124">tooconfigure hello integration of SciQuest Spend Director into Azure AD, you need tooadd SciQuest Spend Director from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9af51-125">**tooadd SciQuest dépenses directeur à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9af51-125">**tooadd SciQuest Spend Director from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9af51-126">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9af51-126">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]

2. <span data-ttu-id="9af51-128">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="9af51-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="9af51-129">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="9af51-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="9af51-131">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="9af51-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="9af51-133">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="9af51-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="9af51-135">Dans la zone de recherche de hello, tapez **sciQuest dépenses directeur**.</span><span class="sxs-lookup"><span data-stu-id="9af51-135">In hello search box, type **sciQuest spend director**.</span></span>
   
    ![Applications][5]

7. <span data-ttu-id="9af51-137">Dans le volet de résultats hello, sélectionnez **directeur de dépenses SciQuest**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9af51-137">In hello results pane, select **SciQuest Spend Director**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Applications][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9af51-139">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9af51-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9af51-140">objectif Hello de cette section est tooshow comment tooconfigure et test Azure AD l’authentification unique avec le directeur de dépenses SciQuest en fonction d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9af51-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SciQuest Spend Director based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9af51-141">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans directeur de dépenses SciQuest tooan l’utilisateur dans Azure AD est.</span><span class="sxs-lookup"><span data-stu-id="9af51-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SciQuest Spend Director tooan user in Azure AD is.</span></span> <span data-ttu-id="9af51-142">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le directeur de dépenses SciQuest hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="9af51-142">In other words, a link relationship between an Azure AD user and hello related user in SciQuest Spend Director needs toobe established.</span></span>  
<span data-ttu-id="9af51-143">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** directeur de dépenses SciQuest.</span><span class="sxs-lookup"><span data-stu-id="9af51-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SciQuest Spend Director.</span></span>

<span data-ttu-id="9af51-144">tooconfigure et test Azure AD l’authentification unique avec le directeur de dépenses SciQuest, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="9af51-144">tooconfigure and test Azure AD single sign-on with SciQuest Spend Director, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9af51-145">**[Configuration d’Azure AD unique Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9af51-145">**[Configuring Azure AD Single Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9af51-146">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9af51-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9af51-147">**[Création d’un utilisateur de test du directeur de dépenses SciQuest](#creating-a-halogen-software-test-user)**  -toohave de Britta Simon SciQuest dépenses directeur est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="9af51-147">**[Creating a SciQuest Spend Director test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in SciQuest Spend Director that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="9af51-148">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9af51-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9af51-149">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="9af51-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-single-sign-on"></a><span data-ttu-id="9af51-150">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9af51-150">Configuring Azure AD Single Single Sign-On</span></span>
<span data-ttu-id="9af51-151">Hello cette section vise tooenable Azure AD l’authentification unique sur Bonjour portail Azure classic et tooconfigure l’authentification unique dans votre application Directeur de dépenses SciQuest.</span><span class="sxs-lookup"><span data-stu-id="9af51-151">hello objective of this section is tooenable Azure AD single sign-on in hello Azure classic portal and tooconfigure single sign-on in your SciQuest Spend Director application.</span></span>

<span data-ttu-id="9af51-152">**tooconfigure Azure AD l’authentification unique avec le directeur de dépenses SciQuest, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9af51-152">**tooconfigure Azure AD single sign-on with SciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="9af51-153">Bonjour portail Azure classic sur hello **directeur de dépenses SciQuest** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur**boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9af51-153">In hello Azure classic portal, on hello **SciQuest Spend Director** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurer l’authentification unique][8]

2. <span data-ttu-id="9af51-155">Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooSciQuest dépense directeur** page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="9af51-155">On hello **How would you like users toosign on tooSciQuest Spend Director** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Authentification unique Azure AD][9]

3. <span data-ttu-id="9af51-157">Sur hello **configurer les paramètres de l’application** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9af51-157">On hello **Configure App Settings** dialog page, perform hello following steps:</span></span> 
   
    ![Configurer les paramètres d’application][10]
   
     <span data-ttu-id="9af51-159">a.</span><span class="sxs-lookup"><span data-stu-id="9af51-159">a.</span></span> <span data-ttu-id="9af51-160">Bonjour **URL de connexion** zone de texte, tapez l’URL utilisée par votre toosign d’utilisateurs dans l’application Directeur de dépenses SciQuest tooyour à l’aide de hello modèle : *https://.* SciQuest.com/.**</span><span class="sxs-lookup"><span data-stu-id="9af51-160">In hello **Sign On URL** textbox, type your URL used by your users toosign on tooyour SciQuest Spend Director application using hello following pattern: *https://.*sciquest.com/.**</span></span>
   
     <span data-ttu-id="9af51-161">b.</span><span class="sxs-lookup"><span data-stu-id="9af51-161">b.</span></span> <span data-ttu-id="9af51-162">Bonjour **URL de réponse** zone de texte, hello de type même valeur que vous avez tapé dans hello **URL de connexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="9af51-162">In hello **Reply URL** textbox, type hello same value you have typed into hello **Sign On URL** textbox.</span></span> 
   
     <span data-ttu-id="9af51-163">c.</span><span class="sxs-lookup"><span data-stu-id="9af51-163">c.</span></span> <span data-ttu-id="9af51-164">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="9af51-164">Click **Next**.</span></span>

4. <span data-ttu-id="9af51-165">Sur hello **configurer l’authentification unique au directeur de dépenses SciQuest** , cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier de métadonnées hello localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9af51-165">On hello **Configure single sign-on at SciQuest Spend Director** page, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][11]

5. <span data-ttu-id="9af51-167">Contactez SciQuest prise en charge tooenable cette méthode d’authentification à l’aide de métadonnées de hello ci-dessus téléchargé.</span><span class="sxs-lookup"><span data-stu-id="9af51-167">Contact SciQuest support tooenable this authentication method using hello above downloaded metadata.</span></span>

6. <span data-ttu-id="9af51-168">Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9af51-168">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span> 
   
    ![Qu’est-ce qu’Azure AD Connect ?][15]

7. <span data-ttu-id="9af51-170">Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.</span><span class="sxs-lookup"><span data-stu-id="9af51-170">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9af51-171">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9af51-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="9af51-172">objectif Hello de cette section est toocreate un utilisateur de test dans le portail Azure classic appelé Britta Simon de hello.</span><span class="sxs-lookup"><span data-stu-id="9af51-172">hello objective of this section is toocreate a test user in hello Azure classic portal called Britta Simon.</span></span>

<span data-ttu-id="9af51-173">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9af51-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9af51-174">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9af51-174">In hello **Azure classic portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][100] 

2. <span data-ttu-id="9af51-176">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="9af51-176">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="9af51-177">liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9af51-177">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][101] 

4. <span data-ttu-id="9af51-179">tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="9af51-179">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span> 
   
    ![Qu’est-ce qu’Azure AD Connect ?][102] 

5. <span data-ttu-id="9af51-181">Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9af51-181">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][103] 
   
    <span data-ttu-id="9af51-183">a.</span><span class="sxs-lookup"><span data-stu-id="9af51-183">a.</span></span> <span data-ttu-id="9af51-184">Dans **Type d’utilisateur**, sélectionnez **Nouvel utilisateur dans votre organisation**.</span><span class="sxs-lookup"><span data-stu-id="9af51-184">As **Type Of User**, select **New user in your organization**.</span></span>
   
    <span data-ttu-id="9af51-185">b.</span><span class="sxs-lookup"><span data-stu-id="9af51-185">b.</span></span> <span data-ttu-id="9af51-186">Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9af51-186">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="9af51-187">c.</span><span class="sxs-lookup"><span data-stu-id="9af51-187">c.</span></span> <span data-ttu-id="9af51-188">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="9af51-188">Click **Next**.</span></span>

6. <span data-ttu-id="9af51-189">Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9af51-189">On hello **User Profile** dialog page, perform hello following steps:</span></span> 
   
    ![Qu’est-ce qu’Azure AD Connect ?][104] 
   
    <span data-ttu-id="9af51-191">a.</span><span class="sxs-lookup"><span data-stu-id="9af51-191">a.</span></span> <span data-ttu-id="9af51-192">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="9af51-192">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="9af51-193">b.</span><span class="sxs-lookup"><span data-stu-id="9af51-193">b.</span></span> <span data-ttu-id="9af51-194">Bonjour **nom** txtbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="9af51-194">In hello **Last Name** txtbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="9af51-195">c.</span><span class="sxs-lookup"><span data-stu-id="9af51-195">c.</span></span> <span data-ttu-id="9af51-196">Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9af51-196">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="9af51-197">d.</span><span class="sxs-lookup"><span data-stu-id="9af51-197">d.</span></span> <span data-ttu-id="9af51-198">Bonjour **rôle** liste, sélectionnez **utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="9af51-198">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="9af51-199">e.</span><span class="sxs-lookup"><span data-stu-id="9af51-199">e.</span></span> <span data-ttu-id="9af51-200">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="9af51-200">Click **Next**.</span></span>

7. <span data-ttu-id="9af51-201">Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="9af51-201">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][105]  

8. <span data-ttu-id="9af51-203">Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="9af51-203">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][106]   
   
    <span data-ttu-id="9af51-205">a.</span><span class="sxs-lookup"><span data-stu-id="9af51-205">a.</span></span> <span data-ttu-id="9af51-206">Notez la valeur hello hello **nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9af51-206">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="9af51-207">b.</span><span class="sxs-lookup"><span data-stu-id="9af51-207">b.</span></span> <span data-ttu-id="9af51-208">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="9af51-208">Click **Complete**.</span></span>   

### <a name="creating-a-sciquest-spend-director-test-user"></a><span data-ttu-id="9af51-209">Création d’un utilisateur de test SciQuest Spend Director</span><span class="sxs-lookup"><span data-stu-id="9af51-209">Creating a SciQuest Spend Director test user</span></span>
<span data-ttu-id="9af51-210">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon directeur de dépenses SciQuest.</span><span class="sxs-lookup"><span data-stu-id="9af51-210">hello objective of this section is toocreate a user called Britta Simon in SciQuest Spend Director.</span></span>

<span data-ttu-id="9af51-211">Vous devez toocontact votre équipe de support du directeur de dépenses SciQuest et que vous les fournissez des détails de hello sur votre tooget de compte de test de que sa création.</span><span class="sxs-lookup"><span data-stu-id="9af51-211">You need toocontact your SciQuest Spend Director support team and provide them with hello details about your test account tooget it created.</span></span>

<span data-ttu-id="9af51-212">Sinon, vous pouvez également tirer parti de l’approvisionnement juste-à-temps, une fonctionnalité d’authentification unique prise en charge par SciQuest Spend Director.</span><span class="sxs-lookup"><span data-stu-id="9af51-212">Alternatively, you can also leverage just-in-time provisioning, a single sign-on feature that is supported by SciQuest Spend Director.</span></span>  
<span data-ttu-id="9af51-213">Si l’approvisionnement juste-à-temps est activé, SciQuest Spend Director crée les utilisateurs automatiquement, si nécessaire, lors d’une tentative d’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9af51-213">If just-in-time provisioning is enabled, users are automatically created by SciQuest Spend Director during a single sign-on attempt if they don't exist.</span></span> <span data-ttu-id="9af51-214">Cette fonctionnalité élimine la nécessité de hello toomanually créer équivalent de l’authentification unique des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9af51-214">This feature eliminates hello need toomanually create single sign-on counterpart users.</span></span>

<span data-ttu-id="9af51-215">tooget juste-à-temps de configuration activé, vous devez toocontact vous êtes directeur de dépenses SciQuest votre équipe.</span><span class="sxs-lookup"><span data-stu-id="9af51-215">tooget just-in-time provisioning enabled, you need toocontact your your SciQuest Spend Director support team.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9af51-216">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9af51-216">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="9af51-217">objectif Hello de cette section est tooenabling toouse Britta Simon Azure l’authentification unique en accordant son tooSciQuest accès directeur de dépense.</span><span class="sxs-lookup"><span data-stu-id="9af51-217">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSciQuest Spend Director.</span></span>

![Qu’est-ce qu’Azure AD Connect ?][200]

<span data-ttu-id="9af51-219">**tooassign Britta Simon tooSciQuest directeur de dépense, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9af51-219">**tooassign Britta Simon tooSciQuest Spend Director, perform hello following steps:**</span></span>

1. <span data-ttu-id="9af51-220">Dans hello Azure portail classique, la vue applications hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="9af51-220">On hello Azure classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][201]

2. <span data-ttu-id="9af51-222">Dans la liste des applications hello, sélectionnez **directeur de dépenses SciQuest**.</span><span class="sxs-lookup"><span data-stu-id="9af51-222">In hello applications list, select **SciQuest Spend Director**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][202]

3. <span data-ttu-id="9af51-224">Dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9af51-224">In hello menu on hello top, click **Users**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][203]

4. <span data-ttu-id="9af51-226">Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9af51-226">In hello Users list, select **Britta Simon**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][204]

5. <span data-ttu-id="9af51-228">Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.</span><span class="sxs-lookup"><span data-stu-id="9af51-228">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="9af51-230">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9af51-230">Testing Single Sign-On</span></span>
<span data-ttu-id="9af51-231">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="9af51-231">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="9af51-232">Lorsque vous cliquez sur mosaïque du directeur de dépenses SciQuest hello Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour directeur de dépenses SciQuest application.</span><span class="sxs-lookup"><span data-stu-id="9af51-232">When you click hello SciQuest Spend Director tile in hello Access Panel, you should get automatically signed-on tooyour SciQuest Spend Director application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9af51-233">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9af51-233">Additional Resources</span></span>
* [<span data-ttu-id="9af51-234">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9af51-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9af51-235">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9af51-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

