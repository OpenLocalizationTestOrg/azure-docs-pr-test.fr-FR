---
title: "Didacticiel : Intégration d’Azure Active Directory à Cerner Central | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Cerner Central."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 3493d180e8f229b7cd228769f780f10208114889
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="8307c-103">Didacticiel : Intégration d’Azure Active Directory à Cerner Central</span><span class="sxs-lookup"><span data-stu-id="8307c-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="8307c-104">Dans ce didacticiel, vous apprendrez comment toointegrate centre Cerner avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8307c-104">In this tutorial, you learn how toointegrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8307c-105">Intégration Cerner Central à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8307c-105">Integrating Cerner Central with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8307c-106">Vous pouvez contrôler dans Azure AD qui a accès tooCerner Central</span><span class="sxs-lookup"><span data-stu-id="8307c-106">You can control in Azure AD who has access tooCerner Central</span></span>
- <span data-ttu-id="8307c-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooCerner Central (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="8307c-107">You can enable your users tooautomatically get signed-on tooCerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8307c-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8307c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8307c-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8307c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8307c-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8307c-110">Prerequisites</span></span>

<span data-ttu-id="8307c-111">tooconfigure intégration d’Azure AD avec Cerner Central, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8307c-111">tooconfigure Azure AD integration with Cerner Central, you need hello following items:</span></span>

- <span data-ttu-id="8307c-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8307c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8307c-113">Un compte du système Central Cerner approuvé</span><span class="sxs-lookup"><span data-stu-id="8307c-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="8307c-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8307c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8307c-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="8307c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8307c-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8307c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8307c-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8307c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8307c-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8307c-118">Scenario description</span></span>
<span data-ttu-id="8307c-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8307c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8307c-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="8307c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8307c-121">Ajout de Cerner Central à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8307c-121">Adding Cerner Central from hello gallery</span></span>
2. <span data-ttu-id="8307c-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8307c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-hello-gallery"></a><span data-ttu-id="8307c-123">Ajout de Cerner Central à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8307c-123">Adding Cerner Central from hello gallery</span></span>
<span data-ttu-id="8307c-124">intégration de hello tooconfigure de Cerner Central dans Azure AD, vous devez tooadd Cerner Central à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8307c-124">tooconfigure hello integration of Cerner Central into Azure AD, you need tooadd Cerner Central from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8307c-125">**tooadd centre Cerner à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8307c-125">**tooadd Cerner Central from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8307c-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8307c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8307c-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8307c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8307c-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8307c-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8307c-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de la boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="8307c-131">tooadd new application, click **New application** button on top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8307c-133">Dans la zone de recherche de hello, tapez **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="8307c-133">In hello search box, type **Cerner Central**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="8307c-135">Dans le volet de résultats hello, sélectionnez **Cerner centre**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8307c-135">In hello results panel, select **Cerner Central**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8307c-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8307c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8307c-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Cerner Central pour un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8307c-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8307c-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Cerner Central est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8307c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cerner Central is tooa user in Azure AD.</span></span> <span data-ttu-id="8307c-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le centre de Cerner hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="8307c-140">In other words, a link relationship between an Azure AD user and hello related user in Cerner Central needs toobe established.</span></span>

<span data-ttu-id="8307c-141">tooconfigure et test Azure AD l’authentification unique avec Cerner Central, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="8307c-141">tooconfigure and test Azure AD single sign-on with Cerner Central, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8307c-142">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8307c-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8307c-143">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8307c-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8307c-144">**[Création d’un utilisateur de test Cerner centre](#creating-a-cerner-central-test-user)**  -toohave un équivalent de Britta Simon Cerner central qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="8307c-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - toohave a counterpart of Britta Simon in Cerner Central that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="8307c-145">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8307c-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8307c-146">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="8307c-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8307c-147">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8307c-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8307c-148">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de centre de Cerner.</span><span class="sxs-lookup"><span data-stu-id="8307c-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="8307c-149">**tooconfigure Azure AD single sign-on avec Cerner Central, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8307c-149">**tooconfigure Azure AD single sign-on with Cerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="8307c-150">Bonjour portail Azure, sur hello **Cerner centre** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8307c-150">In hello Azure portal, on hello **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8307c-152">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8307c-152">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="8307c-154">Sur hello **Cerner les domaine Central et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8307c-154">On hello **Cerner Central Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="8307c-156">a.</span><span class="sxs-lookup"><span data-stu-id="8307c-156">a.</span></span> <span data-ttu-id="8307c-157">Bonjour **identificateur** zone de texte, valeur hello de type hello suivant des modèles à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="8307c-157">In hello **Identifier** textbox, type hello value using hello following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="8307c-158">b.</span><span class="sxs-lookup"><span data-stu-id="8307c-158">b.</span></span> <span data-ttu-id="8307c-159">Bonjour **URL de réponse** modèles de zone de texte, tapez une URL à l’aide de hello suivant :</span><span class="sxs-lookup"><span data-stu-id="8307c-159">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="8307c-160">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="8307c-160">These values are not hello real.</span></span> <span data-ttu-id="8307c-161">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="8307c-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="8307c-162">Contact [équipe de support Cerner centre](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="8307c-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget these values.</span></span>
 
