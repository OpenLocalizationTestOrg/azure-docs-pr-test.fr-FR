---
title: "Didacticiel : Intégration d’Azure Active Directory à BenefitHub | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et BenefitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4069fe32-a452-463f-973e-7aa0baa4c2fa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: c07d6e44e8cbc79afd79c900664011b059206b56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefithub"></a><span data-ttu-id="8f1eb-103">Didacticiel : Intégration d’Azure Active Directory à BenefitHub</span><span class="sxs-lookup"><span data-stu-id="8f1eb-103">Tutorial: Azure Active Directory integration with BenefitHub</span></span>

<span data-ttu-id="8f1eb-104">Dans ce didacticiel, vous apprendrez comment toointegrate BenefitHub avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8f1eb-104">In this tutorial, you learn how toointegrate BenefitHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8f1eb-105">Intégration BenefitHub à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8f1eb-105">Integrating BenefitHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8f1eb-106">Vous pouvez contrôler dans Azure AD qui a accès tooBenefitHub</span><span class="sxs-lookup"><span data-stu-id="8f1eb-106">You can control in Azure AD who has access tooBenefitHub</span></span>
- <span data-ttu-id="8f1eb-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBenefitHub (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f1eb-107">You can enable your users tooautomatically get signed-on tooBenefitHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8f1eb-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8f1eb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8f1eb-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8f1eb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f1eb-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8f1eb-110">Prerequisites</span></span>

<span data-ttu-id="8f1eb-111">tooconfigure intégration d’Azure AD avec BenefitHub, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8f1eb-111">tooconfigure Azure AD integration with BenefitHub, you need hello following items:</span></span>

- <span data-ttu-id="8f1eb-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f1eb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8f1eb-113">Un abonnement BenefitHub pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8f1eb-113">A BenefitHub single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8f1eb-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8f1eb-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="8f1eb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8f1eb-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8f1eb-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f1eb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8f1eb-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8f1eb-118">Scenario description</span></span>
<span data-ttu-id="8f1eb-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8f1eb-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="8f1eb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8f1eb-121">Ajout de BenefitHub à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8f1eb-121">Adding BenefitHub from hello gallery</span></span>
2. <span data-ttu-id="8f1eb-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f1eb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benefithub-from-hello-gallery"></a><span data-ttu-id="8f1eb-123">Ajout de BenefitHub à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8f1eb-123">Adding BenefitHub from hello gallery</span></span>
<span data-ttu-id="8f1eb-124">intégration de hello tooconfigure de BenefitHub dans Azure AD, vous devez tooadd BenefitHub à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-124">tooconfigure hello integration of BenefitHub into Azure AD, you need tooadd BenefitHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8f1eb-125">**tooadd BenefitHub à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8f1eb-125">**tooadd BenefitHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f1eb-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8f1eb-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8f1eb-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8f1eb-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8f1eb-133">Dans la zone de recherche de hello, tapez **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-133">In hello search box, type **BenefitHub**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_search.png)

5. <span data-ttu-id="8f1eb-135">Dans le volet de résultats hello, sélectionnez **BenefitHub**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-135">In hello results panel, select **BenefitHub**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8f1eb-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f1eb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8f1eb-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec BenefitHub avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8f1eb-138">In this section, you configure and test Azure AD single sign-on with BenefitHub based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8f1eb-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans BenefitHub est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BenefitHub is tooa user in Azure AD.</span></span> <span data-ttu-id="8f1eb-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans BenefitHub doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-140">In other words, a link relationship between an Azure AD user and hello related user in BenefitHub needs toobe established.</span></span>

