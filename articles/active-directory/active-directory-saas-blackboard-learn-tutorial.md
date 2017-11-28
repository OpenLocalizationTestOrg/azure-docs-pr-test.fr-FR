---
title: "Didacticiel : Intégration d'Azure Active Directory à Blackboard Learn | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et unicolore en savoir plus."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0b8ca505-61ea-487c-9a3e-fa50c936df0c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jeedes
ms.openlocfilehash: e94cdd6eaf876d4f66bdd783c442dc468f104e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn"></a><span data-ttu-id="1e53e-103">Didacticiel : Intégration d'Azure Active Directory à Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="1e53e-103">Tutorial: Azure Active Directory integration with Blackboard Learn</span></span>

<span data-ttu-id="1e53e-104">Dans ce didacticiel, vous découvrez comment obtenir des informations toointegrate unicolore avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1e53e-104">In this tutorial, you learn how toointegrate Blackboard Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e53e-105">Intégration unicolore apprendre auprès d’Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1e53e-105">Integrating Blackboard Learn with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1e53e-106">Vous pouvez contrôler dans Azure AD qui a accès tooBlackboard en savoir plus</span><span class="sxs-lookup"><span data-stu-id="1e53e-106">You can control in Azure AD who has access tooBlackboard Learn</span></span>
- <span data-ttu-id="1e53e-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBlackboard apprentissage (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e53e-107">You can enable your users tooautomatically get signed-on tooBlackboard Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1e53e-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="1e53e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1e53e-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1e53e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e53e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1e53e-110">Prerequisites</span></span>

<span data-ttu-id="1e53e-111">tooconfigure intégration d’Azure AD avec unicolore en savoir plus, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1e53e-111">tooconfigure Azure AD integration with Blackboard Learn, you need hello following items:</span></span>

- <span data-ttu-id="1e53e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e53e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e53e-113">Un abonnement avec authentification unique à Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="1e53e-113">A Blackboard Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e53e-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1e53e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e53e-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="1e53e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e53e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1e53e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e53e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e53e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e53e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1e53e-118">Scenario description</span></span>
<span data-ttu-id="1e53e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1e53e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e53e-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="1e53e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e53e-121">Ajout d’unicolore en savoir plus à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="1e53e-121">Adding Blackboard Learn from hello gallery</span></span>
2. <span data-ttu-id="1e53e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e53e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn-from-hello-gallery"></a><span data-ttu-id="1e53e-123">Ajout d’unicolore en savoir plus à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="1e53e-123">Adding Blackboard Learn from hello gallery</span></span>
<span data-ttu-id="1e53e-124">tooconfigure hello intégration d’unicolore savoir dans Azure AD, vous devez tooadd unicolore en savoir plus à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1e53e-124">tooconfigure hello integration of Blackboard Learn into Azure AD, you need tooadd Blackboard Learn from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1e53e-125">**tooadd unicolore en savoir plus à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1e53e-125">**tooadd Blackboard Learn from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e53e-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="1e53e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1e53e-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1e53e-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1e53e-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1e53e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1e53e-133">Dans la zone de recherche de hello, tapez **unicolore en savoir**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-133">In hello search box, type **Blackboard Learn**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_search.png)

5. <span data-ttu-id="1e53e-135">Dans le volet de résultats hello, sélectionnez **unicolore en savoir**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1e53e-135">In hello results panel, select **Blackboard Learn**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1e53e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e53e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1e53e-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Blackboard Learn avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1e53e-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1e53e-139">Pour toowork de l’authentification unique, Azure AD doit tooknow unicolore en savoir quel utilisateur équivalent hello est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e53e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Blackboard Learn is tooa user in Azure AD.</span></span> <span data-ttu-id="1e53e-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans unicolore savoir doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="1e53e-140">In other words, a link relationship between an Azure AD user and hello related user in Blackboard Learn needs toobe established.</span></span>

<span data-ttu-id="1e53e-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans unicolore en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="1e53e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Blackboard Learn.</span></span>

