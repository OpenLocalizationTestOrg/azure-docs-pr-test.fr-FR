---
title: "Didacticiel : Intégration d’Azure Active Directory à Reward Gateway | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de la passerelle de récompense."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34336386-998a-4d47-ab55-721d97708e5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 30cdd538471b373468c3d990e4568ddb08081a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-reward-gateway"></a><span data-ttu-id="52b77-103">Didacticiel : Intégration d’Azure Active Directory à Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="52b77-103">Tutorial: Azure Active Directory integration with Reward Gateway</span></span>

<span data-ttu-id="52b77-104">Dans ce didacticiel, vous apprendrez comment toointegrate passerelle récompense avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52b77-104">In this tutorial, you learn how toointegrate Reward Gateway with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52b77-105">Intégration de passerelle de récompense à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="52b77-105">Integrating Reward Gateway with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="52b77-106">Vous pouvez contrôler dans Azure AD qui a accès tooReward passerelle</span><span class="sxs-lookup"><span data-stu-id="52b77-106">You can control in Azure AD who has access tooReward Gateway</span></span>
- <span data-ttu-id="52b77-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooReward passerelle (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="52b77-107">You can enable your users tooautomatically get signed-on tooReward Gateway (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="52b77-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="52b77-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="52b77-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52b77-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52b77-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="52b77-110">Prerequisites</span></span>

<span data-ttu-id="52b77-111">intégration d’Azure AD avec une passerelle de récompense de tooconfigure, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="52b77-111">tooconfigure Azure AD integration with Reward Gateway, you need hello following items:</span></span>

- <span data-ttu-id="52b77-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="52b77-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52b77-113">Un abonnement Reward Gateway pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="52b77-113">A Reward Gateway single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52b77-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="52b77-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52b77-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="52b77-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52b77-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="52b77-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52b77-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52b77-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52b77-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="52b77-118">Scenario description</span></span>
<span data-ttu-id="52b77-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="52b77-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52b77-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="52b77-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52b77-121">Ajout de passerelle de récompense de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="52b77-121">Adding Reward Gateway from hello gallery</span></span>
2. <span data-ttu-id="52b77-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="52b77-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-reward-gateway-from-hello-gallery"></a><span data-ttu-id="52b77-123">Ajout de passerelle de récompense de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="52b77-123">Adding Reward Gateway from hello gallery</span></span>
<span data-ttu-id="52b77-124">tooconfigure hello intégration de passerelle de récompense dans Azure AD, vous devez tooadd passerelle récompense à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="52b77-124">tooconfigure hello integration of Reward Gateway into Azure AD, you need tooadd Reward Gateway from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="52b77-125">**tooadd passerelle de récompense de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="52b77-125">**tooadd Reward Gateway from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="52b77-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="52b77-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="52b77-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="52b77-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="52b77-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="52b77-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="52b77-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="52b77-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="52b77-133">Dans la zone de recherche de hello, tapez **récompense passerelle**.</span><span class="sxs-lookup"><span data-stu-id="52b77-133">In hello search box, type **Reward Gateway**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_search.png)

5. <span data-ttu-id="52b77-135">Dans le volet de résultats hello, sélectionnez **récompense passerelle**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="52b77-135">In hello results panel, select **Reward Gateway**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="52b77-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="52b77-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="52b77-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Reward Gateway, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="52b77-138">In this section, you configure and test Azure AD single sign-on with Reward Gateway based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="52b77-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans la passerelle de récompense est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52b77-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Reward Gateway is tooa user in Azure AD.</span></span> <span data-ttu-id="52b77-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans la passerelle de récompense hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="52b77-140">In other words, a link relationship between an Azure AD user and hello related user in Reward Gateway needs toobe established.</span></span>

<span data-ttu-id="52b77-141">Dans la passerelle de récompense, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="52b77-141">In Reward Gateway, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="52b77-142">tooconfigure et test Azure AD l’authentification unique avec une passerelle de récompense, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="52b77-142">tooconfigure and test Azure AD single sign-on with Reward Gateway, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="52b77-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="52b77-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="52b77-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52b77-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52b77-145">**[Création d’un utilisateur de test de passerelle de récompense](#creating-a-reward-gateway-test-user)**  -toohave un équivalent de Britta Simon dans la passerelle de récompense est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="52b77-145">**[Creating a Reward Gateway test user](#creating-a-reward-gateway-test-user)** - toohave a counterpart of Britta Simon in Reward Gateway that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="52b77-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="52b77-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52b77-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="52b77-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="52b77-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="52b77-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="52b77-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de la passerelle de récompense.</span><span class="sxs-lookup"><span data-stu-id="52b77-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Reward Gateway application.</span></span>

<span data-ttu-id="52b77-150">**tooconfigure Azure AD authentification unique avec la passerelle de récompense, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="52b77-150">**tooconfigure Azure AD single sign-on with Reward Gateway, perform hello following steps:**</span></span>

1. <span data-ttu-id="52b77-151">Bonjour portail Azure, sur hello **récompense passerelle** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="52b77-151">In hello Azure portal, on hello **Reward Gateway** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="52b77-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="52b77-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_samlbase.png)

