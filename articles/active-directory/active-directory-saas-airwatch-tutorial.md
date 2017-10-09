---
title: "Didacticiel : Intégration d’Azure Active Directory à AirWatch | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et AirWatch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a><span data-ttu-id="142f3-103">Didacticiel : Intégration d’Azure Active Directory à AirWatch</span><span class="sxs-lookup"><span data-stu-id="142f3-103">Tutorial: Azure Active Directory integration with AirWatch</span></span>

<span data-ttu-id="142f3-104">Dans ce didacticiel, vous apprendrez comment toointegrate AirWatch avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="142f3-104">In this tutorial, you learn how toointegrate AirWatch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="142f3-105">Intégration d’AirWatch à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="142f3-105">Integrating AirWatch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="142f3-106">Vous pouvez contrôler dans Azure AD qui a accès tooAirWatch</span><span class="sxs-lookup"><span data-stu-id="142f3-106">You can control in Azure AD who has access tooAirWatch</span></span>
- <span data-ttu-id="142f3-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAirWatch (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="142f3-107">You can enable your users tooautomatically get signed-on tooAirWatch (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="142f3-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="142f3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="142f3-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="142f3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="142f3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="142f3-110">Prerequisites</span></span>

<span data-ttu-id="142f3-111">tooconfigure intégration d’Azure AD à AirWatch, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="142f3-111">tooconfigure Azure AD integration with AirWatch, you need hello following items:</span></span>

- <span data-ttu-id="142f3-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="142f3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="142f3-113">Un abonnement AirWatch pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="142f3-113">An AirWatch single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="142f3-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="142f3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="142f3-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="142f3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="142f3-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="142f3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="142f3-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="142f3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="142f3-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="142f3-118">Scenario description</span></span>
<span data-ttu-id="142f3-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="142f3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="142f3-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="142f3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="142f3-121">Ajout d’AirWatch à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="142f3-121">Adding AirWatch from hello gallery</span></span>
2. <span data-ttu-id="142f3-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="142f3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-airwatch-from-hello-gallery"></a><span data-ttu-id="142f3-123">Ajout d’AirWatch à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="142f3-123">Adding AirWatch from hello gallery</span></span>
<span data-ttu-id="142f3-124">intégration de hello tooconfigure d’AirWatch dans Azure AD, vous devez tooadd AirWatch à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="142f3-124">tooconfigure hello integration of AirWatch into Azure AD, you need tooadd AirWatch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="142f3-125">**tooadd AirWatch à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="142f3-125">**tooadd AirWatch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="142f3-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="142f3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="142f3-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="142f3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="142f3-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="142f3-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="142f3-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="142f3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="142f3-133">Dans la zone de recherche de hello, tapez **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="142f3-133">In hello search box, type **AirWatch**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. <span data-ttu-id="142f3-135">Dans le volet de résultats hello, sélectionnez **AirWatch**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="142f3-135">In hello results panel, select **AirWatch**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="142f3-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="142f3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="142f3-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec AirWatch, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="142f3-138">In this section, you configure and test Azure AD single sign-on with AirWatch based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="142f3-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans AirWatch est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="142f3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AirWatch is tooa user in Azure AD.</span></span> <span data-ttu-id="142f3-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans AirWatch doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="142f3-140">In other words, a link relationship between an Azure AD user and hello related user in AirWatch needs toobe established.</span></span>

<span data-ttu-id="142f3-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans AirWatch.</span><span class="sxs-lookup"><span data-stu-id="142f3-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in AirWatch.</span></span>

