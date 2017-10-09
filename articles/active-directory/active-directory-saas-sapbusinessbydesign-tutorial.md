---
title: "Didacticiel : intégration d’Azure Active Directory à SAP Business ByDesign | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et SAP Business ByDesign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: c14714fd27f8d7fc555f25c7be83fad2b0d7f333
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="e1be6-103">Didacticiel : Intégration d’Azure Active Directory à SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="e1be6-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="e1be6-104">Dans ce didacticiel, vous apprendrez comment toointegrate SAP ByDesign d’entreprise avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e1be6-104">In this tutorial, you learn how toointegrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e1be6-105">Intégration de SAP Business ByDesign avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e1be6-105">Integrating SAP Business ByDesign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e1be6-106">Vous pouvez contrôler dans Azure AD qui a accès tooSAP ByDesign de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="e1be6-106">You can control in Azure AD who has access tooSAP Business ByDesign.</span></span>
- <span data-ttu-id="e1be6-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSAP ByDesign entreprise (SSO) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1be6-107">You can enable your users tooautomatically get signed-on tooSAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e1be6-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e1be6-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e1be6-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e1be6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e1be6-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e1be6-110">Prerequisites</span></span>

<span data-ttu-id="e1be6-111">tooconfigure intégration d’Azure AD avec SAP Business ByDesign, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e1be6-111">tooconfigure Azure AD integration with SAP Business ByDesign, you need hello following items:</span></span>

- <span data-ttu-id="e1be6-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1be6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e1be6-113">Un abonnement SAP Business ByDesign pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="e1be6-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e1be6-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e1be6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e1be6-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="e1be6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e1be6-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e1be6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e1be6-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1be6-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e1be6-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e1be6-118">Scenario description</span></span>
<span data-ttu-id="e1be6-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e1be6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e1be6-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="e1be6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e1be6-121">Ajout de SAP Business ByDesign à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e1be6-121">Adding SAP Business ByDesign from hello gallery</span></span>
2. <span data-ttu-id="e1be6-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1be6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-hello-gallery"></a><span data-ttu-id="e1be6-123">Ajout de SAP Business ByDesign à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e1be6-123">Adding SAP Business ByDesign from hello gallery</span></span>
<span data-ttu-id="e1be6-124">tooconfigure hello intégration de SAP Business ByDesign dans Azure AD, vous devez tooadd SAP Business ByDesign à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="e1be6-124">tooconfigure hello integration of SAP Business ByDesign into Azure AD, you need tooadd SAP Business ByDesign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e1be6-125">**tooadd ByDesign d’entreprise SAP à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e1be6-125">**tooadd SAP Business ByDesign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1be6-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e1be6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="e1be6-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e1be6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e1be6-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e1be6-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="e1be6-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e1be6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="e1be6-133">Dans la zone de recherche de hello, tapez **SAP Business ByDesign**, sélectionnez **SAP Business ByDesign** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e1be6-133">In hello search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ByDesign d’entreprise SAP dans la liste des résultats hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e1be6-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1be6-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e1be6-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP Business ByDesign, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e1be6-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e1be6-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SAP Business ByDesign est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e1be6-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Business ByDesign is tooa user in Azure AD.</span></span> <span data-ttu-id="e1be6-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans SAP Business ByDesign doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="e1be6-138">In other words, a link relationship between an Azure AD user and hello related user in SAP Business ByDesign needs toobe established.</span></span>