3. <span data-ttu-id="52b77-155">Sur hello **domaine récompense de la passerelle et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="52b77-155">On hello **Reward Gateway Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_url.png)

    <span data-ttu-id="52b77-157">a.</span><span class="sxs-lookup"><span data-stu-id="52b77-157">a.</span></span> <span data-ttu-id="52b77-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="52b77-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.rewardgateway.com` |
    | `https://<companyname>.rewardgateway.co.uk/` |
    | `https://<companyname>.rewardgateway.co.nz/` |
    | `https://<companyname>.rewardgateway.com.au/` |

    <span data-ttu-id="52b77-159">b.</span><span class="sxs-lookup"><span data-stu-id="52b77-159">b.</span></span> <span data-ttu-id="52b77-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="52b77-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    |  `https://<companyname>.rewardgateway.com/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.uk/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.nz/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.com.au/Authentication/EndLogin?idp=<Unique Id>` |

    > [!NOTE] 
    > <span data-ttu-id="52b77-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="52b77-161">These values are not real.</span></span> <span data-ttu-id="52b77-162">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="52b77-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="52b77-163">Contact [équipe de support technique de récompense passerelle](mailto:clientsupport@rewardgateway.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="52b77-163">Contact [Reward Gateway support team](mailto:clientsupport@rewardgateway.com) tooget these values.</span></span>
 
4. <span data-ttu-id="52b77-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="52b77-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_certificate.png) 

5. <span data-ttu-id="52b77-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="52b77-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="52b77-168">tooconfigure l’authentification unique sur **récompense passerelle** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support technique de récompense passerelle](mailto:clientsupport@rewardgateway.com).</span><span class="sxs-lookup"><span data-stu-id="52b77-168">tooconfigure single sign-on on **Reward Gateway** side, you need toosend hello downloaded **Metadata XML** too[Reward Gateway support team](mailto:clientsupport@rewardgateway.com).</span></span> <span data-ttu-id="52b77-169">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="52b77-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="52b77-170">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="52b77-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="52b77-171">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="52b77-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="52b77-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="52b77-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="52b77-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="52b77-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="52b77-174">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="52b77-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="52b77-176">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="52b77-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="52b77-177">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="52b77-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="52b77-179">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="52b77-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="52b77-181">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="52b77-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="52b77-183">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="52b77-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="52b77-185">a.</span><span class="sxs-lookup"><span data-stu-id="52b77-185">a.</span></span> <span data-ttu-id="52b77-186">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52b77-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52b77-187">b.</span><span class="sxs-lookup"><span data-stu-id="52b77-187">b.</span></span> <span data-ttu-id="52b77-188">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="52b77-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="52b77-189">c.</span><span class="sxs-lookup"><span data-stu-id="52b77-189">c.</span></span> <span data-ttu-id="52b77-190">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="52b77-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="52b77-191">d.</span><span class="sxs-lookup"><span data-stu-id="52b77-191">d.</span></span> <span data-ttu-id="52b77-192">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="52b77-192">Click **Create**.</span></span>
 
### <a name="creating-a-reward-gateway-test-user"></a><span data-ttu-id="52b77-193">Création d’un utilisateur de test Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="52b77-193">Creating a Reward Gateway test user</span></span>

<span data-ttu-id="52b77-194">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="52b77-194">In this section, you create a user called Britta Simon in Reward Gateway.</span></span> <span data-ttu-id="52b77-195">Travailler avec la passerelle de récompense [équipe de support](mailto:clientsupport@rewardgateway.com) tooadd les utilisateurs de hello dans la plateforme de passerelle de récompense hello.</span><span class="sxs-lookup"><span data-stu-id="52b77-195">Work with Reward Gateway [support team](mailto:clientsupport@rewardgateway.com) tooadd hello users in hello Reward Gateway platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="52b77-196">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="52b77-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="52b77-197">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooReward passerelle.</span><span class="sxs-lookup"><span data-stu-id="52b77-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooReward Gateway.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="52b77-199">**tooassign Britta Simon tooReward passerelle, exécutez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="52b77-199">**tooassign Britta Simon tooReward Gateway, perform hello following steps:**</span></span>

1. <span data-ttu-id="52b77-200">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="52b77-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="52b77-202">Dans la liste des applications hello, sélectionnez **récompense passerelle**.</span><span class="sxs-lookup"><span data-stu-id="52b77-202">In hello applications list, select **Reward Gateway**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_app.png) 

3. <span data-ttu-id="52b77-204">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="52b77-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="52b77-206">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="52b77-206">Click **Add** button.</span></span> <span data-ttu-id="52b77-207">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="52b77-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="52b77-209">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="52b77-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="52b77-210">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="52b77-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="52b77-211">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="52b77-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="52b77-212">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="52b77-212">Testing single sign-on</span></span>

<span data-ttu-id="52b77-213">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="52b77-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="52b77-214">Lorsque vous cliquez sur mosaïque de récompense passerelle hello Bonjour volet d’accès, vous devez obtenir l’application de récompense passerelle tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="52b77-214">When you click hello Reward Gateway tile in hello Access Panel, you should get automatically signed-on tooyour Reward Gateway application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="52b77-215">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="52b77-215">Additional resources</span></span>

* [<span data-ttu-id="52b77-216">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52b77-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52b77-217">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="52b77-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_203.png

