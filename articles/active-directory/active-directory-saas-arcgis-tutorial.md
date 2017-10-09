---
title: "Didacticiel : Intégration d’Azure Active Directory à ArcGIS Online | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de ArcGIS en ligne."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="b0f7d-103">Didacticiel : Intégration d’Azure Active Directory à ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="b0f7d-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="b0f7d-104">Dans ce didacticiel, vous apprendrez comment toointegrate ArcGIS en ligne avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0f7d-104">In this tutorial, you learn how toointegrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0f7d-105">Intégration de ArcGIS en ligne auprès d’Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="b0f7d-105">Integrating ArcGIS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b0f7d-106">Vous pouvez contrôler dans Azure AD qui a accès tooArcGIS en ligne</span><span class="sxs-lookup"><span data-stu-id="b0f7d-106">You can control in Azure AD who has access tooArcGIS Online</span></span>
- <span data-ttu-id="b0f7d-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooArcGIS en ligne (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0f7d-107">You can enable your users tooautomatically get signed-on tooArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b0f7d-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b0f7d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b0f7d-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b0f7d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="b0f7d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b0f7d-110">Prerequisites</span></span>

<span data-ttu-id="b0f7d-111">tooconfigure intégration d’Azure AD avec ArcGIS en ligne, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b0f7d-111">tooconfigure Azure AD integration with ArcGIS Online, you need hello following items:</span></span>

- <span data-ttu-id="b0f7d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0f7d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b0f7d-113">Un abonnement ArcGIS Online pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="b0f7d-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0f7d-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b0f7d-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="b0f7d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b0f7d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b0f7d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0f7d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0f7d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b0f7d-118">Scenario description</span></span>
<span data-ttu-id="b0f7d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b0f7d-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="b0f7d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0f7d-121">Ajout de ArcGIS en ligne à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="b0f7d-121">Adding ArcGIS Online from hello gallery</span></span>
2. <span data-ttu-id="b0f7d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0f7d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-hello-gallery"></a><span data-ttu-id="b0f7d-123">Ajout de ArcGIS en ligne à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="b0f7d-123">Adding ArcGIS Online from hello gallery</span></span>
<span data-ttu-id="b0f7d-124">intégration de hello tooconfigure de ArcGIS en ligne dans Azure AD, vous devez tooadd ArcGIS en ligne à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-124">tooconfigure hello integration of ArcGIS Online into Azure AD, you need tooadd ArcGIS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b0f7d-125">**tooadd ArcGIS en ligne à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b0f7d-125">**tooadd ArcGIS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0f7d-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b0f7d-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b0f7d-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="b0f7d-131">Cliquez sur **nouvelle application** bouton en haut de hello de nouvelle application hello dialogue tooadd.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Applications][3]

4. <span data-ttu-id="b0f7d-133">Dans la zone de recherche de hello, tapez **ArcGIS en ligne**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-133">In hello search box, type **ArcGIS Online**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="b0f7d-135">Dans le volet de résultats hello, sélectionnez **ArcGIS en ligne**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-135">In hello results panel, select **ArcGIS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b0f7d-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0f7d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b0f7d-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ArcGIS Online sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b0f7d-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b0f7d-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans ArcGIS en ligne est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ArcGIS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="b0f7d-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ArcGIS en ligne doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-140">In other words, a link relationship between an Azure AD user and hello related user in ArcGIS Online needs toobe established.</span></span>