<span data-ttu-id="e1be6-139">Dans SAP Business ByDesign, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="e1be6-139">In SAP Business ByDesign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e1be6-140">tooconfigure et test Azure AD l’authentification unique avec SAP Business ByDesign, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="e1be6-140">tooconfigure and test Azure AD single sign-on with SAP Business ByDesign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e1be6-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e1be6-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e1be6-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1be6-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e1be6-143">**[Créer un utilisateur de test SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)**  -toohave un équivalent de Britta Simon dans SAP Business ByDesign qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e1be6-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - toohave a counterpart of Britta Simon in SAP Business ByDesign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e1be6-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e1be6-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e1be6-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="e1be6-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e1be6-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1be6-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e1be6-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="e1be6-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="e1be6-148">**tooconfigure Azure AD l’authentification unique avec SAP Business ByDesign, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e1be6-148">**tooconfigure Azure AD single sign-on with SAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1be6-149">Bonjour portail Azure, sur hello **SAP Business ByDesign** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e1be6-149">In hello Azure portal, on hello **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="e1be6-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e1be6-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="e1be6-153">Sur hello **URL et le domaine de SAP Business ByDesign** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e1be6-153">On hello **SAP Business ByDesign Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans la section Domaine et URL SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="e1be6-155">a.</span><span class="sxs-lookup"><span data-stu-id="e1be6-155">a.</span></span> <span data-ttu-id="e1be6-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="e1be6-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="e1be6-157">b.</span><span class="sxs-lookup"><span data-stu-id="e1be6-157">b.</span></span> <span data-ttu-id="e1be6-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="e1be6-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e1be6-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="e1be6-159">These values are not real.</span></span> <span data-ttu-id="e1be6-160">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="e1be6-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e1be6-161">Contact [équipe de support SAP Business ByDesign Client](https://www.sap.com/products/cloud-analytics.support.html) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="e1be6-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooget these values.</span></span>

4. <span data-ttu-id="e1be6-162">Sur hello **attributs utilisateur** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e1be6-162">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![Section d’attribut de SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="e1be6-164">a.</span><span class="sxs-lookup"><span data-stu-id="e1be6-164">a.</span></span> <span data-ttu-id="e1be6-165">Dans **identificateur de l’utilisateur** liste, sélectionnez hello **ExtractMailPrefix()** (fonction).</span><span class="sxs-lookup"><span data-stu-id="e1be6-165">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="e1be6-166">b.</span><span class="sxs-lookup"><span data-stu-id="e1be6-166">b.</span></span> <span data-ttu-id="e1be6-167">À partir de hello **Mail** liste, sélectionnez hello utilisateur attribut toouse pour votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="e1be6-167">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span> <span data-ttu-id="e1be6-168">Par exemple, si vous voulez toouse hello EmployeeID comme identificateur d’utilisateur unique et si vous avez stocké la valeur de l’attribut hello Bonjour ExtensionAttribute2, puis sélectionnez user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="e1be6-168">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>   

