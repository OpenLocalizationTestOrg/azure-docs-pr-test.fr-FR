---
title: "Didacticiel : Intégration d’ADP GlobalView à Azure Active Directory | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et ADP Globalview."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: aee2d56f05b486d12facbc41c9503455094604ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="8de39-103">Didacticiel : Intégration d’ADP GlobalView à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8de39-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="8de39-104">Dans ce didacticiel, vous apprendrez comment toointegrate ADP Globalview avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8de39-104">In this tutorial, you learn how toointegrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8de39-105">Intégration ADP Globalview à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8de39-105">Integrating ADP Globalview with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8de39-106">Vous pouvez contrôler dans Azure AD qui a accès tooADP Globalview</span><span class="sxs-lookup"><span data-stu-id="8de39-106">You can control in Azure AD who has access tooADP Globalview</span></span>
- <span data-ttu-id="8de39-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooADP Globalview (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="8de39-107">You can enable your users tooautomatically get signed-on tooADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8de39-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8de39-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8de39-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8de39-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8de39-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8de39-110">Prerequisites</span></span>

<span data-ttu-id="8de39-111">tooconfigure intégration d’Azure AD avec ADP Globalview, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8de39-111">tooconfigure Azure AD integration with ADP Globalview, you need hello following items:</span></span>

- <span data-ttu-id="8de39-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8de39-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8de39-113">Un abonnement ADP GlobalView pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8de39-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8de39-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8de39-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8de39-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="8de39-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8de39-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8de39-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8de39-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8de39-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8de39-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8de39-118">Scenario description</span></span>
<span data-ttu-id="8de39-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8de39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8de39-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="8de39-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8de39-121">Ajout de ADP Globalview à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8de39-121">Adding ADP Globalview from hello gallery</span></span>
2. <span data-ttu-id="8de39-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8de39-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-hello-gallery"></a><span data-ttu-id="8de39-123">Ajout de ADP Globalview à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="8de39-123">Adding ADP Globalview from hello gallery</span></span>
<span data-ttu-id="8de39-124">tooconfigure hello intégration de ADP Globalview dans Azure AD, vous devez tooadd ADP Globalview à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8de39-124">tooconfigure hello integration of ADP Globalview into Azure AD, you need tooadd ADP Globalview from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8de39-125">**tooadd ADP Globalview à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8de39-125">**tooadd ADP Globalview from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8de39-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8de39-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8de39-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8de39-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8de39-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8de39-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8de39-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8de39-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8de39-133">Dans la zone de recherche de hello, tapez **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="8de39-133">In hello search box, type **ADP Globalview**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="8de39-135">Dans le volet de résultats hello, sélectionnez **ADP Globalview**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="8de39-135">In hello results panel, select **ADP Globalview**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8de39-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8de39-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8de39-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ADP GlobalView avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8de39-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8de39-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello ADP Globalview est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8de39-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP Globalview is tooa user in Azure AD.</span></span> <span data-ttu-id="8de39-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ADP Globalview doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="8de39-140">In other words, a link relationship between an Azure AD user and hello related user in ADP Globalview needs toobe established.</span></span>

<span data-ttu-id="8de39-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="8de39-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP Globalview.</span></span>