<span data-ttu-id="8f1eb-141">Dans BenefitHub, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-141">In BenefitHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8f1eb-142">tooconfigure et test Azure AD l’authentification unique avec BenefitHub, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="8f1eb-142">tooconfigure and test Azure AD single sign-on with BenefitHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8f1eb-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8f1eb-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8f1eb-145">**[Création d’un utilisateur de test BenefitHub](#creating-a-benefithub-test-user)**  -toohave un équivalent de Britta Simon dans BenefitHub est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-145">**[Creating a BenefitHub test user](#creating-a-benefithub-test-user)** - toohave a counterpart of Britta Simon in BenefitHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8f1eb-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8f1eb-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8f1eb-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f1eb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8f1eb-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BenefitHub application.</span></span>

<span data-ttu-id="8f1eb-150">**tooconfigure Azure AD single sign-on avec BenefitHub, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8f1eb-150">**tooconfigure Azure AD single sign-on with BenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f1eb-151">Bonjour portail Azure, sur hello **BenefitHub** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-151">In hello Azure portal, on hello **BenefitHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8f1eb-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_samlbase.png)

3. <span data-ttu-id="8f1eb-155">Sur hello **BenefitHub domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8f1eb-155">On hello **BenefitHub Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_url1.png)
  
    <span data-ttu-id="8f1eb-157">a.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-157">a.</span></span> <span data-ttu-id="8f1eb-158">Bonjour **identificateur** zone de texte, type :`urn:benefithub:passport`</span><span class="sxs-lookup"><span data-stu-id="8f1eb-158">In hello **Identifier** textbox, type: `urn:benefithub:passport`</span></span>
    
    <span data-ttu-id="8f1eb-159">b.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-159">b.</span></span> <span data-ttu-id="8f1eb-160">Bonjour **URL de réponse** zone de texte, type :`https://passport.benefithub.info/saml/post/ac`</span><span class="sxs-lookup"><span data-stu-id="8f1eb-160">In hello **Reply URL** textbox, type: `https://passport.benefithub.info/saml/post/ac`</span></span>

4. <span data-ttu-id="8f1eb-161">Hello BenefitHub application attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-161">hello BenefitHub application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="8f1eb-162">Configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-162">Configure hello following claims for this application.</span></span> <span data-ttu-id="8f1eb-163">Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-163">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_attribute.png)

5. <span data-ttu-id="8f1eb-165">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans hello précédant l’image et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8f1eb-165">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="8f1eb-166">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="8f1eb-166">Attribute Name</span></span> | <span data-ttu-id="8f1eb-167">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="8f1eb-167">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="8f1eb-168">organizationid</span><span class="sxs-lookup"><span data-stu-id="8f1eb-168">organizationid</span></span> | <span data-ttu-id="8f1eb-169">< organizationid ></span><span class="sxs-lookup"><span data-stu-id="8f1eb-169">< organizationid ></span></span> |

    > [!NOTE]
    > <span data-ttu-id="8f1eb-170">Cette valeur d’attribut n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-170">This attribute value is not real.</span></span> <span data-ttu-id="8f1eb-171">Remplacez cette valeur par la valeur réelle d’organizationid.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-171">Update this value with actual organizationid.</span></span> <span data-ttu-id="8f1eb-172">Contact [équipe de support BenefitHub](https://www.benefithub.com/Home/ContactUs) tooget hello organizationid réel.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-172">Contact [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) tooget hello actual organizationid.</span></span>
    
    <span data-ttu-id="8f1eb-173">a.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-173">a.</span></span> <span data-ttu-id="8f1eb-174">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-174">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="8f1eb-177">b.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-177">b.</span></span> <span data-ttu-id="8f1eb-178">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-178">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="8f1eb-179">c.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-179">c.</span></span> <span data-ttu-id="8f1eb-180">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-180">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8f1eb-181">d.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-181">d.</span></span> <span data-ttu-id="8f1eb-182">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-182">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8f1eb-183">Avant de pouvoir configurer assertion SAML de hello, vous devez toocontact votre [prise en charge BenefitHub](https://www.benefithub.com/Home/ContactUs) et demander la valeur hello d’attribut d’identificateur unique hello pour votre client.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-183">Before you can configure hello SAML assertion, you need toocontact your [BenefitHub support](https://www.benefithub.com/Home/ContactUs) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="8f1eb-184">Vous avez besoin de cette revendication personnalisée hello valeur tooconfigure pour votre application.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-184">You need this value tooconfigure hello custom claim for your application.</span></span>

6. <span data-ttu-id="8f1eb-185">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-185">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_certificate.png) 

7. <span data-ttu-id="8f1eb-187">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8f1eb-187">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8f1eb-189">tooconfigure l’authentification unique sur **BenefitHub** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support BenefitHub](https://www.benefithub.com/Home/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="8f1eb-189">tooconfigure single sign-on on **BenefitHub** side, you need toosend hello downloaded **Metadata XML** too[BenefitHub support team](https://www.benefithub.com/Home/ContactUs).</span></span> <span data-ttu-id="8f1eb-190">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-190">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8f1eb-191">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="8f1eb-191">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8f1eb-192">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-192">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8f1eb-193">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8f1eb-193">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8f1eb-194">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f1eb-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="8f1eb-195">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-195">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8f1eb-197">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8f1eb-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f1eb-198">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-198">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8f1eb-200">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-200">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8f1eb-202">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-202">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8f1eb-204">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8f1eb-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benefithub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8f1eb-206">a.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-206">a.</span></span> <span data-ttu-id="8f1eb-207">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8f1eb-208">b.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-208">b.</span></span> <span data-ttu-id="8f1eb-209">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8f1eb-210">c.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-210">c.</span></span> <span data-ttu-id="8f1eb-211">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8f1eb-212">d.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-212">d.</span></span> <span data-ttu-id="8f1eb-213">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-213">Click **Create**.</span></span>
 
### <a name="creating-a-benefithub-test-user"></a><span data-ttu-id="8f1eb-214">Création d’un utilisateur de test BenefitHub</span><span class="sxs-lookup"><span data-stu-id="8f1eb-214">Creating a BenefitHub test user</span></span>

<span data-ttu-id="8f1eb-215">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans BenefitHub.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-215">In this section, you create a user called Britta Simon in BenefitHub.</span></span> <span data-ttu-id="8f1eb-216">Travailler avec [équipe de support BenefitHub](https://www.benefithub.com/Home/ContactUs) pour ajouter des utilisateurs de hello de plateforme de BenefitHub hello.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-216">Work with [BenefitHub support team](https://www.benefithub.com/Home/ContactUs) to add hello users in hello BenefitHub platform.</span></span> <span data-ttu-id="8f1eb-217">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-217">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8f1eb-218">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8f1eb-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8f1eb-219">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooBenefitHub.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBenefitHub.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8f1eb-221">**tooassign Britta Simon tooBenefitHub, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8f1eb-221">**tooassign Britta Simon tooBenefitHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="8f1eb-222">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8f1eb-224">Dans la liste des applications hello, sélectionnez **BenefitHub**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-224">In hello applications list, select **BenefitHub**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benefithub-tutorial/tutorial_benefithub_app.png) 

3. <span data-ttu-id="8f1eb-226">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8f1eb-228">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-228">Click **Add** button.</span></span> <span data-ttu-id="8f1eb-229">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8f1eb-231">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8f1eb-232">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8f1eb-233">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8f1eb-234">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8f1eb-234">Testing single sign-on</span></span>

<span data-ttu-id="8f1eb-235">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8f1eb-236">Lorsque vous cliquez sur mosaïque BenefitHub hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour BenefitHub application.</span><span class="sxs-lookup"><span data-stu-id="8f1eb-236">When you click hello BenefitHub tile in hello Access Panel, you should get automatically signed-on tooyour BenefitHub application.</span></span>
<span data-ttu-id="8f1eb-237">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="8f1eb-237">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f1eb-238">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8f1eb-238">Additional resources</span></span>

* [<span data-ttu-id="8f1eb-239">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8f1eb-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8f1eb-240">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8f1eb-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benefithub-tutorial/tutorial_general_203.png