<span data-ttu-id="1e53e-142">tooconfigure et test Azure AD l’authentification unique avec unicolore en savoir plus, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="1e53e-142">tooconfigure and test Azure AD single sign-on with Blackboard Learn, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1e53e-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1e53e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1e53e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e53e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e53e-145">**[Création d’un utilisateur test unicolore en savoir](#creating-a-blackboard-learn-test-user)**  -toohave un équivalent de Britta Simon dans unicolore savoir qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1e53e-145">**[Creating a Blackboard Learn test user](#creating-a-blackboard-learn-test-user)** - toohave a counterpart of Britta Simon in Blackboard Learn that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e53e-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1e53e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e53e-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="1e53e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1e53e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e53e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1e53e-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application unicolore en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="1e53e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Blackboard Learn application.</span></span>

<span data-ttu-id="1e53e-150">**tooconfigure Azure AD single sign-on avec unicolore en savoir plus, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1e53e-150">**tooconfigure Azure AD single sign-on with Blackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e53e-151">Bonjour portail Azure, sur hello **unicolore en savoir** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-151">In hello Azure portal, on hello **Blackboard Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1e53e-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1e53e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_samlbase.png)

3. <span data-ttu-id="1e53e-155">Sur hello **URL et le domaine d’en savoir plus unicolore** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1e53e-155">On hello **Blackboard Learn Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_url.png)

    <span data-ttu-id="1e53e-157">a.</span><span class="sxs-lookup"><span data-stu-id="1e53e-157">a.</span></span> <span data-ttu-id="1e53e-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.blackboard.com/`</span><span class="sxs-lookup"><span data-stu-id="1e53e-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/`</span></span>

    <span data-ttu-id="1e53e-159">b.</span><span class="sxs-lookup"><span data-stu-id="1e53e-159">b.</span></span> <span data-ttu-id="1e53e-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span><span class="sxs-lookup"><span data-stu-id="1e53e-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.blackboard.com/auth-saml/saml/SSO/entity-id/SAML_AD`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="1e53e-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1e53e-161">These values are not real.</span></span> <span data-ttu-id="1e53e-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="1e53e-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1e53e-163">Contact [équipe de support Client de savoir unicolore](https://www.blackboard.com/support/index.aspx) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="1e53e-163">Contact [Blackboard Learn Client support team](https://www.blackboard.com/support/index.aspx) tooget these values.</span></span> 

4. <span data-ttu-id="1e53e-164">Application d’apprentissage unicolore attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="1e53e-164">Blackboard Learn application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="1e53e-165">Configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="1e53e-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="1e53e-166">Vous pouvez gérer les valeurs de ces attributs hello depuis hello **attributs utilisateur** section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="1e53e-166">You can manage hello values of these attributes from hello **User Attributes** section on application integration page.</span></span>
 <span data-ttu-id="1e53e-167">Hello suivant capture d’écran montre un exemple sur elle.</span><span class="sxs-lookup"><span data-stu-id="1e53e-167">hello following screenshot shows an example about it.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute.png)

5. <span data-ttu-id="1e53e-169">Bonjour **attributs utilisateur** section sur **l’authentification unique** boîte de dialogue, configurez les attributs de jetons SAML comme indiqué dans l’image de hello et effectuer des hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="1e53e-169">In hello **User Attributes** section on **Single sign-on** dialog, configure SAML token attributes as shown in hello image and perform hello following steps.</span></span> <span data-ttu-id="1e53e-170">Nous avons mappé hello Userprincipalname comme attribut de l’utilisateur unique hello ici, mais vous pouvez les mapper valeur toohello appropriée, qui de manière unique utilisateur hello dans l’organisation de hello et qui mappe le champ de nom d’utilisateur tooBlackboard en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="1e53e-170">We have mapped hello Userprincipalname as hello unique user attribute here but you can map it toohello appropriate value, which uniquely distinguishes hello user in hello organization and that maps tooBlackboard Learn username field.</span></span>
           
    | <span data-ttu-id="1e53e-171">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="1e53e-171">Attribute Name</span></span> | <span data-ttu-id="1e53e-172">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="1e53e-172">Attribute Value</span></span> |   
    | ---------------| ----------------|
    | <span data-ttu-id="1e53e-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span><span class="sxs-lookup"><span data-stu-id="1e53e-173">urn:oid:1.3.6.1.4.1.5923.1.1.1.6</span></span> |<span data-ttu-id="1e53e-174">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="1e53e-174">user.userprincipalname</span></span> |

    <span data-ttu-id="1e53e-175">a.</span><span class="sxs-lookup"><span data-stu-id="1e53e-175">a.</span></span> <span data-ttu-id="1e53e-176">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1e53e-176">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_04.png)
    
    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="1e53e-179">b.</span><span class="sxs-lookup"><span data-stu-id="1e53e-179">b.</span></span> <span data-ttu-id="1e53e-180">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="1e53e-180">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="1e53e-181">c.</span><span class="sxs-lookup"><span data-stu-id="1e53e-181">c.</span></span> <span data-ttu-id="1e53e-182">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="1e53e-182">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="1e53e-183">d.</span><span class="sxs-lookup"><span data-stu-id="1e53e-183">d.</span></span> <span data-ttu-id="1e53e-184">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-184">Click **Ok**.</span></span>