<span data-ttu-id="142f3-142">tooconfigure et test Azure AD l’authentification unique avec AirWatch, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="142f3-142">tooconfigure and test Azure AD single sign-on with AirWatch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="142f3-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="142f3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="142f3-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="142f3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="142f3-145">**[Création d’un utilisateur de test AirWatch](#creating-a-airwatch-test-user)**  -toohave un équivalent de Britta Simon dans AirWatch est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="142f3-145">**[Creating a AirWatch test user](#creating-a-airwatch-test-user)** - toohave a counterpart of Britta Simon in AirWatch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="142f3-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="142f3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="142f3-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="142f3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="142f3-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="142f3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="142f3-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application AirWatch.</span><span class="sxs-lookup"><span data-stu-id="142f3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AirWatch application.</span></span>

<span data-ttu-id="142f3-150">**tooconfigure Azure AD single sign-on avec AirWatch, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="142f3-150">**tooconfigure Azure AD single sign-on with AirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="142f3-151">Bonjour portail Azure, sur hello **AirWatch** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="142f3-151">In hello Azure portal, on hello **AirWatch** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="142f3-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="142f3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. <span data-ttu-id="142f3-155">Sur hello **AirWatch domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="142f3-155">On hello **AirWatch Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    <span data-ttu-id="142f3-157">a.</span><span class="sxs-lookup"><span data-stu-id="142f3-157">a.</span></span> <span data-ttu-id="142f3-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span><span class="sxs-lookup"><span data-stu-id="142f3-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`</span></span>

    <span data-ttu-id="142f3-159">b.</span><span class="sxs-lookup"><span data-stu-id="142f3-159">b.</span></span> <span data-ttu-id="142f3-160">Bonjour **identificateur** valeur hello de type en tant que zone de texte`AirWatch`</span><span class="sxs-lookup"><span data-stu-id="142f3-160">In hello **Identifier** textbox, type hello value as `AirWatch`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="142f3-161">Cette valeur n’est pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="142f3-161">This value is not hello real.</span></span> <span data-ttu-id="142f3-162">Mettre à jour cette valeur avec l’URL de connexion réel hello.</span><span class="sxs-lookup"><span data-stu-id="142f3-162">Update this value with hello actual Sign-on URL.</span></span> <span data-ttu-id="142f3-163">Contact [équipe de support Client de AirWatch](http://www.air-watch.com/company/contact-us/) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="142f3-163">Contact [AirWatch Client support team](http://www.air-watch.com/company/contact-us/) tooget this value.</span></span> 
 
4. <span data-ttu-id="142f3-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="142f3-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. <span data-ttu-id="142f3-166">Sur hello **AirWatch Configuration** , cliquez sur **AirWatch de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="142f3-166">On hello **AirWatch Configuration** section, click **Configure AirWatch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="142f3-167">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="142f3-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. <span data-ttu-id="142f3-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="142f3-169">Click **Save** button.</span></span>

    <span data-ttu-id="142f3-170">![Configurer l’authentification unique](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="142f3-170">![Configure Single Sign-On](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS></span></span>
7. <span data-ttu-id="142f3-171">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise AirWatch tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="142f3-171">In a different web browser window, log in tooyour AirWatch company site as an administrator.</span></span>

8. <span data-ttu-id="142f3-172">Dans le volet de navigation gauche hello, cliquez sur **comptes**, puis cliquez sur **administrateurs**.</span><span class="sxs-lookup"><span data-stu-id="142f3-172">In hello left navigation pane, click **Accounts**, and then click **Administrators**.</span></span>
   
   <span data-ttu-id="142f3-173">![Administrateurs](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrateurs")</span><span class="sxs-lookup"><span data-stu-id="142f3-173">![Administrators](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrators")</span></span>

9. <span data-ttu-id="142f3-174">Développez hello **paramètres** menu, puis sur **Services Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="142f3-174">Expand hello **Settings** menu, and then click **Directory Services**.</span></span>
   
   <span data-ttu-id="142f3-175">![Paramètres](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="142f3-175">![Settings](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Settings")</span></span>

10. <span data-ttu-id="142f3-176">Cliquez sur hello **utilisateur** onglet hello **Base DN** zone de texte, tapez votre nom de domaine, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="142f3-176">Click hello **User** tab, in hello **Base DN** textbox, type your domain name, and then click **Save**.</span></span>
   
   <span data-ttu-id="142f3-177">![Utilisateur](./media/active-directory-saas-airwatch-tutorial/ic791922.png "Utilisateur")</span><span class="sxs-lookup"><span data-stu-id="142f3-177">![User](./media/active-directory-saas-airwatch-tutorial/ic791922.png "User")</span></span>

11. <span data-ttu-id="142f3-178">Cliquez sur hello **Server** onglet.</span><span class="sxs-lookup"><span data-stu-id="142f3-178">Click hello **Server** tab.</span></span>
   
   <span data-ttu-id="142f3-179">![Serveur](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Serveur")</span><span class="sxs-lookup"><span data-stu-id="142f3-179">![Server](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Server")</span></span>

12. <span data-ttu-id="142f3-180">Effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="142f3-180">Perform hello following steps:</span></span>
    
    <span data-ttu-id="142f3-181">![Télécharger](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Télécharger")</span><span class="sxs-lookup"><span data-stu-id="142f3-181">![Upload](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Upload")</span></span>   
    
    <span data-ttu-id="142f3-182">a.</span><span class="sxs-lookup"><span data-stu-id="142f3-182">a.</span></span> <span data-ttu-id="142f3-183">Pour **Directory Type**, sélectionnez **None**.</span><span class="sxs-lookup"><span data-stu-id="142f3-183">As **Directory Type**, select **None**.</span></span>

    <span data-ttu-id="142f3-184">b.</span><span class="sxs-lookup"><span data-stu-id="142f3-184">b.</span></span> <span data-ttu-id="142f3-185">Sélectionnez **Use SAML For Authentication**.</span><span class="sxs-lookup"><span data-stu-id="142f3-185">Select **Use SAML For Authentication**.</span></span>

    <span data-ttu-id="142f3-186">c.</span><span class="sxs-lookup"><span data-stu-id="142f3-186">c.</span></span> <span data-ttu-id="142f3-187">tooupload hello certificat téléchargé, cliquez sur **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="142f3-187">tooupload hello downloaded certificate, click **Upload**.</span></span>

13. <span data-ttu-id="142f3-188">Bonjour **demande** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="142f3-188">In hello **Request** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="142f3-189">![Demande](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Demande")</span><span class="sxs-lookup"><span data-stu-id="142f3-189">![Request](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Request")</span></span>  

    <span data-ttu-id="142f3-190">a.</span><span class="sxs-lookup"><span data-stu-id="142f3-190">a.</span></span> <span data-ttu-id="142f3-191">Pour **Request Binding Type**, sélectionnez **POST**.</span><span class="sxs-lookup"><span data-stu-id="142f3-191">As **Request Binding Type**, select **POST**.</span></span>

    <span data-ttu-id="142f3-192">b.</span><span class="sxs-lookup"><span data-stu-id="142f3-192">b.</span></span> <span data-ttu-id="142f3-193">Bonjour portail Azure, sur hello **configurer l’authentification unique sur Airwatch** page de boîte de dialogue, hello de copie **SAML Sign-On URL du Service unique** valeur, puis collez-le dans hello **fournisseur d’identité Seule l’URL de connexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="142f3-193">In hello Azure portal, on hello **Configure single sign-on at Airwatch** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Identity Provider Single Sign On URL** textbox.</span></span>

    <span data-ttu-id="142f3-194">c.</span><span class="sxs-lookup"><span data-stu-id="142f3-194">c.</span></span> <span data-ttu-id="142f3-195">Pour **NameID Format**, sélectionnez **Email Address**.</span><span class="sxs-lookup"><span data-stu-id="142f3-195">As **NameID Format**, select **Email Address**.</span></span>

    <span data-ttu-id="142f3-196">d.</span><span class="sxs-lookup"><span data-stu-id="142f3-196">d.</span></span> <span data-ttu-id="142f3-197">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="142f3-197">Click **Save**.</span></span>

14. <span data-ttu-id="142f3-198">Cliquez sur hello **utilisateur** onglet à nouveau.</span><span class="sxs-lookup"><span data-stu-id="142f3-198">Click hello **User** tab again.</span></span>
    
    <span data-ttu-id="142f3-199">![Utilisateur](./media/active-directory-saas-airwatch-tutorial/ic791926.png "Utilisateur")</span><span class="sxs-lookup"><span data-stu-id="142f3-199">![User](./media/active-directory-saas-airwatch-tutorial/ic791926.png "User")</span></span>

15. <span data-ttu-id="142f3-200">Bonjour **attribut** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="142f3-200">In hello **Attribute** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="142f3-201">![Attribut](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribut")</span><span class="sxs-lookup"><span data-stu-id="142f3-201">![Attribute](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribute")</span></span>

    <span data-ttu-id="142f3-202">a.</span><span class="sxs-lookup"><span data-stu-id="142f3-202">a.</span></span> <span data-ttu-id="142f3-203">Bonjour **identificateur d’objet** zone de texte, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span><span class="sxs-lookup"><span data-stu-id="142f3-203">In hello **Object Identifier** textbox, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.</span></span>

    <span data-ttu-id="142f3-204">b.</span><span class="sxs-lookup"><span data-stu-id="142f3-204">b.</span></span> <span data-ttu-id="142f3-205">Bonjour **nom d’utilisateur** zone de texte, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="142f3-205">In hello **Username** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="142f3-206">c.</span><span class="sxs-lookup"><span data-stu-id="142f3-206">c.</span></span> <span data-ttu-id="142f3-207">Bonjour **nom d’affichage** zone de texte, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="142f3-207">In hello **Display Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="142f3-208">d.</span><span class="sxs-lookup"><span data-stu-id="142f3-208">d.</span></span> <span data-ttu-id="142f3-209">Bonjour **prénom** zone de texte, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span><span class="sxs-lookup"><span data-stu-id="142f3-209">In hello **First Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.</span></span>

    <span data-ttu-id="142f3-210">e.</span><span class="sxs-lookup"><span data-stu-id="142f3-210">e.</span></span> <span data-ttu-id="142f3-211">Bonjour **nom** zone de texte, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span><span class="sxs-lookup"><span data-stu-id="142f3-211">In hello **Last Name** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.</span></span>

    <span data-ttu-id="142f3-212">f.</span><span class="sxs-lookup"><span data-stu-id="142f3-212">f.</span></span> <span data-ttu-id="142f3-213">Bonjour **messagerie** zone de texte, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="142f3-213">In hello **Email** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="142f3-214">g.</span><span class="sxs-lookup"><span data-stu-id="142f3-214">g.</span></span> <span data-ttu-id="142f3-215">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="142f3-215">Click **Save**.</span></span>

<CE>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="142f3-216">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="142f3-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="142f3-217">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="142f3-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="142f3-219">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="142f3-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="142f3-220">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="142f3-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="142f3-222">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="142f3-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="142f3-224">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="142f3-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="142f3-226">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="142f3-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="142f3-228">a.</span><span class="sxs-lookup"><span data-stu-id="142f3-228">a.</span></span> <span data-ttu-id="142f3-229">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="142f3-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="142f3-230">b.</span><span class="sxs-lookup"><span data-stu-id="142f3-230">b.</span></span> <span data-ttu-id="142f3-231">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="142f3-231">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="142f3-232">c.</span><span class="sxs-lookup"><span data-stu-id="142f3-232">c.</span></span> <span data-ttu-id="142f3-233">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="142f3-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="142f3-234">d.</span><span class="sxs-lookup"><span data-stu-id="142f3-234">d.</span></span> <span data-ttu-id="142f3-235">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="142f3-235">Click **Create**.</span></span>
 
### <a name="creating-a-airwatch-test-user"></a><span data-ttu-id="142f3-236">Création d’un utilisateur de test AirWatch</span><span class="sxs-lookup"><span data-stu-id="142f3-236">Creating a AirWatch test user</span></span>

<span data-ttu-id="142f3-237">tooenable Azure AD les utilisateurs toolog dans tooAirWatch, ils doivent être configurés dans tooAirWatch.</span><span class="sxs-lookup"><span data-stu-id="142f3-237">tooenable Azure AD users toolog in tooAirWatch, they must be provisioned in tooAirWatch.</span></span>

* <span data-ttu-id="142f3-238">Dans le cas d’AirWatch, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="142f3-238">When AirWatch, provisioning is a manual task.</span></span>

<span data-ttu-id="142f3-239">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="142f3-239">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="142f3-240">Connectez-vous à tooyour **AirWatch** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="142f3-240">Log in tooyour **AirWatch** company site as administrator.</span></span>
2. <span data-ttu-id="142f3-241">Dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **comptes**, puis cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="142f3-241">In hello navigation pane on hello left side, click **Accounts**, and then click **Users**.</span></span>
   
   <span data-ttu-id="142f3-242">![Utilisateurs](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="142f3-242">![Users](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Users")</span></span>
3. <span data-ttu-id="142f3-243">Bonjour **utilisateurs** menu, cliquez sur **mode liste**, puis cliquez sur **ajouter \> ajouter un utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="142f3-243">In hello **Users** menu, click **List View**, and then click **Add \> Add User**.</span></span>
   
   <span data-ttu-id="142f3-244">![Ajouter un utilisateur](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="142f3-244">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Add User")</span></span>
4. <span data-ttu-id="142f3-245">Sur hello **Ajouter / modifier un utilisateur** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="142f3-245">On hello **Add / Edit User** dialog, perform hello following steps:</span></span>

   <span data-ttu-id="142f3-246">![Ajouter un utilisateur](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Ajouter un utilisateur")</span><span class="sxs-lookup"><span data-stu-id="142f3-246">![Add User](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Add User")</span></span>   
   1. <span data-ttu-id="142f3-247">Hello de type **nom d’utilisateur**, **mot de passe**, **confirmer le mot de passe**, **prénom**, **nom**,  **Adresse de messagerie** d’un Azure valide compte Active Directory que vous voulez tooprovision dans hello relatives des zones de texte.</span><span class="sxs-lookup"><span data-stu-id="142f3-247">Type hello **Username**, **Password**, **Confirm Password**, **First Name**, **Last Name**, **Email Address** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="142f3-248">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="142f3-248">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="142f3-249">Vous pouvez utiliser n’importe quel autre AirWatch utilisateur compte outil de création ou API fournie par AirWatch tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="142f3-249">You can use any other AirWatch user account creation tools or APIs provided by AirWatch tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="142f3-250">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="142f3-250">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="142f3-251">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAirWatch.</span><span class="sxs-lookup"><span data-stu-id="142f3-251">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAirWatch.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="142f3-253">**tooassign Britta Simon tooAirWatch, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="142f3-253">**tooassign Britta Simon tooAirWatch, perform hello following steps:**</span></span>

1. <span data-ttu-id="142f3-254">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="142f3-254">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="142f3-256">Dans la liste des applications hello, sélectionnez **AirWatch**.</span><span class="sxs-lookup"><span data-stu-id="142f3-256">In hello applications list, select **AirWatch**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. <span data-ttu-id="142f3-258">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="142f3-258">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="142f3-260">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="142f3-260">Click **Add** button.</span></span> <span data-ttu-id="142f3-261">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="142f3-261">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="142f3-263">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="142f3-263">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="142f3-264">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="142f3-264">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="142f3-265">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="142f3-265">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="142f3-266">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="142f3-266">Testing single sign-on</span></span>

<span data-ttu-id="142f3-267">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="142f3-267">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="142f3-268">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="142f3-268">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="142f3-269">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="142f3-269">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="142f3-270">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="142f3-270">Additional resources</span></span>

* [<span data-ttu-id="142f3-271">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="142f3-271">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="142f3-272">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="142f3-272">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

