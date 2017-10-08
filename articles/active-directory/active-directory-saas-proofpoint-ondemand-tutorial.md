---
title: "Didacticiel : Intégration d’Azure Active Directory à Proofpoint on Demand | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Proofpoint à la demande."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 773e7f7d-ec31-411b-860d-6a6633335d43
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 0f9472ddc01f2c18ffc9e8d2b59a17b3b595515e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-proofpoint-on-demand"></a><span data-ttu-id="47f3b-103">Didacticiel : Intégration d’Azure Active Directory avec Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="47f3b-103">Tutorial: Azure Active Directory integration with Proofpoint on Demand</span></span>

<span data-ttu-id="47f3b-104">Dans ce didacticiel, vous apprendrez comment toointegrate Proofpoint à la demande avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="47f3b-104">In this tutorial, you learn how toointegrate Proofpoint on Demand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="47f3b-105">Intégration Proofpoint à la demande à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="47f3b-105">Integrating Proofpoint on Demand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="47f3b-106">Vous pouvez contrôler dans Azure AD qui a tooProofpoint d’accès à la demande</span><span class="sxs-lookup"><span data-stu-id="47f3b-106">You can control in Azure AD who has access tooProofpoint on Demand</span></span>
- <span data-ttu-id="47f3b-107">Vous pouvez activer vos utilisateurs tooautomatically get signé sur tooProofpoint à la demande (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="47f3b-107">You can enable your users tooautomatically get signed-on tooProofpoint on Demand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="47f3b-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="47f3b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="47f3b-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="47f3b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47f3b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="47f3b-110">Prerequisites</span></span>

<span data-ttu-id="47f3b-111">intégration d’Azure AD de tooconfigure Proofpoint à la demande, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="47f3b-111">tooconfigure Azure AD integration with Proofpoint on Demand, you need hello following items:</span></span>

- <span data-ttu-id="47f3b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="47f3b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="47f3b-113">Un abonnement Proofpoint on Demand pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="47f3b-113">A Proofpoint on Demand single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="47f3b-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="47f3b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="47f3b-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="47f3b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="47f3b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="47f3b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="47f3b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47f3b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="47f3b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="47f3b-118">Scenario description</span></span>
<span data-ttu-id="47f3b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="47f3b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="47f3b-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="47f3b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="47f3b-121">Ajout de Proofpoint à la demande à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="47f3b-121">Adding Proofpoint on Demand from hello gallery</span></span>
2. <span data-ttu-id="47f3b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="47f3b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-proofpoint-on-demand-from-hello-gallery"></a><span data-ttu-id="47f3b-123">Ajout de Proofpoint à la demande à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="47f3b-123">Adding Proofpoint on Demand from hello gallery</span></span>
<span data-ttu-id="47f3b-124">tooconfigure hello intégration de Proofpoint à la demande dans Azure AD, vous devez tooadd Proofpoint à la demande à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="47f3b-124">tooconfigure hello integration of Proofpoint on Demand into Azure AD, you need tooadd Proofpoint on Demand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="47f3b-125">**tooadd Proofpoint à la demande à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="47f3b-125">**tooadd Proofpoint on Demand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="47f3b-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="47f3b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="47f3b-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="47f3b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="47f3b-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="47f3b-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="47f3b-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="47f3b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="47f3b-133">Dans la zone de recherche de hello, tapez **Proofpoint à la demande**.</span><span class="sxs-lookup"><span data-stu-id="47f3b-133">In hello search box, type **Proofpoint on Demand**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_search.png)

5. <span data-ttu-id="47f3b-135">Dans le volet de résultats hello, sélectionnez **Proofpoint à la demande**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="47f3b-135">In hello results panel, select **Proofpoint on Demand**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="47f3b-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="47f3b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="47f3b-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Proofpoint on Demand grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="47f3b-138">In this section, you configure and test Azure AD single sign-on with Proofpoint on Demand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="47f3b-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Proofpoint à la demande est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47f3b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Proofpoint on Demand is tooa user in Azure AD.</span></span> <span data-ttu-id="47f3b-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Proofpoint à la demande doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="47f3b-140">In other words, a link relationship between an Azure AD user and hello related user in Proofpoint on Demand needs toobe established.</span></span>

<span data-ttu-id="47f3b-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Proofpoint à la demande.</span><span class="sxs-lookup"><span data-stu-id="47f3b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Proofpoint on Demand.</span></span>

