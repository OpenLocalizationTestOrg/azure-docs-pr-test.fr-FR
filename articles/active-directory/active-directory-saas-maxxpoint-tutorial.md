---
title: "Didacticiel : Intégration d’Azure Active Directory à MaxxPoint | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et MaxxPoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ba026e-96fc-4ae8-b135-0169da810e99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 03b13908add8d8c62f1d1480ed2288658fce14d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-maxxpoint"></a><span data-ttu-id="505a8-103">Didacticiel : Intégration d’Azure Active Directory à MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="505a8-103">Tutorial: Azure Active Directory integration with MaxxPoint</span></span>

<span data-ttu-id="505a8-104">Dans ce didacticiel, vous apprendrez comment toointegrate MaxxPoint avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="505a8-104">In this tutorial, you learn how toointegrate MaxxPoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="505a8-105">Intégration MaxxPoint à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="505a8-105">Integrating MaxxPoint with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="505a8-106">Vous pouvez contrôler dans Azure AD qui a accès tooMaxxPoint</span><span class="sxs-lookup"><span data-stu-id="505a8-106">You can control in Azure AD who has access tooMaxxPoint</span></span>
- <span data-ttu-id="505a8-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMaxxPoint (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="505a8-107">You can enable your users tooautomatically get signed-on tooMaxxPoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="505a8-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="505a8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="505a8-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="505a8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="505a8-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="505a8-110">Prerequisites</span></span>

<span data-ttu-id="505a8-111">tooconfigure intégration d’Azure AD avec MaxxPoint, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="505a8-111">tooconfigure Azure AD integration with MaxxPoint, you need hello following items:</span></span>

- <span data-ttu-id="505a8-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="505a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="505a8-113">Un abonnement MaxxPoint pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="505a8-113">A MaxxPoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="505a8-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="505a8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="505a8-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="505a8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="505a8-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="505a8-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="505a8-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="505a8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="505a8-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="505a8-118">Scenario description</span></span>
<span data-ttu-id="505a8-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="505a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="505a8-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="505a8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="505a8-121">Ajout de MaxxPoint à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="505a8-121">Adding MaxxPoint from hello gallery</span></span>
2. <span data-ttu-id="505a8-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="505a8-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-maxxpoint-from-hello-gallery"></a><span data-ttu-id="505a8-123">Ajout de MaxxPoint à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="505a8-123">Adding MaxxPoint from hello gallery</span></span>
<span data-ttu-id="505a8-124">intégration de hello tooconfigure de MaxxPoint dans Azure AD, vous devez tooadd MaxxPoint à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="505a8-124">tooconfigure hello integration of MaxxPoint into Azure AD, you need tooadd MaxxPoint from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="505a8-125">**tooadd MaxxPoint à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="505a8-125">**tooadd MaxxPoint from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="505a8-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="505a8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="505a8-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="505a8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="505a8-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="505a8-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="505a8-131">Cliquez sur **nouvelle application** bouton en haut de hello de nouvelle application de boîte de dialogue tooadd.</span><span class="sxs-lookup"><span data-stu-id="505a8-131">Click **New application** button on hello top of dialog tooadd new application.</span></span>

    ![Applications][3]

4. <span data-ttu-id="505a8-133">Dans la zone de recherche de hello, tapez **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="505a8-133">In hello search box, type **MaxxPoint**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_001.png)

5. <span data-ttu-id="505a8-135">Dans le volet de résultats hello, sélectionnez **MaxxPoint**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="505a8-135">In hello results panel, select **MaxxPoint**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="505a8-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="505a8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="505a8-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec MaxxPoint avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="505a8-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="505a8-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans MaxxPoint est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="505a8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MaxxPoint is tooa user in Azure AD.</span></span> <span data-ttu-id="505a8-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans MaxxPoint doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="505a8-140">In other words, a link relationship between an Azure AD user and hello related user in MaxxPoint needs toobe established.</span></span>

<span data-ttu-id="505a8-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="505a8-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in MaxxPoint.</span></span>

<span data-ttu-id="505a8-142">tooconfigure et test Azure AD l’authentification unique avec MaxxPoint, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="505a8-142">tooconfigure and test Azure AD single sign-on with MaxxPoint, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="505a8-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="505a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="505a8-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="505a8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="505a8-145">**[Création d’un utilisateur de test MaxxPoint](#creating-a-maxxpoint-test-user)**  -toohave de Britta Simon dans MaxxPoint qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="505a8-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - toohave a counterpart of Britta Simon in MaxxPoint that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="505a8-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="505a8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="505a8-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="505a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="505a8-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="505a8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="505a8-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="505a8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MaxxPoint application.</span></span>

<span data-ttu-id="505a8-150">**tooconfigure Azure AD single sign-on avec MaxxPoint, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="505a8-150">**tooconfigure Azure AD single sign-on with MaxxPoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="505a8-151">Bonjour portail Azure, sur hello **MaxxPoint** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="505a8-151">In hello Azure portal, on hello **MaxxPoint** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="505a8-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="505a8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_300.png)

