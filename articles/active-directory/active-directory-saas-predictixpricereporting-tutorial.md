---
title: "Didacticiel : Intégration d’Azure Active Directory à Predictix Price Reporting | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et la création de rapports prix Predictix."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 691d0c43-3aa1-4220-9e46-e7a88db234ad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: c2ba85f613f5a71de72278a0d1916c135b835b60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-price-reporting"></a><span data-ttu-id="eb09f-103">Didacticiel : Intégration d’Azure Active Directory à Predictix Price Reporting</span><span class="sxs-lookup"><span data-stu-id="eb09f-103">Tutorial: Azure Active Directory integration with Predictix Price Reporting</span></span>

<span data-ttu-id="eb09f-104">Dans ce didacticiel, vous apprendrez comment toointegrate Predictix prix Reporting avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb09f-104">In this tutorial, you learn how toointegrate Predictix Price Reporting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eb09f-105">Intégration de Reporting de prix Predictix avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="eb09f-105">Integrating Predictix Price Reporting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eb09f-106">Vous pouvez contrôler dans Azure AD qui a tooPredictix accès prix Reporting.</span><span class="sxs-lookup"><span data-stu-id="eb09f-106">You can control in Azure AD who has access tooPredictix Price Reporting.</span></span>
- <span data-ttu-id="eb09f-107">Vous pouvez activer vos utilisateurs tooautomatically get signé sur tooPredictix prix Reporting (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb09f-107">You can enable your users tooautomatically get signed-on tooPredictix Price Reporting (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="eb09f-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="eb09f-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="eb09f-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb09f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb09f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="eb09f-110">Prerequisites</span></span>

<span data-ttu-id="eb09f-111">tooconfigure intégration d’Azure AD avec Predictix Reporting de prix, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="eb09f-111">tooconfigure Azure AD integration with Predictix Price Reporting, you need hello following items:</span></span>

- <span data-ttu-id="eb09f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb09f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eb09f-113">Un abonnement Predictix Price Reporting pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="eb09f-113">A Predictix Price Reporting single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eb09f-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="eb09f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eb09f-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="eb09f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb09f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="eb09f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eb09f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb09f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eb09f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="eb09f-118">Scenario description</span></span>
<span data-ttu-id="eb09f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="eb09f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eb09f-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="eb09f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb09f-121">Ajout de création de rapports prix Predictix à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="eb09f-121">Adding Predictix Price Reporting from hello gallery</span></span>
2. <span data-ttu-id="eb09f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb09f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-price-reporting-from-hello-gallery"></a><span data-ttu-id="eb09f-123">Ajout de création de rapports prix Predictix à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="eb09f-123">Adding Predictix Price Reporting from hello gallery</span></span>
<span data-ttu-id="eb09f-124">tooconfigure hello intégration de Reporting de prix Predictix dans Azure AD, vous devez tooadd Reporting de prix Predictix à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="eb09f-124">tooconfigure hello integration of Predictix Price Reporting into Azure AD, you need tooadd Predictix Price Reporting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eb09f-125">**tooadd Predictix prix de création de rapports à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb09f-125">**tooadd Predictix Price Reporting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb09f-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="eb09f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="eb09f-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="eb09f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eb09f-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="eb09f-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="eb09f-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="eb09f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="eb09f-133">Dans la zone de recherche de hello, tapez **Reporting de prix Predictix**, sélectionnez **Reporting de prix Predictix** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="eb09f-133">In hello search box, type **Predictix Price Reporting**, select **Predictix Price Reporting** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste des résultats de création de rapports prix Predictix Bonjour](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="eb09f-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb09f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="eb09f-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Predictix Price Reporting avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="eb09f-136">In this section, you configure and test Azure AD single sign-on with Predictix Price Reporting based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eb09f-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans le rapport de prix Predictix est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb09f-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Predictix Price Reporting is tooa user in Azure AD.</span></span> <span data-ttu-id="eb09f-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le rapport de prix Predictix hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="eb09f-138">In other words, a link relationship between an Azure AD user and hello related user in Predictix Price Reporting needs toobe established.</span></span>

<span data-ttu-id="eb09f-139">Dans le rapport de prix Predictix, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="eb09f-139">In Predictix Price Reporting, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eb09f-140">tooconfigure et test Azure AD l’authentification unique sur les rapports de prix Predictix, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="eb09f-140">tooconfigure and test Azure AD single sign-on with Predictix Price Reporting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eb09f-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="eb09f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eb09f-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb09f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb09f-143">**[Créer un utilisateur de test de communication des prix Predictix](#create-a-predictix-price-reporting-test-user)**  -toohave un équivalent de Britta Simon dans Predictix prix Reporting qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="eb09f-143">**[Create a Predictix Price Reporting test user](#create-a-predictix-price-reporting-test-user)** - toohave a counterpart of Britta Simon in Predictix Price Reporting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eb09f-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="eb09f-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb09f-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="eb09f-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="eb09f-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb09f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="eb09f-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de création de rapports prix Predictix.</span><span class="sxs-lookup"><span data-stu-id="eb09f-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Predictix Price Reporting application.</span></span>

<span data-ttu-id="eb09f-148">**tooconfigure Azure AD l’authentification unique avec le signalement de prix Predictix, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb09f-148">**tooconfigure Azure AD single sign-on with Predictix Price Reporting, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb09f-149">Bonjour portail Azure, sur hello **Reporting de prix Predictix** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="eb09f-149">In hello Azure portal, on hello **Predictix Price Reporting** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="eb09f-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="eb09f-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_samlbase.png)

