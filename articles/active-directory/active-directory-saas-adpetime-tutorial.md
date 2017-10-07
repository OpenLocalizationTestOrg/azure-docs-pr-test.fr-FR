---
title: "Didacticiel : Intégration d’Azure Active Directory à ADP eTime | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et ADP eTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a5c7d14a18220f8c7a5b14055c30662ecd8f14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="d8b59-103">Didacticiel : Intégration d’Azure AD à ADP eTime</span><span class="sxs-lookup"><span data-stu-id="d8b59-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="d8b59-104">Dans ce didacticiel, vous apprendrez comment eTime toointegrate ADP avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d8b59-104">In this tutorial, you learn how toointegrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d8b59-105">Intégration ADP eTime à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d8b59-105">Integrating ADP eTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d8b59-106">Vous pouvez contrôler dans Azure AD qui a accès tooADP eTime</span><span class="sxs-lookup"><span data-stu-id="d8b59-106">You can control in Azure AD who has access tooADP eTime</span></span>
- <span data-ttu-id="d8b59-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooADP eTime (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8b59-107">You can enable your users tooautomatically get signed-on tooADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d8b59-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d8b59-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d8b59-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d8b59-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8b59-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d8b59-110">Prerequisites</span></span>

<span data-ttu-id="d8b59-111">tooconfigure intégration d’Azure AD avec ADP eTime, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d8b59-111">tooconfigure Azure AD integration with ADP eTime, you need hello following items:</span></span>

- <span data-ttu-id="d8b59-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8b59-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d8b59-113">Un abonnement ADP eTime pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d8b59-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d8b59-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d8b59-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d8b59-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="d8b59-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d8b59-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d8b59-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d8b59-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8b59-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d8b59-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d8b59-118">Scenario description</span></span>
<span data-ttu-id="d8b59-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d8b59-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d8b59-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="d8b59-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d8b59-121">Ajout de ADP eTime à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d8b59-121">Adding ADP eTime from hello gallery</span></span>
2. <span data-ttu-id="d8b59-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8b59-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-hello-gallery"></a><span data-ttu-id="d8b59-123">Ajout de ADP eTime à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d8b59-123">Adding ADP eTime from hello gallery</span></span>
<span data-ttu-id="d8b59-124">tooconfigure hello intégration de ADP eTime dans Azure AD, vous devez eTime de ADP tooadd à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d8b59-124">tooconfigure hello integration of ADP eTime into Azure AD, you need tooadd ADP eTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d8b59-125">**eTime tooadd ADP à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d8b59-125">**tooadd ADP eTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8b59-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d8b59-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d8b59-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d8b59-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d8b59-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d8b59-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d8b59-133">Dans la zone de recherche de hello, tapez **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-133">In hello search box, type **ADP eTime**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="d8b59-135">Dans le volet de résultats hello, sélectionnez **ADP eTime**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d8b59-135">In hello results panel, select **ADP eTime**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d8b59-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8b59-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d8b59-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ADP eTime, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d8b59-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d8b59-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello ADP eTime est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8b59-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP eTime is tooa user in Azure AD.</span></span> <span data-ttu-id="d8b59-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ADP eTime doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="d8b59-140">In other words, a link relationship between an Azure AD user and hello related user in ADP eTime needs toobe established.</span></span>

<span data-ttu-id="d8b59-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="d8b59-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP eTime.</span></span>

