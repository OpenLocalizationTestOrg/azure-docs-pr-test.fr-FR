---
title: "Didacticiel : Intégration d’Azure Active Directory avec Wizergos Productivity Software | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et les logiciels de productivité Wizergos."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a><span data-ttu-id="25ee9-103">Didacticiel : Intégration d’Azure Active Directory avec Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="25ee9-103">Tutorial: Azure Active Directory integration with Wizergos Productivity Software</span></span>
<span data-ttu-id="25ee9-104">objectif Hello de ce didacticiel est tooshow vous comment toointegrate Wizergos des logiciels de productivité avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="25ee9-104">hello objective of this tutorial is tooshow you how toointegrate Wizergos Productivity Software  with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="25ee9-105">Intégration des logiciels de productivité Wizergos à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="25ee9-105">Integrating Wizergos Productivity Software with Azure AD provides you with hello following benefits:</span></span>

* <span data-ttu-id="25ee9-106">Vous pouvez contrôler dans Azure AD qui a accès tooWizergos logiciels de productivité</span><span class="sxs-lookup"><span data-stu-id="25ee9-106">You can control in Azure AD who has access tooWizergos Productivity Software</span></span>
* <span data-ttu-id="25ee9-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWizergos logiciels de productivité-session unique (SSO) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="25ee9-107">You can enable your users tooautomatically get signed-on tooWizergos Productivity Software single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="25ee9-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="25ee9-108">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="25ee9-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="25ee9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25ee9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="25ee9-110">Prerequisites</span></span>
<span data-ttu-id="25ee9-111">tooconfigure intégration d’Azure AD avec des logiciels de productivité Wizergos, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="25ee9-111">tooconfigure Azure AD integration with Wizergos Productivity Software, you need hello following items:</span></span>

