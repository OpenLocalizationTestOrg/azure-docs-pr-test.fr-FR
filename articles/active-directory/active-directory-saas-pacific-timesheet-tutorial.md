---
title: "Didacticiel : Intégration d’Azure Active Directory à Pacific Timesheet | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et les feuilles de temps du Pacifique."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e546e8ba-821a-4942-9545-c84b0670beab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 5fd57ff78a3a64c135f2de9895f4643b39e33bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pacific-timesheet"></a><span data-ttu-id="e700e-103">Didacticiel : Intégration d’Azure Active Directory avec Pacific Timesheet</span><span class="sxs-lookup"><span data-stu-id="e700e-103">Tutorial: Azure Active Directory integration with Pacific Timesheet</span></span>

<span data-ttu-id="e700e-104">Dans ce didacticiel, vous apprendrez comment toointegrate Pacific la feuille de temps avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e700e-104">In this tutorial, you learn how toointegrate Pacific Timesheet with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e700e-105">Intégration de la feuille de temps Pacific à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e700e-105">Integrating Pacific Timesheet with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e700e-106">Vous pouvez contrôler dans Azure AD qui a accès tooPacific de feuille de temps</span><span class="sxs-lookup"><span data-stu-id="e700e-106">You can control in Azure AD who has access tooPacific Timesheet</span></span>
- <span data-ttu-id="e700e-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPacific de feuille de temps (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="e700e-107">You can enable your users tooautomatically get signed-on tooPacific Timesheet (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e700e-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e700e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e700e-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e700e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e700e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e700e-110">Prerequisites</span></span>

<span data-ttu-id="e700e-111">tooconfigure intégration d’Azure AD avec des feuilles de temps du Pacifique, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e700e-111">tooconfigure Azure AD integration with Pacific Timesheet, you need hello following items:</span></span>

- <span data-ttu-id="e700e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e700e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e700e-113">Un abonnement Pacific Timesheet pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="e700e-113">A Pacific Timesheet single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e700e-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e700e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e700e-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="e700e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e700e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e700e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e700e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e700e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e700e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e700e-118">Scenario description</span></span>
<span data-ttu-id="e700e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e700e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e700e-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="e700e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e700e-121">Ajout de la feuille de temps Pacific à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e700e-121">Adding Pacific Timesheet from hello gallery</span></span>
2. <span data-ttu-id="e700e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e700e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pacific-timesheet-from-hello-gallery"></a><span data-ttu-id="e700e-123">Ajout de la feuille de temps Pacific à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e700e-123">Adding Pacific Timesheet from hello gallery</span></span>
<span data-ttu-id="e700e-124">intégration de hello tooconfigure de feuille de temps Pacific dans Azure AD, vous devez tooadd Pacifique de feuille de temps à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="e700e-124">tooconfigure hello integration of Pacific Timesheet into Azure AD, you need tooadd Pacific Timesheet from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e700e-125">**tooadd Pacifique la feuille de temps à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e700e-125">**tooadd Pacific Timesheet from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e700e-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e700e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e700e-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e700e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e700e-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e700e-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="e700e-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e700e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="e700e-133">Dans la zone de recherche de hello, tapez **feuille de temps Pacific**.</span><span class="sxs-lookup"><span data-stu-id="e700e-133">In hello search box, type **Pacific Timesheet**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_search.png)

5. <span data-ttu-id="e700e-135">Dans le volet de résultats hello, sélectionnez **feuille de temps Pacific**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e700e-135">In hello results panel, select **Pacific Timesheet**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e700e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e700e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e700e-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Pacific Timesheet, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e700e-138">In this section, you configure and test Azure AD single sign-on with Pacific Timesheet based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e700e-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans la feuille de temps Pacific est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e700e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pacific Timesheet is tooa user in Azure AD.</span></span> <span data-ttu-id="e700e-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans la feuille de temps Pacific hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="e700e-140">In other words, a link relationship between an Azure AD user and hello related user in Pacific Timesheet needs toobe established.</span></span>

<span data-ttu-id="e700e-141">Dans la feuille de temps du Pacifique, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="e700e-141">In Pacific Timesheet, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e700e-142">tooconfigure et test Azure AD l’authentification unique avec des feuilles de temps du Pacifique, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="e700e-142">tooconfigure and test Azure AD single sign-on with Pacific Timesheet, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e700e-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e700e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e700e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e700e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e700e-145">**[Création d’un utilisateur de test de la feuille de temps Pacific](#creating-a-pacific-timesheet-test-user)**  -toohave un équivalent de Britta Simon dans une feuille de temps Pacifique qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e700e-145">**[Creating a Pacific Timesheet test user](#creating-a-pacific-timesheet-test-user)** - toohave a counterpart of Britta Simon in Pacific Timesheet that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e700e-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e700e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e700e-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="e700e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e700e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e700e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e700e-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de la feuille de temps du Pacifique.</span><span class="sxs-lookup"><span data-stu-id="e700e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Pacific Timesheet application.</span></span>

<span data-ttu-id="e700e-150">**tooconfigure Azure AD authentification unique avec la feuille de temps du Pacifique, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e700e-150">**tooconfigure Azure AD single sign-on with Pacific Timesheet, perform hello following steps:**</span></span>

1. <span data-ttu-id="e700e-151">Bonjour portail Azure, sur hello **feuille de temps Pacific** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e700e-151">In hello Azure portal, on hello **Pacific Timesheet** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="e700e-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e700e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_samlbase.png)