<span data-ttu-id="d8b59-142">tooconfigure et test Azure AD l’authentification unique avec ADP eTime, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="d8b59-142">tooconfigure and test Azure AD single sign-on with ADP eTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d8b59-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d8b59-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d8b59-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d8b59-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d8b59-145">**[Création d’un utilisateur de test eTime ADP](#creating-an-adp-etime-test-user)**  -toohave un homologue de Britta Simon dans eTime ADP qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d8b59-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - toohave a counterpart of Britta Simon in ADP eTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d8b59-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d8b59-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d8b59-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="d8b59-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d8b59-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8b59-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d8b59-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application d’eTime ADP.</span><span class="sxs-lookup"><span data-stu-id="d8b59-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="d8b59-150">**tooconfigure Azure AD single sign-on avec ADP eTime, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d8b59-150">**tooconfigure Azure AD single sign-on with ADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8b59-151">Bonjour portail Azure, sur hello **ADP eTime** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-151">In hello Azure portal, on hello **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d8b59-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d8b59-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="d8b59-155">Sur hello **ADP eTime domaine et les URL** section, effectuer hello suivant l’étape :</span><span class="sxs-lookup"><span data-stu-id="d8b59-155">On hello **ADP eTime Domain and URLs** section, perform hello following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="d8b59-157">a.</span><span class="sxs-lookup"><span data-stu-id="d8b59-157">a.</span></span> <span data-ttu-id="d8b59-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="d8b59-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="d8b59-159">b.</span><span class="sxs-lookup"><span data-stu-id="d8b59-159">b.</span></span> <span data-ttu-id="d8b59-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="d8b59-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="d8b59-161">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="d8b59-161">These values are not hello real.</span></span> <span data-ttu-id="d8b59-162">Mettre à jour ces valeurs avec l’URL de réponse réelle hello et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="d8b59-162">Update these values with hello actual Reply URL and Identifier.</span></span> <span data-ttu-id="d8b59-163">Contact [équipe de support ADP eTime](https://www.adp.com/contact-us/overview.aspx) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="d8b59-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooget these values.</span></span>

4. <span data-ttu-id="d8b59-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d8b59-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="d8b59-166">Hello application eTime de ADP attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages.</span><span class="sxs-lookup"><span data-stu-id="d8b59-166">hello ADP eTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="d8b59-167">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="d8b59-167">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="d8b59-168">Hello nom de la revendication sera toujours **« PersonImmutableID »** et valeur hello dont nous avons mappé tooExtensionAttribute2 contenant hello EmployeeID d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="d8b59-168">hello claim name will always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2 which contains hello EmployeeID of hello user.</span></span> 

    <span data-ttu-id="d8b59-169">Mappage de l’utilisateur à partir d’Azure AD tooADP eTime hello est effectuée sur hello EmployeeID ici, mais vous pouvez mapper cette valeur différents tooa également en fonction de vos paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="d8b59-169">Here hello user mapping from Azure AD tooADP eTime will be done on hello EmployeeID but you can map this tooa different value also based on your application settings.</span></span> <span data-ttu-id="d8b59-170">Veuillez travail avec [équipe de support ADP eTime](https://www.adp.com/contact-us/overview.aspx) toouse premier hello identificateur correct d’un utilisateur et mapper cette valeur avec hello **« PersonImmutableID »** de revendication.</span><span class="sxs-lookup"><span data-stu-id="d8b59-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="d8b59-172">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image de hello et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d8b59-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="d8b59-173">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="d8b59-173">Attribute Name</span></span> | <span data-ttu-id="d8b59-174">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="d8b59-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="d8b59-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="d8b59-175">PersonImmutableID</span></span> | <span data-ttu-id="d8b59-176">user.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="d8b59-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="d8b59-177">a.</span><span class="sxs-lookup"><span data-stu-id="d8b59-177">a.</span></span> <span data-ttu-id="d8b59-178">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d8b59-178">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="d8b59-181">b.</span><span class="sxs-lookup"><span data-stu-id="d8b59-181">b.</span></span> <span data-ttu-id="d8b59-182">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="d8b59-182">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="d8b59-183">c.</span><span class="sxs-lookup"><span data-stu-id="d8b59-183">c.</span></span> <span data-ttu-id="d8b59-184">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="d8b59-184">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d8b59-185">d.</span><span class="sxs-lookup"><span data-stu-id="d8b59-185">d.</span></span> <span data-ttu-id="d8b59-186">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d8b59-187">Avant de pouvoir configurer assertion SAML de hello, vous devez toocontact votre [équipe de support ADP eTime](https://www.adp.com/contact-us/overview.aspx) et demander la valeur hello d’attribut d’identificateur unique hello pour votre client.</span><span class="sxs-lookup"><span data-stu-id="d8b59-187">Before you can configure hello SAML assertion, you need toocontact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="d8b59-188">Vous avez besoin de cette revendication personnalisée hello valeur tooconfigure pour votre application.</span><span class="sxs-lookup"><span data-stu-id="d8b59-188">You need this value tooconfigure hello custom claim for your application.</span></span> 

7. <span data-ttu-id="d8b59-189">Sur hello **ADP eTime Configuration** , cliquez sur **configurer un ADP eTime** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d8b59-189">On hello **ADP eTime Configuration** section, click **Configure ADP eTime** tooopen **Configure sign-on** window.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="d8b59-191">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d8b59-191">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="d8b59-193">tooconfigure l’authentification unique sur **ADP eTime** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support ADP eTime](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8b59-193">tooconfigure single sign-on on **ADP eTime** side, you need toosend hello downloaded **Metadata XML** too[ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="d8b59-194">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="d8b59-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d8b59-195">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="d8b59-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d8b59-196">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d8b59-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d8b59-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8b59-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="d8b59-198">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="d8b59-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d8b59-200">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d8b59-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8b59-201">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d8b59-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d8b59-203">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d8b59-205">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="d8b59-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d8b59-207">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d8b59-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d8b59-209">a.</span><span class="sxs-lookup"><span data-stu-id="d8b59-209">a.</span></span> <span data-ttu-id="d8b59-210">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d8b59-211">b.</span><span class="sxs-lookup"><span data-stu-id="d8b59-211">b.</span></span> <span data-ttu-id="d8b59-212">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d8b59-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d8b59-213">c.</span><span class="sxs-lookup"><span data-stu-id="d8b59-213">c.</span></span> <span data-ttu-id="d8b59-214">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d8b59-215">d.</span><span class="sxs-lookup"><span data-stu-id="d8b59-215">d.</span></span> <span data-ttu-id="d8b59-216">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="d8b59-217">Création d’un utilisateur test ADP eTime</span><span class="sxs-lookup"><span data-stu-id="d8b59-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="d8b59-218">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="d8b59-218">hello objective of this section is toocreate a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="d8b59-219">Travailler avec [équipe de support ADP eTime](https://www.adp.com/contact-us/overview.aspx) utilisateurs hello tooadd compte d’eTime hello ADP.</span><span class="sxs-lookup"><span data-stu-id="d8b59-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP eTime account.</span></span> 
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d8b59-220">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8b59-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d8b59-221">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooADP eTime.</span><span class="sxs-lookup"><span data-stu-id="d8b59-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP eTime.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d8b59-223">**tooassign Britta Simon tooADP eTime, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d8b59-223">**tooassign Britta Simon tooADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8b59-224">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d8b59-226">Dans la liste des applications hello, sélectionnez **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-226">In hello applications list, select **ADP eTime**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="d8b59-228">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d8b59-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-230">Click **Add** button.</span></span> <span data-ttu-id="d8b59-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d8b59-233">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="d8b59-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d8b59-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d8b59-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d8b59-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d8b59-236">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d8b59-236">Testing single sign-on</span></span>

<span data-ttu-id="d8b59-237">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="d8b59-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d8b59-238">Lorsque vous cliquez sur mosaïque eTime hello ADP hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour ADP eTime application.</span><span class="sxs-lookup"><span data-stu-id="d8b59-238">When you click hello ADP eTime tile in hello Access Panel, you should get automatically signed-on tooyour ADP eTime application.</span></span>
<span data-ttu-id="d8b59-239">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d8b59-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d8b59-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d8b59-240">Additional resources</span></span>

* [<span data-ttu-id="d8b59-241">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8b59-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d8b59-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d8b59-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

