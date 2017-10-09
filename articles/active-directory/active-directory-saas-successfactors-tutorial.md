---
title: "Didacticiel : Intégration d’Azure Active Directory à SuccessFactors | Microsoft Docs"
description: "Découvrez comment toouse SuccessFactors avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
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
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="c5b9e-103">Didacticiel : Intégration d’Azure Active Directory à SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="c5b9e-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="c5b9e-104">objectif Hello de ce didacticiel est tooshow vous comment toointegrate SuccessFactors avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-104">hello objective of this tutorial is tooshow you how toointegrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c5b9e-105">Intégration de SuccessFactors à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c5b9e-105">Integrating SuccessFactors with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="c5b9e-106">Vous pouvez contrôler dans Azure AD qui a accès tooSuccessFactors</span><span class="sxs-lookup"><span data-stu-id="c5b9e-106">You can control in Azure AD who has access tooSuccessFactors</span></span>
* <span data-ttu-id="c5b9e-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSuccessFactors (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b9e-107">You can enable your users tooautomatically get signed-on tooSuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="c5b9e-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="c5b9e-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="c5b9e-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5b9e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c5b9e-110">Prerequisites</span></span>
<span data-ttu-id="c5b9e-111">tooconfigure intégration d’Azure AD avec SuccessFactors, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c5b9e-111">tooconfigure Azure AD integration with SuccessFactors, you need hello following items:</span></span>