<span data-ttu-id="8de39-142">tooconfigure et test Azure AD l’authentification unique avec ADP Globalview, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="8de39-142">tooconfigure and test Azure AD single sign-on with ADP Globalview, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8de39-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8de39-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8de39-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8de39-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8de39-145">**[Création d’un utilisateur de test ADP Globalview](#creating-an-adp-globalview-test-user)**  -toohave un équivalent de Britta Simon dans ADP Globalview qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8de39-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - toohave a counterpart of Britta Simon in ADP Globalview that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8de39-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8de39-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8de39-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="8de39-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8de39-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8de39-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8de39-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="8de39-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="8de39-150">**tooconfigure Azure AD single sign-on avec ADP Globalview, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8de39-150">**tooconfigure Azure AD single sign-on with ADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="8de39-151">Bonjour portail Azure, sur hello **ADP Globalview** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8de39-151">In hello Azure portal, on hello **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8de39-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8de39-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="8de39-155">Sur hello **ADP Globalview domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8de39-155">On hello **ADP Globalview Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="8de39-157">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle : `https://<subdomain>.globalview.adp.com/federate` ou`https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="8de39-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8de39-158">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="8de39-158">hello value is not real.</span></span> <span data-ttu-id="8de39-159">Mettre à jour la valeur de hello avec hello identificateur réel.</span><span class="sxs-lookup"><span data-stu-id="8de39-159">Update hello value with hello actual Identifier.</span></span> <span data-ttu-id="8de39-160">Contact [prise en charge ADP Globalview](https://www.adp.com/contact-us/overview.aspx) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="8de39-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooget hello value.</span></span>
 
4. <span data-ttu-id="8de39-161">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8de39-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="8de39-163">Hello ADP GlobalView application attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages.</span><span class="sxs-lookup"><span data-stu-id="8de39-163">hello ADP GlobalView application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="8de39-164">Hello suivant capture d’écran montre un exemple pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="8de39-164">hello following screenshot shows an example for it.</span></span> <span data-ttu-id="8de39-165">Hello revendication toujours porter **« PersonImmutableID »** et valeur hello dont nous avons mappé tooExtensionAttribute2, lequel contient hello EmployeeID d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="8de39-165">hello claim names always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2, which contains hello EmployeeID of hello user.</span></span> <span data-ttu-id="8de39-166">Mappage de l’utilisateur à partir d’Azure AD tooADP GlobalView hello est effectuée sur hello EmployeeID ici, mais vous pouvez mapper tooa autre valeur est également basé sur les paramètres de votre application.</span><span class="sxs-lookup"><span data-stu-id="8de39-166">Here hello user mapping from Azure AD tooADP GlobalView is done on hello EmployeeID but you can map it tooa different value also based on your application settings.</span></span> <span data-ttu-id="8de39-167">Vous pouvez utiliser hello ADP GlobalView équipe premier toouse hello identificateur correct d’un utilisateur et mapper cette valeur avec hello **« PersonImmutableID »** de revendication.</span><span class="sxs-lookup"><span data-stu-id="8de39-167">You can work with hello ADP GlobalView team first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="8de39-168">Vous pouvez également mapper la revendication d’E-mail et UserID hello comme indiqué dans l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="8de39-168">You can also map hello Email and UserID claim as shown in hello picture.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="8de39-170">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image de hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8de39-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="8de39-171">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="8de39-171">Attribute Name</span></span> | <span data-ttu-id="8de39-172">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="8de39-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="8de39-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="8de39-173">personalimmutableid</span></span> | <span data-ttu-id="8de39-174">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="8de39-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="8de39-175">email</span><span class="sxs-lookup"><span data-stu-id="8de39-175">email</span></span>               | <span data-ttu-id="8de39-176">user.mail</span><span class="sxs-lookup"><span data-stu-id="8de39-176">user.mail</span></span> |
    | <span data-ttu-id="8de39-177">userId</span><span class="sxs-lookup"><span data-stu-id="8de39-177">userid</span></span>              | <span data-ttu-id="8de39-178">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="8de39-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="8de39-179">a.</span><span class="sxs-lookup"><span data-stu-id="8de39-179">a.</span></span> <span data-ttu-id="8de39-180">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8de39-180">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="8de39-183">b.</span><span class="sxs-lookup"><span data-stu-id="8de39-183">b.</span></span> <span data-ttu-id="8de39-184">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="8de39-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="8de39-185">c.</span><span class="sxs-lookup"><span data-stu-id="8de39-185">c.</span></span> <span data-ttu-id="8de39-186">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="8de39-186">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="8de39-187">d.</span><span class="sxs-lookup"><span data-stu-id="8de39-187">d.</span></span> <span data-ttu-id="8de39-188">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8de39-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8de39-189">Avant de pouvoir configurer assertion SAML de hello, vous devez toocontact votre [prise en charge ADP Globalview](https://www.adp.com/contact-us/overview.aspx) et demander la valeur hello d’attribut d’identificateur unique hello pour votre client.</span><span class="sxs-lookup"><span data-stu-id="8de39-189">Before you can configure hello SAML assertion, you need toocontact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="8de39-190">Vous avez besoin de cette revendication personnalisée hello valeur tooconfigure pour votre application.</span><span class="sxs-lookup"><span data-stu-id="8de39-190">You need this value tooconfigure hello custom claim for your application.</span></span> 

8. <span data-ttu-id="8de39-191">Sur hello **ADP Globalview Configuration** , cliquez sur **Globalview de ADP configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="8de39-191">On hello **ADP Globalview Configuration** section, click **Configure ADP Globalview** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8de39-192">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="8de39-192">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="8de39-194">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8de39-194">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="8de39-196">tooconfigure l’authentification unique sur **ADP Globalview** côté, vous devez hello toosend téléchargé **certificat (Base64)**, **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** trop[prise en charge ADP Globalview](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="8de39-196">tooconfigure single sign-on on **ADP Globalview** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="8de39-197">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="8de39-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8de39-198">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="8de39-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8de39-199">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8de39-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8de39-200">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8de39-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="8de39-201">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="8de39-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8de39-203">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8de39-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8de39-204">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="8de39-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="8de39-206">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8de39-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8de39-208">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="8de39-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8de39-210">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8de39-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8de39-212">a.</span><span class="sxs-lookup"><span data-stu-id="8de39-212">a.</span></span> <span data-ttu-id="8de39-213">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8de39-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8de39-214">b.</span><span class="sxs-lookup"><span data-stu-id="8de39-214">b.</span></span> <span data-ttu-id="8de39-215">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8de39-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8de39-216">c.</span><span class="sxs-lookup"><span data-stu-id="8de39-216">c.</span></span> <span data-ttu-id="8de39-217">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8de39-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8de39-218">d.</span><span class="sxs-lookup"><span data-stu-id="8de39-218">d.</span></span> <span data-ttu-id="8de39-219">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8de39-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="8de39-220">Création d’un utilisateur de test ADP GlobalView</span><span class="sxs-lookup"><span data-stu-id="8de39-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="8de39-221">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="8de39-221">hello objective of this section is toocreate a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="8de39-222">Travailler avec [prise en charge ADP Globalview](https://www.adp.com/contact-us/overview.aspx) utilisateurs hello tooadd hello ADP GlobalView compte.</span><span class="sxs-lookup"><span data-stu-id="8de39-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP GlobalView account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8de39-223">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8de39-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8de39-224">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="8de39-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP Globalview.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8de39-226">**tooassign Britta Simon tooADP Globalview, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8de39-226">**tooassign Britta Simon tooADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="8de39-227">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8de39-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8de39-229">Dans la liste des applications hello, sélectionnez **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="8de39-229">In hello applications list, select **ADP Globalview**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="8de39-231">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8de39-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8de39-233">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8de39-233">Click **Add** button.</span></span> <span data-ttu-id="8de39-234">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8de39-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8de39-236">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="8de39-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8de39-237">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8de39-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8de39-238">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8de39-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8de39-239">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8de39-239">Testing single sign-on</span></span>

<span data-ttu-id="8de39-240">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="8de39-240">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="8de39-241">Lorsque vous cliquez sur hello ADP GlobalView vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour ADP GlobalView application.</span><span class="sxs-lookup"><span data-stu-id="8de39-241">When you click hello ADP GlobalView tile in hello Access Panel, you should get automatically signed-on tooyour ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8de39-242">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8de39-242">Additional resources</span></span>

* [<span data-ttu-id="8de39-243">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8de39-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8de39-244">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8de39-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