4. <span data-ttu-id="1e53e-185">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1e53e-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_certificate.png)

7. <span data-ttu-id="1e53e-187">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1e53e-187">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="1e53e-189">Sur hello **Configuration d’en savoir plus unicolore** , cliquez sur **configurer le savoir unicolore** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="1e53e-189">On hello **Blackboard Learn Configuration** section, click **Configure Blackboard Learn** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1e53e-190">Hello de copie **ID d’entité SAML** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="1e53e-190">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_configure.png) 

9. <span data-ttu-id="1e53e-192">tooconfigure l’authentification unique sur **unicolore en savoir** côté, vous devez hello toosend téléchargé **Metadata XML** et **ID d’entité SAML** trop[unicolore en savoir plus prend en charge](https://www.blackboard.com/support/index.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e53e-192">tooconfigure single sign-on on **Blackboard Learn** side, you need toosend hello downloaded **Metadata XML** and **SAML Entity ID** too[Blackboard Learn support](https://www.blackboard.com/support/index.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="1e53e-193">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="1e53e-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1e53e-194">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="1e53e-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1e53e-195">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1e53e-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1e53e-196">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e53e-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="1e53e-197">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="1e53e-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1e53e-199">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1e53e-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e53e-200">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="1e53e-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1e53e-202">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1e53e-204">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="1e53e-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1e53e-206">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1e53e-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-blackboard-learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1e53e-208">a.</span><span class="sxs-lookup"><span data-stu-id="1e53e-208">a.</span></span> <span data-ttu-id="1e53e-209">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e53e-210">b.</span><span class="sxs-lookup"><span data-stu-id="1e53e-210">b.</span></span> <span data-ttu-id="1e53e-211">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1e53e-211">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="1e53e-212">c.</span><span class="sxs-lookup"><span data-stu-id="1e53e-212">c.</span></span> <span data-ttu-id="1e53e-213">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1e53e-214">d.</span><span class="sxs-lookup"><span data-stu-id="1e53e-214">d.</span></span> <span data-ttu-id="1e53e-215">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-215">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn-test-user"></a><span data-ttu-id="1e53e-216">Création d’un utilisateur de test Blackboard Learn</span><span class="sxs-lookup"><span data-stu-id="1e53e-216">Creating a Blackboard Learn test user</span></span>
<span data-ttu-id="1e53e-217">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Blackboard Learn.</span><span class="sxs-lookup"><span data-stu-id="1e53e-217">In this section, you create a user called Britta Simon in Blackboard Learn.</span></span> 

<span data-ttu-id="1e53e-218">L'application Blackboard Learn prend en charge la configuration de l'utilisateur au moment opportun.</span><span class="sxs-lookup"><span data-stu-id="1e53e-218">Blackboard Learn application support just in time user provisioning.</span></span> <span data-ttu-id="1e53e-219">Assurez-vous que vous avez configuré les revendications hello comme décrit dans la section de hello  **[configuration Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span><span class="sxs-lookup"><span data-stu-id="1e53e-219">Make sure that you have configured hello claims as described in hello section **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**</span></span>
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1e53e-220">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1e53e-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1e53e-221">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooBlackboard en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="1e53e-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBlackboard Learn.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1e53e-223">**tooassign Britta Simon tooBlackboard en savoir plus, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1e53e-223">**tooassign Britta Simon tooBlackboard Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="1e53e-224">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1e53e-226">Dans la liste des applications hello, sélectionnez **unicolore en savoir**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-226">In hello applications list, select **Blackboard Learn**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-blackboard-learn-tutorial/tutorial_blackboardlearn_app.png) 

3. <span data-ttu-id="1e53e-228">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1e53e-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-230">Click **Add** button.</span></span> <span data-ttu-id="1e53e-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1e53e-233">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="1e53e-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1e53e-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e53e-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1e53e-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1e53e-236">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1e53e-236">Testing single sign-on</span></span>

<span data-ttu-id="1e53e-237">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="1e53e-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1e53e-238">Lorsque vous cliquez sur hello unicolore savoir mosaïque hello volet d’accès, vous devez obtenir l’application de tooyour automatiquement signé sur unicolore en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="1e53e-238">When you click hello Blackboard Learn tile in hello Access Panel, you should get automatically signed-on tooyour Blackboard Learn application.</span></span> <span data-ttu-id="1e53e-239">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1e53e-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="1e53e-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1e53e-240">Additional resources</span></span>

* [<span data-ttu-id="1e53e-241">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1e53e-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e53e-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1e53e-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-tutorial/tutorial_general_203.png