4. <span data-ttu-id="8307c-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8307c-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="8307c-165">toogenerate hello **métadonnées** url, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8307c-165">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="8307c-166">a.</span><span class="sxs-lookup"><span data-stu-id="8307c-166">a.</span></span> <span data-ttu-id="8307c-167">Cliquez sur **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="8307c-167">Click **App registrations**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="8307c-169">b.</span><span class="sxs-lookup"><span data-stu-id="8307c-169">b.</span></span> <span data-ttu-id="8307c-170">Cliquez sur **points de terminaison** tooopen **points de terminaison** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8307c-170">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="8307c-172">c.</span><span class="sxs-lookup"><span data-stu-id="8307c-172">c.</span></span> <span data-ttu-id="8307c-173">Cliquez sur hello copie bouton toocopy **DOCUMENT de métadonnées de fédération** url et collez-le dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="8307c-173">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="8307c-175">d.</span><span class="sxs-lookup"><span data-stu-id="8307c-175">d.</span></span> <span data-ttu-id="8307c-176">Maintenant accédez toohello page de propriétés de **Cerner centre** et copie Bonjour **Id d’Application** à l’aide de **copie** bouton et collez-le dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="8307c-176">Now go toohello property page of **Cerner Central** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="8307c-178">e.</span><span class="sxs-lookup"><span data-stu-id="8307c-178">e.</span></span> <span data-ttu-id="8307c-179">Générer hello **URL de métadonnées** hello suivant le modèle à l’aide de :`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="8307c-179">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="8307c-180">tooconfigure l’authentification unique sur **Cerner centre** côté, vous devez toosend hello **URL de métadonnées** trop[prise en charge du centre de Cerner](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="8307c-180">tooconfigure single sign-on on **Cerner Central** side, you need toosend hello **Metadata URL** too[Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="8307c-181">Ils configurent hello SSO sur l’intégration d’application côté toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="8307c-181">They configure hello SSO on application side toocomplete hello integration.</span></span>

> [!TIP]
> <span data-ttu-id="8307c-182">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="8307c-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8307c-183">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="8307c-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8307c-184">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8307c-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8307c-185">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8307c-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="8307c-186">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="8307c-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span> 

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8307c-188">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8307c-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8307c-189">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8307c-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8307c-191">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8307c-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8307c-193">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8307c-193">tooopen hello **User** dialog, click **Add**.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8307c-195">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8307c-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8307c-197">a.</span><span class="sxs-lookup"><span data-stu-id="8307c-197">a.</span></span> <span data-ttu-id="8307c-198">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8307c-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8307c-199">b.</span><span class="sxs-lookup"><span data-stu-id="8307c-199">b.</span></span> <span data-ttu-id="8307c-200">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8307c-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="8307c-201">c.</span><span class="sxs-lookup"><span data-stu-id="8307c-201">c.</span></span> <span data-ttu-id="8307c-202">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8307c-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8307c-203">d.</span><span class="sxs-lookup"><span data-stu-id="8307c-203">d.</span></span> <span data-ttu-id="8307c-204">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8307c-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="8307c-205">Création d’un utilisateur de test Cerner Central</span><span class="sxs-lookup"><span data-stu-id="8307c-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="8307c-206">L’application **Cerner Central** permet l’authentification à partir de n’importe quel fournisseur d’identité fédérée.</span><span class="sxs-lookup"><span data-stu-id="8307c-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="8307c-207">Si un utilisateur est en mesure de toolog dans la page d’accueil toohello application, ils sont fédérés et n’ont pas besoin de toute configuration manuelle.</span><span class="sxs-lookup"><span data-stu-id="8307c-207">If a user is able toolog in toohello application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8307c-208">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8307c-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8307c-209">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCerner Central.</span><span class="sxs-lookup"><span data-stu-id="8307c-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCerner Central.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8307c-211">**tooassign Britta Simon tooCerner Central, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8307c-211">**tooassign Britta Simon tooCerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="8307c-212">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8307c-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8307c-214">Dans la liste des applications hello, sélectionnez **Cerner Central**.</span><span class="sxs-lookup"><span data-stu-id="8307c-214">In hello applications list, select **Cerner Central**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="8307c-216">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8307c-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8307c-218">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8307c-218">Click **Add** button.</span></span> <span data-ttu-id="8307c-219">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8307c-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8307c-221">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="8307c-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8307c-222">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8307c-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8307c-223">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8307c-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8307c-224">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8307c-224">Testing single sign-on</span></span>

<span data-ttu-id="8307c-225">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="8307c-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8307c-226">Lorsque vous cliquez sur hello Cerner centre vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application Cerner centrale.</span><span class="sxs-lookup"><span data-stu-id="8307c-226">When you click hello Cerner Central tile in hello Access Panel, you should get automatically signed-on tooyour Cerner Central application.</span></span> <span data-ttu-id="8307c-227">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8307c-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8307c-228">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8307c-228">Additional resources</span></span>

* [<span data-ttu-id="8307c-229">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8307c-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8307c-230">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8307c-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