3. <span data-ttu-id="e700e-155">Sur hello **URL et le domaine de feuille de temps Pacific** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e700e-155">On hello **Pacific Timesheet Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_url.png)

    <span data-ttu-id="e700e-157">a.</span><span class="sxs-lookup"><span data-stu-id="e700e-157">a.</span></span> <span data-ttu-id="e700e-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="e700e-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    <span data-ttu-id="e700e-159">b.</span><span class="sxs-lookup"><span data-stu-id="e700e-159">b.</span></span> <span data-ttu-id="e700e-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span><span class="sxs-lookup"><span data-stu-id="e700e-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<InstanceID>.pacifictimesheet.com/timesheet/home.do`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e700e-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="e700e-161">These values are not real.</span></span> <span data-ttu-id="e700e-162">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="e700e-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="e700e-163">Contact [équipe de support technique de la feuille de temps Pacific](http://www.pacifictimesheet.com/support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="e700e-163">Contact [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) tooget these values.</span></span>
 
4. <span data-ttu-id="e700e-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e700e-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_certificate.png) 

5. <span data-ttu-id="e700e-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e700e-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e700e-168">Sur hello **Configuration de la feuille de temps Pacific** , cliquez sur **configurer la feuille de temps Pacific** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e700e-168">On hello **Pacific Timesheet Configuration** section, click **Configure Pacific Timesheet** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e700e-169">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="e700e-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_configure.png) 

7. <span data-ttu-id="e700e-171">tooconfigure l’authentification unique sur **feuille de temps Pacific** côté, vous devez hello toosend téléchargé **certificat (Base64)**, **SAML Sign-On URL du Service unique**et  **ID d’entité SAML** trop[équipe de support technique de la feuille de temps Pacific](http://www.pacifictimesheet.com/support).</span><span class="sxs-lookup"><span data-stu-id="e700e-171">tooconfigure single sign-on on **Pacific Timesheet** side, you need toosend hello downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Pacific Timesheet support team](http://www.pacifictimesheet.com/support).</span></span> <span data-ttu-id="e700e-172">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="e700e-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e700e-173">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="e700e-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e700e-174">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="e700e-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e700e-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e700e-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e700e-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e700e-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="e700e-177">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="e700e-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="e700e-179">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e700e-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e700e-180">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e700e-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e700e-182">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e700e-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e700e-184">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="e700e-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e700e-186">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e700e-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-pacific-timesheet-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e700e-188">a.</span><span class="sxs-lookup"><span data-stu-id="e700e-188">a.</span></span> <span data-ttu-id="e700e-189">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e700e-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e700e-190">b.</span><span class="sxs-lookup"><span data-stu-id="e700e-190">b.</span></span> <span data-ttu-id="e700e-191">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e700e-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e700e-192">c.</span><span class="sxs-lookup"><span data-stu-id="e700e-192">c.</span></span> <span data-ttu-id="e700e-193">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="e700e-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e700e-194">d.</span><span class="sxs-lookup"><span data-stu-id="e700e-194">d.</span></span> <span data-ttu-id="e700e-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e700e-195">Click **Create**.</span></span>
 
### <a name="creating-a-pacific-timesheet-test-user"></a><span data-ttu-id="e700e-196">Création d’un utilisateur de test Pacific Timesheet</span><span class="sxs-lookup"><span data-stu-id="e700e-196">Creating a Pacific Timesheet test user</span></span>

<span data-ttu-id="e700e-197">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Pacific Timesheet.</span><span class="sxs-lookup"><span data-stu-id="e700e-197">In this section, you create a user called Britta Simon in Pacific Timesheet.</span></span> <span data-ttu-id="e700e-198">Travailler avec [équipe de support technique de la feuille de temps Pacific](http://www.pacifictimesheet.com/support) toocreate un utilisateur dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="e700e-198">Work with [Pacific Timesheet support team](http://www.pacifictimesheet.com/support) toocreate a user in hello application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e700e-199">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e700e-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e700e-200">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPacific de feuille de temps.</span><span class="sxs-lookup"><span data-stu-id="e700e-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPacific Timesheet.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="e700e-202">**tooassign Britta Simon tooPacific feuille de temps, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e700e-202">**tooassign Britta Simon tooPacific Timesheet, perform hello following steps:**</span></span>

1. <span data-ttu-id="e700e-203">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e700e-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e700e-205">Dans la liste des applications hello, sélectionnez **feuille de temps Pacific**.</span><span class="sxs-lookup"><span data-stu-id="e700e-205">In hello applications list, select **Pacific Timesheet**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_pacifictimesheet_app.png) 

3. <span data-ttu-id="e700e-207">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e700e-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="e700e-209">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e700e-209">Click **Add** button.</span></span> <span data-ttu-id="e700e-210">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e700e-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="e700e-212">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="e700e-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e700e-213">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e700e-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e700e-214">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e700e-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e700e-215">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e700e-215">Testing single sign-on</span></span>

<span data-ttu-id="e700e-216">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="e700e-216">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e700e-217">Lorsque vous cliquez sur mosaïque de feuille de temps Pacific hello Bonjour volet d’accès, vous devez obtenir l’application de feuille de temps du Pacifique tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="e700e-217">When you click hello Pacific Timesheet tile in hello Access Panel, you should get automatically signed-on tooyour Pacific Timesheet application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e700e-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e700e-218">Additional resources</span></span>

* [<span data-ttu-id="e700e-219">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e700e-219">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e700e-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e700e-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pacific-timesheet-tutorial/tutorial_general_203.png