<span data-ttu-id="b0f7d-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans ArcGIS en ligne.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="b0f7d-142">tooconfigure et test Azure AD l’authentification unique avec ArcGIS en ligne, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="b0f7d-142">tooconfigure and test Azure AD single sign-on with ArcGIS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b0f7d-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b0f7d-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0f7d-145">**[Création d’un utilisateur de test en ligne de ArcGIS](#creating-an-arcgis-online-test-user)**  -toohave un équivalent de Britta Simon dans ArcGIS en ligne qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - toohave a counterpart of Britta Simon in ArcGIS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b0f7d-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0f7d-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b0f7d-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0f7d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b0f7d-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application en ligne de ArcGIS.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="b0f7d-150">**tooconfigure Azure AD l’authentification unique sur ArcGIS Online, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b0f7d-150">**tooconfigure Azure AD single sign-on with ArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0f7d-151">Bonjour portail Azure, sur hello **ArcGIS en ligne** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-151">In hello Azure portal, on hello **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="b0f7d-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="b0f7d-155">Sur hello **URL et domaine en ligne de ArcGIS** section, effectuer hello suivant l’étape :</span><span class="sxs-lookup"><span data-stu-id="b0f7d-155">On hello **ArcGIS Online Domain and URLs** section, perform hello following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="b0f7d-157">Bonjour **URL de connexion** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="b0f7d-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b0f7d-158">Cette valeur n’est pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-158">This value is not hello real.</span></span> <span data-ttu-id="b0f7d-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="b0f7d-160">Contact [équipe de support Client en ligne de ArcGIS](http://support.esri.com/) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) tooget this value.</span></span> 

4. <span data-ttu-id="b0f7d-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="b0f7d-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="b0f7d-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b0f7d-165">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise ArcGIS en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="b0f7d-166">Cliquez sur **Edit Settings** (Modifier les paramètres).</span><span class="sxs-lookup"><span data-stu-id="b0f7d-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="b0f7d-167">![Modifier les paramètres](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Modifier les paramètres")</span><span class="sxs-lookup"><span data-stu-id="b0f7d-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="b0f7d-168">Cliquez sur **Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-168">Click **Security**.</span></span>

    <span data-ttu-id="b0f7d-169">![Sécurité](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Sécurité")</span><span class="sxs-lookup"><span data-stu-id="b0f7d-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="b0f7d-170">Sous **Enterprise Logins** (Informations de connexion entreprise), cliquez sur **Set Identity Provider** (Définir un fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="b0f7d-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="b0f7d-171">![Connexions de l’entreprise](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Connexions de l’entreprise")</span><span class="sxs-lookup"><span data-stu-id="b0f7d-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="b0f7d-172">Sur hello **définir le fournisseur d’identité** configuration page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b0f7d-172">On hello **Set Identity Provider** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="b0f7d-173">![Définir le fournisseur d’identité](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Définir le fournisseur d’identité")</span><span class="sxs-lookup"><span data-stu-id="b0f7d-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="b0f7d-174">a.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-174">a.</span></span> <span data-ttu-id="b0f7d-175">Bonjour **nom** zone de texte, tapez le nom de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-175">In hello **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="b0f7d-176">b.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-176">b.</span></span> <span data-ttu-id="b0f7d-177">Pour **métadonnées pour hello fournisseur d’identité d’entreprise sont fournies à l’aide de**, sélectionnez **un fichier**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-177">For **Metadata for hello Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="b0f7d-178">c.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-178">c.</span></span> <span data-ttu-id="b0f7d-179">tooupload votre fichier de métadonnées téléchargé, cliquez sur **choisir un fichier**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-179">tooupload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="b0f7d-180">d.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-180">d.</span></span> <span data-ttu-id="b0f7d-181">Cliquez sur **Set Identity Provider** (Définir un fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="b0f7d-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="b0f7d-182">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="b0f7d-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b0f7d-183">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b0f7d-184">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b0f7d-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b0f7d-185">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0f7d-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="b0f7d-186">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="b0f7d-188">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b0f7d-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0f7d-189">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b0f7d-191">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b0f7d-193">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b0f7d-195">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b0f7d-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b0f7d-197">a.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-197">a.</span></span> <span data-ttu-id="b0f7d-198">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b0f7d-199">b.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-199">b.</span></span> <span data-ttu-id="b0f7d-200">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="b0f7d-201">c.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-201">c.</span></span> <span data-ttu-id="b0f7d-202">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b0f7d-203">d.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-203">d.</span></span> <span data-ttu-id="b0f7d-204">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="b0f7d-205">Création d’un utilisateur de test ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="b0f7d-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="b0f7d-206">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans ArcGIS en ligne, vous devez les configurer dans ArcGIS en ligne.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-206">In order tooenable Azure AD users toolog into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="b0f7d-207">Dans les cas de hello de ArcGIS en ligne, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-207">In hello case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="b0f7d-208">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b0f7d-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0f7d-209">Connectez-vous à tooyour **ArcGIS** client.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-209">Log in tooyour **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="b0f7d-210">Cliquez sur **Invite Members** (Inviter des membres).</span><span class="sxs-lookup"><span data-stu-id="b0f7d-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="b0f7d-211">![Inviter des membres](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Inviter des membres")</span><span class="sxs-lookup"><span data-stu-id="b0f7d-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="b0f7d-212">Sélectionnez **Add members automatically without sending an email** (Ajouter des membres automatiquement sans envoyer d’e-mail), puis cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="b0f7d-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="b0f7d-213">![Ajouter des membres automatiquement](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Ajouter des membres automatiquement")</span><span class="sxs-lookup"><span data-stu-id="b0f7d-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="b0f7d-214">Sur hello **membres** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b0f7d-214">On hello **Members** dialog page, perform hello following steps:</span></span>
   
     <span data-ttu-id="b0f7d-215">![Ajouter et vérifier](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Ajouter et vérifier")</span><span class="sxs-lookup"><span data-stu-id="b0f7d-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="b0f7d-216">a.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-216">a.</span></span> <span data-ttu-id="b0f7d-217">Entrez hello **messagerie**, **prénom**, et **nom** d’un compte AAD valide que vous souhaitez tooprovision.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-217">Enter hello **Email**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision.</span></span>
  
     <span data-ttu-id="b0f7d-218">b.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-218">b.</span></span> <span data-ttu-id="b0f7d-219">Cliquez sur **Add And Review** (Ajouter et vérifier).</span><span class="sxs-lookup"><span data-stu-id="b0f7d-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="b0f7d-220">Passez en revue les données hello vous avez entrées, puis cliquez sur **ajouter des membres**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-220">Review hello data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="b0f7d-221">![Ajouter un membre](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Ajouter un membre")</span><span class="sxs-lookup"><span data-stu-id="b0f7d-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="b0f7d-222">titulaire du compte Azure Active Directory Hello sera reçoivent un e-mail et suivez les leur compte d’un tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-222">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b0f7d-223">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0f7d-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b0f7d-224">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooArcGIS accès en ligne.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooArcGIS Online.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="b0f7d-226">**tooassign tooArcGIS Britta Simon en ligne, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b0f7d-226">**tooassign Britta Simon tooArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="b0f7d-227">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="b0f7d-229">Dans la liste des applications hello, sélectionnez **ArcGIS en ligne**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-229">In hello applications list, select **ArcGIS Online**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="b0f7d-231">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="b0f7d-233">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-233">Click **Add** button.</span></span> <span data-ttu-id="b0f7d-234">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="b0f7d-236">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b0f7d-237">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b0f7d-238">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b0f7d-239">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="b0f7d-239">Testing single sign-on</span></span>

<span data-ttu-id="b0f7d-240">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b0f7d-241">Lorsque vous cliquez sur mosaïque ArcGIS en ligne hello hello volet d’accès, vous devez obtenir tooyour automatiquement signé sur des applications ArcGIS en ligne.</span><span class="sxs-lookup"><span data-stu-id="b0f7d-241">When you click hello ArcGIS Online tile in hello Access Panel, you should get automatically signed-on tooyour ArcGIS Online application.</span></span>
<span data-ttu-id="b0f7d-242">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b0f7d-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b0f7d-243">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b0f7d-243">Additional resources</span></span>

* [<span data-ttu-id="b0f7d-244">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0f7d-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0f7d-245">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b0f7d-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