3. <span data-ttu-id="505a8-155">Sur hello **MaxxPoint domaine et les URL** section, si vous le souhaitez application hello tooconfigure **mode initialisée par IDP**, aucun besoin tooperform toutes les étapes.</span><span class="sxs-lookup"><span data-stu-id="505a8-155">On hello **MaxxPoint Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, no need tooperform any steps.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_02.png)
    
4. <span data-ttu-id="505a8-157">Sur hello **MaxxPoint domaine et les URL** section, si vous le souhaitez application hello tooconfigure **mode initiée par SP**, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="505a8-157">On hello **MaxxPoint Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_03.png)

    <span data-ttu-id="505a8-159">a.</span><span class="sxs-lookup"><span data-stu-id="505a8-159">a.</span></span> <span data-ttu-id="505a8-160">Cliquez sur l’option **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="505a8-160">Click **Show advanced URL settings** option</span></span>

    <span data-ttu-id="505a8-161">b.</span><span class="sxs-lookup"><span data-stu-id="505a8-161">b.</span></span> <span data-ttu-id="505a8-162">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span><span class="sxs-lookup"><span data-stu-id="505a8-162">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="505a8-163">Notez qu’il ne s’agit pas de la valeur réelle hello.</span><span class="sxs-lookup"><span data-stu-id="505a8-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="505a8-164">Vous avez tooupdate URL de connexion cette valeur avec hello réel.</span><span class="sxs-lookup"><span data-stu-id="505a8-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="505a8-165">Appeler l’équipe MaxxPoint **888-728-0950** tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="505a8-165">Call MaxxPoint team on **888-728-0950** tooget this value.</span></span>

5. <span data-ttu-id="505a8-166">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="505a8-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_06.png) 

6. <span data-ttu-id="505a8-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="505a8-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="505a8-170">tooget l’authentification unique configurée pour votre application, d’appeler l’équipe de support MaxxPoint sur **888-728-0950** et ils allez faciliter davantage sur le mode de téléchargement tooprovide les hello **Metadata XML** fichier.</span><span class="sxs-lookup"><span data-stu-id="505a8-170">tooget SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how tooprovide them hello downloaded **Metadata XML** file.</span></span> 

> [!TIP]
> <span data-ttu-id="505a8-171">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="505a8-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="505a8-172">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** section, cliquez simplement sur **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="505a8-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="505a8-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="505a8-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="505a8-174">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="505a8-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="505a8-175">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="505a8-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="505a8-177">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="505a8-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="505a8-178">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="505a8-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="505a8-180">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="505a8-180">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="505a8-182">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="505a8-182">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="505a8-184">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="505a8-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="505a8-186">a.</span><span class="sxs-lookup"><span data-stu-id="505a8-186">a.</span></span> <span data-ttu-id="505a8-187">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="505a8-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="505a8-188">b.</span><span class="sxs-lookup"><span data-stu-id="505a8-188">b.</span></span> <span data-ttu-id="505a8-189">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="505a8-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="505a8-190">c.</span><span class="sxs-lookup"><span data-stu-id="505a8-190">c.</span></span> <span data-ttu-id="505a8-191">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="505a8-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="505a8-192">d.</span><span class="sxs-lookup"><span data-stu-id="505a8-192">d.</span></span> <span data-ttu-id="505a8-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="505a8-193">Click **Create**.</span></span> 

### <a name="creating-a-maxxpoint-test-user"></a><span data-ttu-id="505a8-194">Création d’un utilisateur de test MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="505a8-194">Creating a MaxxPoint test user</span></span>

<span data-ttu-id="505a8-195">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="505a8-195">In this section, you create a user called Britta Simon in MaxxPoint.</span></span> <span data-ttu-id="505a8-196">Contactez l’équipe de support MaxxPoint sur **888-728-0950** tooadd les utilisateurs de hello Bonjour MaxxPoint application.</span><span class="sxs-lookup"><span data-stu-id="505a8-196">Please call MaxxPoint support team on **888-728-0950** tooadd hello users in hello MaxxPoint application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="505a8-197">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="505a8-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="505a8-198">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooMaxxPoint de son accès.</span><span class="sxs-lookup"><span data-stu-id="505a8-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooMaxxPoint.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="505a8-200">**tooassign Britta Simon tooMaxxPoint, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="505a8-200">**tooassign Britta Simon tooMaxxPoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="505a8-201">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="505a8-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="505a8-203">Dans la liste des applications hello, sélectionnez **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="505a8-203">In hello applications list, select **MaxxPoint**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_50.png) 

3. <span data-ttu-id="505a8-205">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="505a8-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="505a8-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="505a8-207">Click **Add** button.</span></span> <span data-ttu-id="505a8-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="505a8-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="505a8-210">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="505a8-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="505a8-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="505a8-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="505a8-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="505a8-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="505a8-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="505a8-213">Testing single sign-on</span></span>

<span data-ttu-id="505a8-214">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="505a8-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="505a8-215">Lorsque vous cliquez sur mosaïque MaxxPoint hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour MaxxPoint application.</span><span class="sxs-lookup"><span data-stu-id="505a8-215">When you click hello MaxxPoint tile in hello Access Panel, you should get automatically signed-on tooyour MaxxPoint application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="505a8-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="505a8-216">Additional resources</span></span>

* [<span data-ttu-id="505a8-217">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="505a8-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="505a8-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="505a8-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_203.png