<span data-ttu-id="47f3b-142">tooconfigure et test Azure AD sur l’authentification unique avec Proofpoint à la demande, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="47f3b-142">tooconfigure and test Azure AD single sign-on with Proofpoint on Demand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="47f3b-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="47f3b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="47f3b-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47f3b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="47f3b-145">**[Création d’un Proofpoint sur utilisateur de test à la demande](#creating-a-proofpoint-on-demand-test-user)**  -toohave un équivalent de Britta Simon dans Proofpoint à la demande qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="47f3b-145">**[Creating a Proofpoint on Demand test user](#creating-a-proofpoint-on-demand-test-user)** - toohave a counterpart of Britta Simon in Proofpoint on Demand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="47f3b-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="47f3b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="47f3b-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="47f3b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="47f3b-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="47f3b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="47f3b-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre Proofpoint dans l’application à la demande.</span><span class="sxs-lookup"><span data-stu-id="47f3b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Proofpoint on Demand application.</span></span>

<span data-ttu-id="47f3b-150">**tooconfigure Azure AD single sign-on avec Proofpoint à la demande, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="47f3b-150">**tooconfigure Azure AD single sign-on with Proofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="47f3b-151">Bonjour portail Azure, sur hello **Proofpoint à la demande** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="47f3b-151">In hello Azure portal, on hello **Proofpoint on Demand** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="47f3b-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="47f3b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
  
    ![Configurer l’authentification unique](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_samlbase.png)

3. <span data-ttu-id="47f3b-155">Sur hello **Proofpoint sur le domaine de la demande et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="47f3b-155">On hello **Proofpoint on Demand Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_url.png)

    <span data-ttu-id="47f3b-157">a.In hello **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<hostname>.pphosted.com/ppssamlsp_hostname`</span><span class="sxs-lookup"><span data-stu-id="47f3b-157">a.In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp_hostname`</span></span>

    <span data-ttu-id="47f3b-158">b.</span><span class="sxs-lookup"><span data-stu-id="47f3b-158">b.</span></span> <span data-ttu-id="47f3b-159">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<hostname>.pphosted.com/ppssamlsp`</span><span class="sxs-lookup"><span data-stu-id="47f3b-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com/ppssamlsp`</span></span>

    <span data-ttu-id="47f3b-160">c.</span><span class="sxs-lookup"><span data-stu-id="47f3b-160">c.</span></span>  <span data-ttu-id="47f3b-161">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span><span class="sxs-lookup"><span data-stu-id="47f3b-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<hostname>.pphosted.com:portnumber/v1/samlauth/samlconsumer`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="47f3b-162">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="47f3b-162">These values are not hello real.</span></span> <span data-ttu-id="47f3b-163">Mettre à jour les valeurs de hello réel identificateur, les URL de réponse et les URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="47f3b-163">Update these values with hello actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="47f3b-164">Contact [Proofpoint sur l’équipe de support technique à la demande Client](https://www.proofpoint.com/us/support-services) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="47f3b-164">Contact [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooget these values.</span></span> 

4. <span data-ttu-id="47f3b-165">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="47f3b-165">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_certificate.png) 

5. <span data-ttu-id="47f3b-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="47f3b-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="47f3b-169">Sur hello **Proofpoint sur la Configuration de la demande** , cliquez sur **Proofpoint de configurer à la demande** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="47f3b-169">On hello **Proofpoint on Demand Configuration** section, click **Configure Proofpoint on Demand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="47f3b-170">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="47f3b-170">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_configure.png) 