3. <span data-ttu-id="eb09f-153">Sur hello **Predictix prix Reporting domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb09f-153">On hello **Predictix Price Reporting Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Predictix Price Reporting](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_url.png)

    <span data-ttu-id="eb09f-155">a.</span><span class="sxs-lookup"><span data-stu-id="eb09f-155">a.</span></span> <span data-ttu-id="eb09f-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname-pricing>.predictix.com/sso/request`</span><span class="sxs-lookup"><span data-stu-id="eb09f-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname-pricing>.predictix.com/sso/request`</span></span>

    <span data-ttu-id="eb09f-157">b.</span><span class="sxs-lookup"><span data-stu-id="eb09f-157">b.</span></span> <span data-ttu-id="eb09f-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="eb09f-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname-pricing>.predictix.com` |
    | `https://<companyname-pricing>.dev.predictix.com` |

    > [!NOTE] 
    > <span data-ttu-id="eb09f-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="eb09f-159">These values are not real.</span></span> <span data-ttu-id="eb09f-160">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="eb09f-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="eb09f-161">Contact [équipe de support Client de création de rapports prix Predictix](http://www.infor.com/company/customer-center/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="eb09f-161">Contact [Predictix Price Reporting Client support team](http://www.infor.com/company/customer-center/) tooget these values.</span></span> 
 
4. <span data-ttu-id="eb09f-162">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="eb09f-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_certificate.png) 

5. <span data-ttu-id="eb09f-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="eb09f-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eb09f-166">Sur hello **Configuration de Reporting prix Predictix** , cliquez sur **configurer un rapport de prix Predictix** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="eb09f-166">On hello **Predictix Price Reporting Configuration** section, click **Configure Predictix Price Reporting** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eb09f-167">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="eb09f-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de Predictix Price Reporting](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_configure.png) 

7. <span data-ttu-id="eb09f-169">tooconfigure l’authentification unique sur **Reporting de prix Predictix** côté, vous devez hello toosend téléchargé **certificat (Base64)**, **URL de déconnexion, ID d’entité SAML et SAML Single Sign-On URL du service** trop[équipe de support technique de création de rapports prix Predictix](http://www.infor.com/company/customer-center/).</span><span class="sxs-lookup"><span data-stu-id="eb09f-169">tooconfigure single sign-on on **Predictix Price Reporting** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Predictix Price Reporting support team](http://www.infor.com/company/customer-center/).</span></span> <span data-ttu-id="eb09f-170">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="eb09f-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="eb09f-171">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="eb09f-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eb09f-172">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="eb09f-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eb09f-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eb09f-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="eb09f-174">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb09f-174">Create an Azure AD test user</span></span>

<span data-ttu-id="eb09f-175">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="eb09f-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="eb09f-177">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb09f-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb09f-178">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="eb09f-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="eb09f-180">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="eb09f-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="eb09f-182">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="eb09f-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="eb09f-184">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb09f-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-predictixpricereporting-tutorial/create_aaduser_04.png)

    <span data-ttu-id="eb09f-186">a.</span><span class="sxs-lookup"><span data-stu-id="eb09f-186">a.</span></span> <span data-ttu-id="eb09f-187">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb09f-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb09f-188">b.</span><span class="sxs-lookup"><span data-stu-id="eb09f-188">b.</span></span> <span data-ttu-id="eb09f-189">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb09f-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="eb09f-190">c.</span><span class="sxs-lookup"><span data-stu-id="eb09f-190">c.</span></span> <span data-ttu-id="eb09f-191">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="eb09f-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="eb09f-192">d.</span><span class="sxs-lookup"><span data-stu-id="eb09f-192">d.</span></span> <span data-ttu-id="eb09f-193">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="eb09f-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-price-reporting-test-user"></a><span data-ttu-id="eb09f-194">Créer un utilisateur de test Predictix Price Reporting</span><span class="sxs-lookup"><span data-stu-id="eb09f-194">Create a Predictix Price Reporting test user</span></span>

<span data-ttu-id="eb09f-195">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Predictix Price Reporting.</span><span class="sxs-lookup"><span data-stu-id="eb09f-195">In this section, you create a user called Britta Simon in Predictix Price Reporting.</span></span> <span data-ttu-id="eb09f-196">Travailler avec [équipe de support technique de création de rapports prix Predictix](http://www.infor.com/company/customer-center/) tooadd les utilisateurs de hello dans la plateforme de création de rapports prix Predictix hello.</span><span class="sxs-lookup"><span data-stu-id="eb09f-196">Work with [Predictix Price Reporting support team](http://www.infor.com/company/customer-center/) tooadd hello users in hello Predictix Price Reporting platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="eb09f-197">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb09f-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="eb09f-198">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooPredictix accès prix Reporting.</span><span class="sxs-lookup"><span data-stu-id="eb09f-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPredictix Price Reporting.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="eb09f-200">**tooassign tooPredictix Britta Simon prix Reporting, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb09f-200">**tooassign Britta Simon tooPredictix Price Reporting, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb09f-201">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="eb09f-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="eb09f-203">Dans la liste des applications hello, sélectionnez **Predictix Reporting de prix**.</span><span class="sxs-lookup"><span data-stu-id="eb09f-203">In hello applications list, select **Predictix Price Reporting**.</span></span>

    ![lien de communication des prix Predictix Hello dans la liste des Applications hello](./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_predictixpricereporting_app.png)  

3. <span data-ttu-id="eb09f-205">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="eb09f-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="eb09f-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="eb09f-207">Click **Add** button.</span></span> <span data-ttu-id="eb09f-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="eb09f-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="eb09f-210">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="eb09f-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eb09f-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="eb09f-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eb09f-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="eb09f-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="eb09f-213">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="eb09f-213">Test single sign-on</span></span>

<span data-ttu-id="eb09f-214">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="eb09f-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eb09f-215">Lorsque vous cliquez sur mosaïque de communication des prix Predictix hello Bonjour volet d’accès, vous devez obtenir l’application de création de rapports prix Predictix tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="eb09f-215">When you click hello Predictix Price Reporting tile in hello Access Panel, you should get automatically signed-on tooyour Predictix Price Reporting application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eb09f-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="eb09f-216">Additional resources</span></span>

* [<span data-ttu-id="eb09f-217">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb09f-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb09f-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="eb09f-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictixpricereporting-tutorial/tutorial_general_203.png