* <span data-ttu-id="c5b9e-112">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="c5b9e-112">A valid Azure subscription</span></span>
* <span data-ttu-id="c5b9e-113">Un locataire SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="c5b9e-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="c5b9e-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="c5b9e-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="c5b9e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="c5b9e-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="c5b9e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c5b9e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c5b9e-118">Scenario description</span></span>
<span data-ttu-id="c5b9e-119">objectif Hello de ce didacticiel est tooenable vous tootest Azure AD l’authentification unique dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-119">hello objective of this tutorial is tooenable you tootest Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="c5b9e-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="c5b9e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c5b9e-121">Ajout de SuccessFactors à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c5b9e-121">Adding SuccessFactors from hello gallery</span></span>
2. <span data-ttu-id="c5b9e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b9e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-hello-gallery"></a><span data-ttu-id="c5b9e-123">Ajout de SuccessFactors à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="c5b9e-123">Adding SuccessFactors from hello gallery</span></span>
<span data-ttu-id="c5b9e-124">intégration de hello tooconfigure de SuccessFactors dans Azure AD, vous devez tooadd SuccessFactors à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-124">tooconfigure hello integration of SuccessFactors into Azure AD, you need tooadd SuccessFactors from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c5b9e-125">**tooadd SuccessFactors à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c5b9e-125">**tooadd SuccessFactors from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5b9e-126">Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-126">In hello Azure classic portal, on hello left navigation panel, click **Active Directory**.</span></span>
   
    ![Configuration de l'authentification unique][1]
2. <span data-ttu-id="c5b9e-128">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="c5b9e-129">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Configuration de l'authentification unique][2]
4. <span data-ttu-id="c5b9e-131">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="c5b9e-133">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Configuration de l'authentification unique][4]
6. <span data-ttu-id="c5b9e-135">Bonjour **zone de recherche**, type **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-135">In hello **search box**, type **SuccessFactors**.</span></span>
   
    ![Configuration de l'authentification unique][5]
7. <span data-ttu-id="c5b9e-137">Dans le volet de résultats hello, sélectionnez **SuccessFactors**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-137">In hello results panel, select **SuccessFactors**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Configuration de l'authentification unique][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c5b9e-139">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b9e-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c5b9e-140">objectif Hello de cette section est tooshow comment tooconfigure et test Azure AD l’authentification unique avec SuccessFactors en fonction d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c5b9e-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c5b9e-141">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SuccessFactors tooan l’utilisateur dans Azure AD est.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-141">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SuccessFactors tooan user in Azure AD is.</span></span> <span data-ttu-id="c5b9e-142">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans SuccessFactors doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-142">In other words, a link relationship between an Azure AD user and hello related user in SuccessFactors needs toobe established.</span></span>

<span data-ttu-id="c5b9e-143">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SuccessFactors.</span></span>

<span data-ttu-id="c5b9e-144">tooconfigure et test Azure AD l’authentification unique avec SuccessFactors, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="c5b9e-144">tooconfigure and test Azure AD single sign-on with SuccessFactors, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c5b9e-145">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c5b9e-146">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c5b9e-147">**[Création d’un utilisateur de test de SuccessFactors](#creating-a-successfactors-test-user)**  -toohave de Britta Simon dans SuccessFactors qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - toohave a counterpart of Britta Simon in SuccessFactors that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="c5b9e-148">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c5b9e-149">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-149">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c5b9e-150">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b9e-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="c5b9e-151">Dans cette section, vous activez Azure AD l’authentification unique dans le portail classique de hello et configurez l’authentification unique dans votre application SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="c5b9e-152">**tooconfigure Azure AD single sign-on avec SuccessFactors, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c5b9e-152">**tooconfigure Azure AD single sign-on with SuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5b9e-153">Bonjour portail Azure classic sur hello **SuccessFactors** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-153">In hello Azure classic portal, on hello **SuccessFactors** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    ![Configuration de l'authentification unique][7]
2. <span data-ttu-id="c5b9e-155">Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooSuccessFactors** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-155">On hello **How would you like users toosign on tooSuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configuration de l'authentification unique][8]
3. <span data-ttu-id="c5b9e-157">Sur hello **Configure App URL** page, effectuer hello comme suit, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-157">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    ![Configuration de l'authentification unique][9]
   
    <span data-ttu-id="c5b9e-159">a.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-159">a.</span></span> <span data-ttu-id="c5b9e-160">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide d’une des hello suivant des modèles :</span><span class="sxs-lookup"><span data-stu-id="c5b9e-160">In hello **Sign On URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="c5b9e-161">b.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-161">b.</span></span> <span data-ttu-id="c5b9e-162">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide d’une des hello suivant des modèles :</span><span class="sxs-lookup"><span data-stu-id="c5b9e-162">In hello **Reply URL** textbox, type a URL using one of hello following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="c5b9e-163">c.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-163">c.</span></span> <span data-ttu-id="c5b9e-164">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="c5b9e-165">Notez qu’il s’agit pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-165">Please note that these are not hello real values.</span></span> <span data-ttu-id="c5b9e-166">Vous avez tooupdate ces valeurs avec URL hello URL de connexion et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-166">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="c5b9e-167">Ces valeurs, contactez le tooget [équipe de support technique SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-167">tooget these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="c5b9e-168">Sur hello **configurer l’authentification unique sur SuccessFactors** , cliquez sur **télécharger le certificat**, puis enregistrez le fichier de certificat hello localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-168">On hello **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save hello certificate file locally on your computer.</span></span>
   
    ![Configuration de l'authentification unique][10]

2. <span data-ttu-id="c5b9e-170">Dans une autre fenêtre de navigateur web, connectez-vous à votre **portail d’administration SuccessFactors** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="c5b9e-171">Visitez **sécurité de l’Application** et native trop**l’authentification unique sur la fonctionnalité**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-171">Visit **Application Security** and native too**Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="c5b9e-172">Placer n’importe quelle valeur Bonjour **réinitialiser le jeton** et cliquez sur **enregistrer le jeton** tooenable SSO SAML.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-172">Place any value in hello **Reset Token** and click **Save Token** tooenable SAML SSO.</span></span>
   
    ![Configuration de l’authentification unique côté application][11]

    > [!NOTE] 
    > <span data-ttu-id="c5b9e-174">Cette valeur est uniquement utilisée comme hello sur commutateur marche/arrêt.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-174">This value is just used as hello on/off switch.</span></span> <span data-ttu-id="c5b9e-175">Si aucune valeur n’est enregistrée, hello SAML SSO est activé.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-175">If any value is saved, hello SAML SSO is ON.</span></span> <span data-ttu-id="c5b9e-176">Si une valeur vide est enregistrée hello SAML SSO est désactivé.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-176">If a blank value is saved hello SAML SSO is OFF.</span></span>

1. <span data-ttu-id="c5b9e-177">Capture d’écran de toobelow natif et effectuer hello suivant des actions.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-177">Native toobelow screenshot and perform hello following actions.</span></span>
   
    ![Configuration de l’authentification unique côté application][12]
   
    <span data-ttu-id="c5b9e-179">a.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-179">a.</span></span> <span data-ttu-id="c5b9e-180">Sélectionnez hello **SAML v2 SSO** case d’option</span><span class="sxs-lookup"><span data-stu-id="c5b9e-180">Select hello **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="c5b9e-181">b.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-181">b.</span></span> <span data-ttu-id="c5b9e-182">Définissez hello SAML assertion tiers Name(e.g. SAml issuer + company name).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-182">Set hello SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="c5b9e-183">c.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-183">c.</span></span> <span data-ttu-id="c5b9e-184">Bonjour **SAML émetteur** zone de texte placer la valeur hello **URL de l’émetteur** à partir de l’Assistant configuration d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-184">In hello **SAML Issuer** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="c5b9e-185">d.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-185">d.</span></span> <span data-ttu-id="c5b9e-186">Sélectionnez **Response(Customer Generated/IdP/AP)** (Réponse (générée par le client/fournisseur d’identité/point d’accès)) pour **Require Mandatory Signature** (Exiger une signature obligatoire).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="c5b9e-187">e.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-187">e.</span></span> <span data-ttu-id="c5b9e-188">Sélectionnez **Enabled** (Activé) dans le champ **Enable SAML Flag** (Activer l’indicateur SAML).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="c5b9e-189">f.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-189">f.</span></span> <span data-ttu-id="c5b9e-190">Sélectionnez **No** (Non) dans le champ **Login Request Signature(SF Generated/SP/RP)** (Signature de la demande de connexion (générée par SF/fournisseur de services/fournisseur de ressources)).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="c5b9e-191">g.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-191">g.</span></span> <span data-ttu-id="c5b9e-192">Sélectionnez **Browser/Post Profile** (Navigateur/Post-profilage) en tant que **profil SAML**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="c5b9e-193">h.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-193">h.</span></span> <span data-ttu-id="c5b9e-194">Sélectionnez **No** (Non) dans le champ **Enforce Certificate Valid Period** (Appliquer la période valide du certificat).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="c5b9e-195">i.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-195">i.</span></span> <span data-ttu-id="c5b9e-196">Copier le contenu du fichier de certificat téléchargé hello hello, puis collez-le dans hello **certificat de vérification SAML** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-196">Copy hello content of hello downloaded certificate file, and then paste it into hello **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5b9e-197">contenu du certificat Hello doit avoir des balises de certificat certificat et de fin de début.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-197">hello certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="c5b9e-198">Accédez tooSAML V2, puis exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c5b9e-198">Navigate tooSAML V2, and then perform hello following steps:</span></span>
   
    ![Configuration de l’authentification unique côté application][13]
   
    <span data-ttu-id="c5b9e-200">a.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-200">a.</span></span> <span data-ttu-id="c5b9e-201">Sélectionnez **Yes** (Oui) dans **Support SP-initiated Global Logout** (Prendre en charge la déconnexion globale initiée par le fournisseur de services).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="c5b9e-202">b.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-202">b.</span></span> <span data-ttu-id="c5b9e-203">Bonjour **Global URL de Service de déconnexion (destination LogoutRequest)** zone de texte placer la valeur hello **URL de déconnexion distante** à partir de l’Assistant configuration d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-203">In hello **Global Logout Service URL (LogoutRequest destination)** textbox put hello value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="c5b9e-204">c.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-204">c.</span></span> <span data-ttu-id="c5b9e-205">Sélectionnez **No** (Non) dans **Require sp must encrypt all NameID element** (Exiger que le fournisseur de services chiffre tous les éléments NameID).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="c5b9e-206">d.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-206">d.</span></span> <span data-ttu-id="c5b9e-207">Sélectionnez **unspecified** (non spécifié) dans **NameID Format** (Format NameID).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="c5b9e-208">e.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-208">e.</span></span> <span data-ttu-id="c5b9e-209">Sélectionnez **Yes** (Oui) dans **Enable sp initiated login (AuthnRequest)** (Activer la connexion initiée par le fournisseur de services (AuthnRequest)).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="c5b9e-210">f.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-210">f.</span></span> <span data-ttu-id="c5b9e-211">Bonjour **demande d’envoi que l’émetteur de société** zone de texte placer la valeur hello **URL de connexion distante** à partir de l’Assistant configuration d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-211">In hello **Send request as Company-Wide issuer** textbox put hello value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="c5b9e-212">Procédez comme suit si vous souhaitez que les noms d’utilisateur de connexion toomake hello respecter la casse,.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-212">Perform these steps if you want toomake hello login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="c5b9e-213">a.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-213">a.</span></span> <span data-ttu-id="c5b9e-214">Visitez **paramètres de la société**(près du bas hello).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-214">Visit **Company Settings**(near hello bottom).</span></span>
   
    <span data-ttu-id="c5b9e-215">b.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-215">b.</span></span> <span data-ttu-id="c5b9e-216">Sélectionnez la case à cocher près de **Enable Non-Case-Sensitive Username**(Activer le non-respect de la casse pour les noms d’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="c5b9e-217">c. Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-217">c.Click **Save**.</span></span>
   
    ![Configurer l’authentification unique][29]

    > [!NOTE] 
    > <span data-ttu-id="c5b9e-219">Si vous essayez tooenable, système de hello vérifie si un nom de connexion SAML en double sera créé.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-219">If you try tooenable this, hello system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="c5b9e-220">Par exemple, si le client de hello possède des noms d’utilisateur, Utilisateur1 et user1.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-220">For example if hello customer has usernames User1 and user1.</span></span> <span data-ttu-id="c5b9e-221">Si vous désactivez le respect de la casse, ces noms deviennent des doublons.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="c5b9e-222">système de Hello vous donne un message d’erreur et n’active pas la fonctionnalité de hello.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-222">hello system will give you an error message and will not enable hello feature.</span></span> <span data-ttu-id="c5b9e-223">Hello client devra toochange un des noms d’utilisateur hello afin qu’il est orthographié réellement différents.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-223">hello customer will need toochange one of hello usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="c5b9e-224">Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-224">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    ![Applications][14]
2. <span data-ttu-id="c5b9e-226">Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-226">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Applications][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c5b9e-228">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b9e-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="c5b9e-229">objectif Hello de cette section est toocreate un utilisateur de test dans le portail classique de hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-229">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][16]

<span data-ttu-id="c5b9e-231">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c5b9e-231">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5b9e-232">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-232">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD][17]
2. <span data-ttu-id="c5b9e-234">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-234">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="c5b9e-235">liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-235">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD][18]
4. <span data-ttu-id="c5b9e-237">tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-237">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD][19]
5. <span data-ttu-id="c5b9e-239">Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c5b9e-239">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD][20]
   
    <span data-ttu-id="c5b9e-241">a.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-241">a.</span></span> <span data-ttu-id="c5b9e-242">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="c5b9e-243">b.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-243">b.</span></span> <span data-ttu-id="c5b9e-244">Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-244">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="c5b9e-245">c.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-245">c.</span></span> <span data-ttu-id="c5b9e-246">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-246">Click **Next**.</span></span>
6. <span data-ttu-id="c5b9e-247">Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c5b9e-247">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD][21]
   
    <span data-ttu-id="c5b9e-249">a.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-249">a.</span></span> <span data-ttu-id="c5b9e-250">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-250">In hello **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="c5b9e-251">b.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-251">b.</span></span> <span data-ttu-id="c5b9e-252">Bonjour **nom** zone de texte, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-252">In hello **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="c5b9e-253">c.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-253">c.</span></span> <span data-ttu-id="c5b9e-254">Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-254">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="c5b9e-255">d.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-255">d.</span></span> <span data-ttu-id="c5b9e-256">Bonjour **rôle** liste, sélectionnez **utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-256">In hello **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="c5b9e-257">e.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-257">e.</span></span> <span data-ttu-id="c5b9e-258">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-258">Click **Next**.</span></span>
7. <span data-ttu-id="c5b9e-259">Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-259">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD][22]
8. <span data-ttu-id="c5b9e-261">Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c5b9e-261">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD][23]
   
    <span data-ttu-id="c5b9e-263">a.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-263">a.</span></span> <span data-ttu-id="c5b9e-264">Notez la valeur hello hello **nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-264">Write down hello value of hello **New Password**.</span></span>
   
    <span data-ttu-id="c5b9e-265">b.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-265">b.</span></span> <span data-ttu-id="c5b9e-266">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="c5b9e-267">Création d’un utilisateur de test SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="c5b9e-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="c5b9e-268">Dans l’ordre tooenable Azure AD les utilisateurs toolog à SuccessFactors, vous devez les configurer dans SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-268">In order tooenable Azure AD users toolog into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="c5b9e-269">Dans les cas de hello de SuccessFactors, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-269">In hello case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="c5b9e-270">les utilisateurs tooget créés dans SuccessFactors, vous devez toocontact hello [équipe de support technique SuccessFactors](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="c5b9e-270">tooget users created in SuccessFactors, you need toocontact hello [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c5b9e-271">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c5b9e-271">Assigning hello Azure AD test user</span></span>
<span data-ttu-id="c5b9e-272">objectif Hello de cette section est tooenabling toouse Britta Simon Azure l’authentification unique en accordant tooSuccessFactors de son accès.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-272">hello objective of this section is tooenabling Britta Simon toouse Azure single sign-on by granting her access tooSuccessFactors.</span></span>

![Affecter des utilisateurs][24]

<span data-ttu-id="c5b9e-274">**tooassign Britta Simon tooSuccessFactors, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c5b9e-274">**tooassign Britta Simon tooSuccessFactors, perform hello following steps:**</span></span>

1. <span data-ttu-id="c5b9e-275">Sur le portail classique hello, cliquez sur la vue applications hello tooopen, dans la vue active de hello, **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-275">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Affecter des utilisateurs][25]
2. <span data-ttu-id="c5b9e-277">Dans la liste des applications hello, sélectionnez **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-277">In hello applications list, select **SuccessFactors**.</span></span>
   
    ![Configurer l’authentification unique][26]
3. <span data-ttu-id="c5b9e-279">Dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-279">In hello menu on hello top, click **Users**.</span></span>
   
    ![Affecter des utilisateurs][27]
4. <span data-ttu-id="c5b9e-281">Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-281">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="c5b9e-282">Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-282">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Affecter des utilisateurs][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="c5b9e-284">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c5b9e-284">Testing single sign-on</span></span>
<span data-ttu-id="c5b9e-285">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-285">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c5b9e-286">Lorsque vous cliquez sur hello SuccessFactors vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="c5b9e-286">When you click hello SuccessFactors tile in hello Access Panel, you should get automatically signed-on tooyour SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c5b9e-287">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c5b9e-287">Additional resources</span></span>
* [<span data-ttu-id="c5b9e-288">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5b9e-288">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c5b9e-289">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c5b9e-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

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