7. <span data-ttu-id="47f3b-172">tooconfigure l’authentification unique sur **Proofpoint à la demande** côté, vous devez hello toosend téléchargé **Certificate(Base64)**,**ID d’entité SAML**, et **SAML Single Sign-On URL du Service** trop[Proofpoint sur l’équipe de support technique à la demande Client](https://www.proofpoint.com/us/support-services).</span><span class="sxs-lookup"><span data-stu-id="47f3b-172">tooconfigure single sign-on on **Proofpoint on Demand** side, you need toosend hello downloaded **Certificate(Base64)**,**SAML Entity ID**, and **SAML Single Sign-On Service URL** too[Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services).</span></span>

> [!TIP]
> <span data-ttu-id="47f3b-173">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="47f3b-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="47f3b-174">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="47f3b-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="47f3b-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="47f3b-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="47f3b-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="47f3b-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="47f3b-177">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="47f3b-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="47f3b-179">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="47f3b-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="47f3b-180">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="47f3b-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="47f3b-182">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="47f3b-182">These values are not hello real.</span></span> <span data-ttu-id="47f3b-183">Mettre à jour ces valeurs avec hello réel</span><span class="sxs-lookup"><span data-stu-id="47f3b-183">Update these values with hello actual</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="47f3b-185">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="47f3b-185">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="47f3b-187">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="47f3b-187">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-proofpoint-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="47f3b-189">a.</span><span class="sxs-lookup"><span data-stu-id="47f3b-189">a.</span></span> <span data-ttu-id="47f3b-190">Bonjour **nom** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="47f3b-190">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="47f3b-191">b.</span><span class="sxs-lookup"><span data-stu-id="47f3b-191">b.</span></span> <span data-ttu-id="47f3b-192">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47f3b-192">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="47f3b-193">c.</span><span class="sxs-lookup"><span data-stu-id="47f3b-193">c.</span></span> <span data-ttu-id="47f3b-194">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="47f3b-194">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="47f3b-195">d.</span><span class="sxs-lookup"><span data-stu-id="47f3b-195">d.</span></span> <span data-ttu-id="47f3b-196">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="47f3b-196">Click **Create**.</span></span>
 
### <a name="creating-a-proofpoint-on-demand-test-user"></a><span data-ttu-id="47f3b-197">Créer un utilisateur de test Proofpoint on Demand</span><span class="sxs-lookup"><span data-stu-id="47f3b-197">Creating a Proofpoint on Demand test user</span></span>

<span data-ttu-id="47f3b-198">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Proofpoint on Demand.</span><span class="sxs-lookup"><span data-stu-id="47f3b-198">In this section, you create a user called Britta Simon in Proofpoint on Demand.</span></span> <span data-ttu-id="47f3b-199">Travailler avec [Proofpoint sur l’équipe de support technique à la demande Client](https://www.proofpoint.com/us/support-services) utilisateurs tooadd Bonjour Proofpoint sur la plateforme de la demande.</span><span class="sxs-lookup"><span data-stu-id="47f3b-199">Work with [Proofpoint on Demand Client support team](https://www.proofpoint.com/us/support-services) tooadd users in hello Proofpoint on Demand platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="47f3b-200">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="47f3b-200">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="47f3b-201">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooProofpoint d’accès à la demande.</span><span class="sxs-lookup"><span data-stu-id="47f3b-201">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooProofpoint on Demand.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="47f3b-203">**tooassign tooProofpoint Britta Simon à la demande, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="47f3b-203">**tooassign Britta Simon tooProofpoint on Demand, perform hello following steps:**</span></span>

1. <span data-ttu-id="47f3b-204">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="47f3b-204">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="47f3b-206">Dans la liste des applications hello, sélectionnez **Proofpoint à la demande**.</span><span class="sxs-lookup"><span data-stu-id="47f3b-206">In hello applications list, select **Proofpoint on Demand**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_proofpointondemand_app.png) 

3. <span data-ttu-id="47f3b-208">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="47f3b-208">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="47f3b-210">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="47f3b-210">Click **Add** button.</span></span> <span data-ttu-id="47f3b-211">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="47f3b-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="47f3b-213">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="47f3b-213">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="47f3b-214">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="47f3b-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="47f3b-215">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="47f3b-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="47f3b-216">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="47f3b-216">Testing single sign-on</span></span>

<span data-ttu-id="47f3b-217">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="47f3b-217">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="47f3b-218">Lorsque vous cliquez sur hello **Proofpoint à la demande** vignette sur hello volet d’accès, vous devez être connecté automatiquement sur tooyour Proofpoint dans l’application à la demande.</span><span class="sxs-lookup"><span data-stu-id="47f3b-218">When you click hello **Proofpoint on Demand** tile on hello Access Panel, you should be automatically signed on tooyour Proofpoint on Demand application.</span></span>
<span data-ttu-id="47f3b-219">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="47f3b-219">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>  

## <a name="additional-resources"></a><span data-ttu-id="47f3b-220">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="47f3b-220">Additional resources</span></span>

* [<span data-ttu-id="47f3b-221">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47f3b-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="47f3b-222">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="47f3b-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-proofpoint-ondemand-tutorial/tutorial_general_203.png