5. <span data-ttu-id="e1be6-169">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e1be6-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="e1be6-171">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e1be6-171">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="e1be6-173">Sur hello **SAP Business ByDesign Configuration** , cliquez sur **configurer de SAP Business ByDesign** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e1be6-173">On hello **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e1be6-174">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="e1be6-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration de SAP Business ByDesign](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="e1be6-176">tooget SSO configuré pour votre application, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e1be6-176">tooget SSO configured for your application, perform hello following steps:</span></span>
   
    <span data-ttu-id="e1be6-177">a.</span><span class="sxs-lookup"><span data-stu-id="e1be6-177">a.</span></span> <span data-ttu-id="e1be6-178">Se connecter sur le portail SAP Business ByDesign tooyour avec des droits d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e1be6-178">Sign on tooyour SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="e1be6-179">b.</span><span class="sxs-lookup"><span data-stu-id="e1be6-179">b.</span></span> <span data-ttu-id="e1be6-180">Accédez trop**Application et la tâche courante de gestion utilisateur** et cliquez sur hello **fournisseur d’identité** onglet.</span><span class="sxs-lookup"><span data-stu-id="e1be6-180">Navigate too**Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="e1be6-181">c.</span><span class="sxs-lookup"><span data-stu-id="e1be6-181">c.</span></span> <span data-ttu-id="e1be6-182">Cliquez sur **nouveau fournisseur d’identité** et le fichier XML de métadonnées hello select que vous avez téléchargé à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e1be6-182">Click **New Identity Provider** and select hello metadata XML file that you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="e1be6-183">En important des métadonnées de hello, système de hello télécharge automatiquement le certificat de signature requis hello et certificat de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="e1be6-183">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="e1be6-185">d.</span><span class="sxs-lookup"><span data-stu-id="e1be6-185">d.</span></span> <span data-ttu-id="e1be6-186">tooinclude hello **Assertion Consumer Service URL** dans la demande SAML hello, sélectionnez **inclure l’URL Assertion Consumer Service**.</span><span class="sxs-lookup"><span data-stu-id="e1be6-186">tooinclude hello **Assertion Consumer Service URL** into hello SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="e1be6-187">e.</span><span class="sxs-lookup"><span data-stu-id="e1be6-187">e.</span></span> <span data-ttu-id="e1be6-188">Cliquez sur **Activate Single Sign-On**(Activer l’authentification unique).</span><span class="sxs-lookup"><span data-stu-id="e1be6-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="e1be6-189">f.</span><span class="sxs-lookup"><span data-stu-id="e1be6-189">f.</span></span> <span data-ttu-id="e1be6-190">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="e1be6-190">Save your changes.</span></span>
   
    <span data-ttu-id="e1be6-191">g.</span><span class="sxs-lookup"><span data-stu-id="e1be6-191">g.</span></span> <span data-ttu-id="e1be6-192">Cliquez sur hello **mon système** onglet.</span><span class="sxs-lookup"><span data-stu-id="e1be6-192">Click hello **My System** tab.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="e1be6-194">h.</span><span class="sxs-lookup"><span data-stu-id="e1be6-194">h.</span></span> <span data-ttu-id="e1be6-195">Coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir de hello portail Azure il dans hello **Azure AD l’URL de connexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="e1be6-195">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal it into hello **Azure AD Sign On URL** textbox.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="e1be6-197">i.</span><span class="sxs-lookup"><span data-stu-id="e1be6-197">i.</span></span> <span data-ttu-id="e1be6-198">Spécifier si les employés hello peuvent manuellement choisir entre l’ouverture de session avec l’ID d’utilisateur et mot de passe ou l’authentification unique en sélectionnant **sélection de fournisseur d’identité manuelle**.</span><span class="sxs-lookup"><span data-stu-id="e1be6-198">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="e1be6-199">j.</span><span class="sxs-lookup"><span data-stu-id="e1be6-199">j.</span></span> <span data-ttu-id="e1be6-200">Bonjour **URL SSO** section, spécifier des URL hello qui doit être utilisée par le système de toohello toologon hello employé.</span><span class="sxs-lookup"><span data-stu-id="e1be6-200">In hello **SSO URL** section, specify hello URL that should be used by hello employee toologon toohello system.</span></span> 
    <span data-ttu-id="e1be6-201">Dans la liste de déroulante tooEmployee URL envoyée hello, vous pouvez choisir entre hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="e1be6-201">In hello URL Sent tooEmployee dropdown list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="e1be6-202">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="e1be6-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="e1be6-203">système de Hello envoie employé toohello hello uniquement des URL de normal du système.</span><span class="sxs-lookup"><span data-stu-id="e1be6-203">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="e1be6-204">employé de Hello ne peut pas se connecter à l’aide de l’authentification unique et doit utiliser le mot de passe ou de certificats à la place.</span><span class="sxs-lookup"><span data-stu-id="e1be6-204">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="e1be6-205">**URL SSO**</span><span class="sxs-lookup"><span data-stu-id="e1be6-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="e1be6-206">système de Hello envoie uniquement les employés de toohello URL SSO hello.</span><span class="sxs-lookup"><span data-stu-id="e1be6-206">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="e1be6-207">les employés Hello peuvent se connecter à l’aide de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e1be6-207">hello employee can log on using SSO.</span></span> <span data-ttu-id="e1be6-208">Demande d’authentification est redirigée via hello IdP.</span><span class="sxs-lookup"><span data-stu-id="e1be6-208">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="e1be6-209">**Sélection automatique**</span><span class="sxs-lookup"><span data-stu-id="e1be6-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="e1be6-210">Si l’authentification unique n’est pas actif, système de hello envoie employé de toohello URL hello normal du système.</span><span class="sxs-lookup"><span data-stu-id="e1be6-210">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="e1be6-211">Si l’authentification unique est actif, système de hello vérifie si les employés hello a un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="e1be6-211">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="e1be6-212">Si un mot de passe est disponible, les URL d’authentification unique et Non-SSO URL sont envoyées toohello employé.</span><span class="sxs-lookup"><span data-stu-id="e1be6-212">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="e1be6-213">Toutefois, si l’employé de hello n’a aucun mot de passe, uniquement hello URL d’authentification unique est envoyé toohello employé.</span><span class="sxs-lookup"><span data-stu-id="e1be6-213">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="e1be6-214">k.</span><span class="sxs-lookup"><span data-stu-id="e1be6-214">k.</span></span> <span data-ttu-id="e1be6-215">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="e1be6-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="e1be6-216">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="e1be6-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e1be6-217">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="e1be6-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e1be6-218">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e1be6-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e1be6-219">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1be6-219">Create an Azure AD test user</span></span>

<span data-ttu-id="e1be6-220">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="e1be6-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="e1be6-222">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e1be6-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1be6-223">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="e1be6-223">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e1be6-225">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e1be6-225">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e1be6-227">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e1be6-227">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e1be6-229">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e1be6-229">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e1be6-231">a.</span><span class="sxs-lookup"><span data-stu-id="e1be6-231">a.</span></span> <span data-ttu-id="e1be6-232">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e1be6-232">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e1be6-233">b.</span><span class="sxs-lookup"><span data-stu-id="e1be6-233">b.</span></span> <span data-ttu-id="e1be6-234">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e1be6-234">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e1be6-235">c.</span><span class="sxs-lookup"><span data-stu-id="e1be6-235">c.</span></span> <span data-ttu-id="e1be6-236">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="e1be6-236">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e1be6-237">d.</span><span class="sxs-lookup"><span data-stu-id="e1be6-237">d.</span></span> <span data-ttu-id="e1be6-238">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e1be6-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="e1be6-239">Créer un utilisateur de test pour SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="e1be6-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="e1be6-240">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="e1be6-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="e1be6-241">Collaborez avec [équipe de support SAP Business ByDesign Client](https://www.sap.com/products/cloud-analytics.support.html) tooadd les utilisateurs de hello dans la plateforme de SAP Business ByDesign hello.</span><span class="sxs-lookup"><span data-stu-id="e1be6-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) tooadd hello users in hello SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="e1be6-242">Assurez-vous que NameID valeur doit correspondre au champ de nom d’utilisateur hello dans la plateforme de SAP Business ByDesign hello.</span><span class="sxs-lookup"><span data-stu-id="e1be6-242">Please make sure that NameID value should match with hello username field in hello SAP Business ByDesign platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e1be6-243">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e1be6-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e1be6-244">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSAP ByDesign de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="e1be6-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Business ByDesign.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="e1be6-246">**tooassign Britta Simon tooSAP ByDesign de l’entreprise, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e1be6-246">**tooassign Britta Simon tooSAP Business ByDesign, perform hello following steps:**</span></span>

1. <span data-ttu-id="e1be6-247">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e1be6-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e1be6-249">Dans la liste des applications hello, sélectionnez **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="e1be6-249">In hello applications list, select **SAP Business ByDesign**.</span></span>

    ![lien de SAP Business ByDesign Hello dans la liste des Applications hello](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="e1be6-251">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e1be6-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="e1be6-253">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e1be6-253">Click **Add** button.</span></span> <span data-ttu-id="e1be6-254">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e1be6-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="e1be6-256">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="e1be6-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e1be6-257">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e1be6-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e1be6-258">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e1be6-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e1be6-259">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e1be6-259">Test single sign-on</span></span>

<span data-ttu-id="e1be6-260">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="e1be6-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e1be6-261">Lorsque vous cliquez sur mosaïque de SAP Business ByDesign hello Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour SAP Business ByDesign application.</span><span class="sxs-lookup"><span data-stu-id="e1be6-261">When you click hello SAP Business ByDesign tile in hello Access Panel, you should get automatically signed-on tooyour SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1be6-262">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e1be6-262">Additional resources</span></span>

* [<span data-ttu-id="e1be6-263">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1be6-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e1be6-264">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e1be6-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