* <span data-ttu-id="25ee9-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="25ee9-112">An Azure AD subscription</span></span>
* <span data-ttu-id="25ee9-113">Un abonnement Wizergos Productivity Software pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="25ee9-113">A Wizergos Productivity Software SSO enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="25ee9-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="25ee9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="25ee9-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="25ee9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="25ee9-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="25ee9-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="25ee9-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="25ee9-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="25ee9-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="25ee9-118">Scenario description</span></span>
<span data-ttu-id="25ee9-119">objectif Hello de ce didacticiel est tooenable vous tootest Azure AD SSO dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="25ee9-119">hello objective of this tutorial is tooenable you tootest Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="25ee9-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="25ee9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="25ee9-121">Ajout d’un logiciel de productivité Wizergos à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="25ee9-121">Adding Wizergos Productivity Software from hello gallery</span></span>
2. <span data-ttu-id="25ee9-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="25ee9-122">Configuring and testing Azure AD SSO</span></span>

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a><span data-ttu-id="25ee9-123">Ajout d’un logiciel de productivité Wizergos à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="25ee9-123">Adding Wizergos Productivity Software from hello gallery</span></span>
<span data-ttu-id="25ee9-124">intégration de hello tooconfigure Wizergos de logiciels de productivité dans Azure AD, vous devez tooadd Wizergos la productivité des logiciels à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="25ee9-124">tooconfigure hello integration of Wizergos Productivity Software into Azure AD, you need tooadd Wizergos Productivity Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="25ee9-125">**tooadd Wizergos des logiciels de productivité à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="25ee9-125">**tooadd Wizergos Productivity Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="25ee9-126">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-126">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Active Directory][1]
2. <span data-ttu-id="25ee9-128">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="25ee9-128">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="25ee9-129">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="25ee9-129">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Applications][2]
4. <span data-ttu-id="25ee9-131">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="25ee9-131">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Applications][3]
5. <span data-ttu-id="25ee9-133">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-133">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    ![Applications][4]
6. <span data-ttu-id="25ee9-135">Dans la zone de recherche de hello, tapez **Wizergos productivité logiciel**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-135">In hello search box, type **Wizergos Productivity Software**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. <span data-ttu-id="25ee9-137">Dans le volet de résultats hello, sélectionnez **logiciels de productivité Wizergos**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="25ee9-137">In hello results panel, select **Wizergos Productivity Software**, and then click **Complete** tooadd hello application.</span></span>
   
    ![Sélection d’application hello dans la galerie de hello](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a><span data-ttu-id="25ee9-139">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="25ee9-139">Configure and test Azure AD SSO</span></span>
<span data-ttu-id="25ee9-140">objectif Hello de cette section est tooshow comment tooconfigure et tester l’authentification unique d’Azure AD avec des logiciels de productivité Wizergos en fonction d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="25ee9-140">hello objective of this section is tooshow you how tooconfigure and test Azure AD SSO with Wizergos Productivity Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="25ee9-141">Pour l’authentification unique toowork, Azure AD doit tooknow quel utilisateur équivalent hello Wizergos productivité tooan utilisateur dans Azure AD est.</span><span class="sxs-lookup"><span data-stu-id="25ee9-141">For SSO toowork, Azure AD needs tooknow what hello counterpart user in Wizergos Productivity Software tooan user in Azure AD is.</span></span> <span data-ttu-id="25ee9-142">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le logiciel de productivité Wizergos hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="25ee9-142">In other words, a link relationship between an Azure AD user and hello related user in Wizergos Productivity Software needs toobe established.</span></span>

<span data-ttu-id="25ee9-143">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** Wizergos productivité logiciel.</span><span class="sxs-lookup"><span data-stu-id="25ee9-143">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Wizergos Productivity Software.</span></span>

<span data-ttu-id="25ee9-144">tooconfigure et test Azure AD l’authentification unique avec BynWizergos productivité Softwareder, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="25ee9-144">tooconfigure and test Azure AD single sign-on with BynWizergos Productivity Softwareder, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="25ee9-145">**[Configuration d’Azure AD l’authentification unique sur](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="25ee9-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="25ee9-146">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25ee9-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="25ee9-147">**[Création d’un utilisateur de test de logiciels de productivité Wizergos](#creating-a-wizergos-productivity-software-test-user)**  -toohave de Britta Simon Wizergos productivité logiciel qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="25ee9-147">**[Creating a Wizergos Productivity Software test user](#creating-a-wizergos-productivity-software-test-user)** - toohave a counterpart of Britta Simon in Wizergos Productivity Software that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="25ee9-148">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="25ee9-148">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="25ee9-149">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="25ee9-149">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="25ee9-150">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="25ee9-150">Configuring Azure AD SSO</span></span>
<span data-ttu-id="25ee9-151">Dans cette section, vous activez Azure AD l’authentification unique dans le portail classique de hello et configurez l’authentification unique dans votre application Wizergos productivité.</span><span class="sxs-lookup"><span data-stu-id="25ee9-151">In this section, you enable Azure AD single sign-on in hello classic portal and configure single sign-on in your Wizergos Productivity Software application.</span></span>

<span data-ttu-id="25ee9-152">**tooconfigure Azure AD l’authentification unique avec le logiciel de productivité Wizergos, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="25ee9-152">**tooconfigure Azure AD single sign-on with Wizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="25ee9-153">Dans le portail classique hello, sur hello **logiciels de productivité Wizergos** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur**boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="25ee9-153">In hello classic portal, on hello **Wizergos Productivity Software** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configurer l’authentification unique][6] 
2. <span data-ttu-id="25ee9-155">Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooWizergos logiciels de productivité** page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**:</span><span class="sxs-lookup"><span data-stu-id="25ee9-155">On hello **How would you like users toosign on tooWizergos Productivity Software** page, select **Azure AD Single Sign-On**, and then click **Next**:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. <span data-ttu-id="25ee9-157">Sur hello **configurer les paramètres de l’application** page de boîte de dialogue, cliquez sur **suivant**:</span><span class="sxs-lookup"><span data-stu-id="25ee9-157">On hello **Configure App Settings** dialog page, click **Next**:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. <span data-ttu-id="25ee9-159">Sur hello **configurer l’authentification unique au niveau des logiciels de productivité Wizergos** , cliquez sur **télécharger le certificat**, puis enregistrez le fichier hello sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="25ee9-159">On hello **Configure single sign-on at Wizergos Productivity Software** page, click **Download certificate**, and then save hello file on your computer:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. <span data-ttu-id="25ee9-161">Dans une fenêtre de navigateur web, client de logiciels de productivité Wizergos tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="25ee9-161">In a different web browser window, sign-on tooyour Wizergos Productivity Software tenant as an administrator.</span></span>
6. <span data-ttu-id="25ee9-162">Dans le menu de hamburger hello, sélectionnez **Admin**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-162">From hello hamburger menu, select **Admin**.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. <span data-ttu-id="25ee9-164">Dans le menu de gauche de la page Admin (Administrateur), sélectionnez **AUTHENTICATION** (AUTHENTIFICATION), puis cliquez sur **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-164">In Admin page on left hand menu select **AUTHENTICATION** and click on **Azure AD**.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. <span data-ttu-id="25ee9-166">Effectuer hello comme suit **authentification** section.</span><span class="sxs-lookup"><span data-stu-id="25ee9-166">Perform hello following steps on **AUTHENTICATION** section.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. <span data-ttu-id="25ee9-168">Cliquez sur **télécharger** hello tooupload de bouton téléchargé un certificat auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25ee9-168">Click **UPLOAD** button tooupload hello downloaded certificate from Azure AD.</span></span> 
  2. <span data-ttu-id="25ee9-169">Bonjour **URL de l’émetteur** zone de texte placer la valeur hello **URL de l’émetteur** à partir de l’Assistant configuration d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25ee9-169">In hello **Issuer URL** textbox put hello value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
  3. <span data-ttu-id="25ee9-170">Bonjour **URL de connexion unique** zone de texte placer la valeur hello **-Service URL d’authentification** à partir de l’Assistant configuration d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25ee9-170">In hello **Single Sign-On URL** textbox put hello value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
  4. <span data-ttu-id="25ee9-171">Bonjour **URL de déconnexion unique** zone de texte placer la valeur hello **URL de Service de déconnexion unique** à partir de l’Assistant configuration d’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25ee9-171">In hello **Single Sign-Out URL** textbox put hello value of **Single Sign-out Service URL** from Azure AD application configuration wizard.</span></span>
  5. <span data-ttu-id="25ee9-172">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="25ee9-172">Click **Save** button.</span></span>
9. <span data-ttu-id="25ee9-173">Dans le portail classique hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-173">In hello classic portal, select hello single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Authentification unique Azure AD][10]
10. <span data-ttu-id="25ee9-175">Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-175">On hello **Single sign-on confirmation** page, click **Complete**.</span></span>  
    
    ![Authentification unique Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="25ee9-177">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="25ee9-177">Create an Azure AD test user</span></span>
<span data-ttu-id="25ee9-178">objectif Hello de cette section est toocreate un utilisateur de test dans le portail classique de hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="25ee9-178">hello objective of this section is toocreate a test user in hello classic portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][20]

<span data-ttu-id="25ee9-180">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="25ee9-180">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="25ee9-181">Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-181">In hello **Azure classic Portal**, on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="25ee9-183">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="25ee9-183">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="25ee9-184">liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-184">toodisplay hello list of users, in hello menu on hello top, click **Users**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="25ee9-186">tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-186">tooopen hello **Add User** dialog, in hello toolbar on hello bottom, click **Add User**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="25ee9-188">Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="25ee9-188">On hello **Tell us about this user** dialog page, perform hello following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="25ee9-190">Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="25ee9-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="25ee9-191">Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-191">In hello User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="25ee9-192">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-192">Click **Next**.</span></span>
6. <span data-ttu-id="25ee9-193">Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="25ee9-193">On hello **User Profile** dialog page, perform hello following steps:</span></span>
   
   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="25ee9-195">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-195">In hello **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="25ee9-196">Bonjour **nom** zone de texte, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-196">In hello **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="25ee9-197">Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-197">In hello **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="25ee9-198">Bonjour **rôle** liste, sélectionnez **utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-198">In hello **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="25ee9-199">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-199">Click **Next**.</span></span>
7. <span data-ttu-id="25ee9-200">Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-200">On hello **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="25ee9-202">Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="25ee9-202">On hello **Get temporary password** dialog page, perform hello following steps:</span></span>
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. <span data-ttu-id="25ee9-204">Notez la valeur hello hello **nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-204">Write down hello value of hello **New Password**.</span></span>
  2. <span data-ttu-id="25ee9-205">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-205">Click **Complete**.</span></span>   

### <a name="create-a-wizergos-productivity-software-test-user"></a><span data-ttu-id="25ee9-206">Créer un utilisateur de test Wizergos Productivity Software</span><span class="sxs-lookup"><span data-stu-id="25ee9-206">Create a Wizergos Productivity Software test user</span></span>
<span data-ttu-id="25ee9-207">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Wizergos Productivity Software.</span><span class="sxs-lookup"><span data-stu-id="25ee9-207">In this section, you create a user called Britta Simon in Wizergos Productivity Software.</span></span> <span data-ttu-id="25ee9-208">Collaborez avec l’équipe de support des logiciels de productivité Wizergos via [ support@wizergos.com ](emailTo:support@wizergos.com) tooadd les utilisateurs de hello dans la plateforme de logiciels de productivité Wizergos hello.</span><span class="sxs-lookup"><span data-stu-id="25ee9-208">Please work with Wizergos Productivity Software support team via [support@wizergos.com](emailTo:support@wizergos.com) tooadd hello users in hello Wizergos Productivity Software platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="25ee9-209">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="25ee9-209">Assign hello Azure AD test user</span></span>
<span data-ttu-id="25ee9-210">objectif Hello de cette section est tooenabling Britta Simon toouse Azure SSO en accordant son tooWizergos accès aux logiciels de productivité.</span><span class="sxs-lookup"><span data-stu-id="25ee9-210">hello objective of this section is tooenabling Britta Simon toouse Azure SSO by granting her access tooWizergos Productivity Software.</span></span>

  ![Affecter des utilisateurs][200]

<span data-ttu-id="25ee9-212">**tooassign Britta Simon tooWizergos logiciels de productivité, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="25ee9-212">**tooassign Britta Simon tooWizergos Productivity Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="25ee9-213">Sur le portail classique hello, cliquez sur la vue applications hello tooopen, dans la vue active de hello, **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="25ee9-213">On hello classic portal, tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    ![Affecter des utilisateurs][201]
2. <span data-ttu-id="25ee9-215">Dans la liste des applications hello, sélectionnez **Wizergos productivité logiciel**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-215">In hello applications list, select **Wizergos Productivity Software**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. <span data-ttu-id="25ee9-217">Dans le menu hello haut de hello, cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-217">In hello menu on hello top, click **Users**.</span></span>
   
    ![Affecter des utilisateurs][203]
4. <span data-ttu-id="25ee9-219">Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-219">In hello Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="25ee9-220">Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.</span><span class="sxs-lookup"><span data-stu-id="25ee9-220">In hello toolbar on hello bottom, click **Assign**.</span></span>
   
    ![Affecter des utilisateurs][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="25ee9-222">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="25ee9-222">Test single sign-on</span></span>
<span data-ttu-id="25ee9-223">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="25ee9-223">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="25ee9-224">Lorsque vous cliquez sur mosaïque de logiciels de productivité Wizergos hello Bonjour volet d’accès, vous devez obtenir l’application de logiciels de productivité Wizergos automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="25ee9-224">When you click hello Wizergos Productivity Software tile in hello Access Panel, you should get automatically signed-on tooyour Wizergos Productivity Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="25ee9-225">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="25ee9-225">Additional resources</span></span>
* [<span data-ttu-id="25ee9-226">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25ee9-226">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="25ee9-227">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="25ee9-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
