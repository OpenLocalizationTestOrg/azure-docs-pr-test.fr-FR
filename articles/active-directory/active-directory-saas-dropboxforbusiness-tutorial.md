---
title: "Didacticiel : Intégration d'Azure Active Directory à Dropbox for Business | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Dropbox for Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a><span data-ttu-id="450e9-103">Didacticiel : Intégration d'Azure Active Directory à Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="450e9-103">Tutorial: Azure Active Directory integration with Dropbox for Business</span></span>

<span data-ttu-id="450e9-104">Dans ce didacticiel, vous apprendrez comment toointegrate Dropbox for Business avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="450e9-104">In this tutorial, you learn how toointegrate Dropbox for Business with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="450e9-105">Intégration de Dropbox for Business à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="450e9-105">Integrating Dropbox for Business with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="450e9-106">Vous pouvez contrôler dans Azure AD qui a accès tooDropbox for Business</span><span class="sxs-lookup"><span data-stu-id="450e9-106">You can control in Azure AD who has access tooDropbox for Business</span></span>
- <span data-ttu-id="450e9-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooDropbox entreprise (SSO) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="450e9-107">You can enable your users tooautomatically get signed-on tooDropbox for Business (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="450e9-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="450e9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="450e9-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="450e9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="450e9-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="450e9-110">Prerequisites</span></span>

<span data-ttu-id="450e9-111">tooconfigure intégration d’Azure AD à Dropbox for Business, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="450e9-111">tooconfigure Azure AD integration with Dropbox for Business, you need hello following items:</span></span>

- <span data-ttu-id="450e9-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="450e9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="450e9-113">Un abonnement Dropbox for Business pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="450e9-113">A Dropbox for Business single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="450e9-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="450e9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="450e9-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="450e9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="450e9-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="450e9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="450e9-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="450e9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="450e9-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="450e9-118">Scenario description</span></span>
<span data-ttu-id="450e9-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="450e9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="450e9-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="450e9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="450e9-121">Ajout de Dropbox for Business à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="450e9-121">Adding Dropbox for Business from hello gallery</span></span>
2. <span data-ttu-id="450e9-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="450e9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dropbox-for-business-from-hello-gallery"></a><span data-ttu-id="450e9-123">Ajout de Dropbox for Business à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="450e9-123">Adding Dropbox for Business from hello gallery</span></span>
<span data-ttu-id="450e9-124">intégration de hello tooconfigure de Dropbox for Business dans Azure AD, vous devez tooadd Dropbox for Business à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="450e9-124">tooconfigure hello integration of Dropbox for Business into Azure AD, you need tooadd Dropbox for Business from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="450e9-125">**tooadd Dropbox for Business à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="450e9-125">**tooadd Dropbox for Business from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="450e9-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="450e9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="450e9-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="450e9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="450e9-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="450e9-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="450e9-131">Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="450e9-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="450e9-133">Dans la zone de recherche de hello, tapez **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="450e9-133">In hello search box, type **Dropbox for Business**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. <span data-ttu-id="450e9-135">Dans le volet de résultats hello, sélectionnez **Dropbox for Business**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="450e9-135">In hello results panel, select **Dropbox for Business**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="450e9-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="450e9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="450e9-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Dropbox for Business, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="450e9-138">In this section, you configure and test Azure AD single sign-on with Dropbox for Business based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="450e9-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Dropbox for Business est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="450e9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Dropbox for Business is tooa user in Azure AD.</span></span> <span data-ttu-id="450e9-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur en Dropbox for Business hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="450e9-140">In other words, a link relationship between an Azure AD user and hello related user in Dropbox for Business needs toobe established.</span></span>

<span data-ttu-id="450e9-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="450e9-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Dropbox for Business.</span></span>

<span data-ttu-id="450e9-142">tooconfigure et test Azure AD l’authentification unique avec Dropbox for Business, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="450e9-142">tooconfigure and test Azure AD single sign-on with Dropbox for Business, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="450e9-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="450e9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="450e9-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="450e9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="450e9-145">**[Création d’un dossier d’échange pour l’utilisateur de test entreprise](#creating-a-dropbox-for-business-test-user)**  -toohave un équivalent de Britta Simon dans Dropbox for Business est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="450e9-145">**[Creating a Dropbox for Business test user](#creating-a-dropbox-for-business-test-user)** - toohave a counterpart of Britta Simon in Dropbox for Business that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="450e9-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="450e9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="450e9-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="450e9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="450e9-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="450e9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="450e9-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre Dropbox pour l’application d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="450e9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Dropbox for Business application.</span></span>

<span data-ttu-id="450e9-150">**tooconfigure Azure AD single sign-on avec Dropbox for Business, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="450e9-150">**tooconfigure Azure AD single sign-on with Dropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="450e9-151">Bonjour portail Azure, sur hello **Dropbox for Business** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="450e9-151">In hello Azure portal, on hello **Dropbox for Business** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="450e9-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="450e9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. <span data-ttu-id="450e9-155">Sur hello **Dropbox pour le domaine d’entreprise et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="450e9-155">On hello **Dropbox for Business Domain and URLs** section, perform hello following steps:</span></span>

    <span data-ttu-id="450e9-156">a.</span><span class="sxs-lookup"><span data-stu-id="450e9-156">a.</span></span> <span data-ttu-id="450e9-157">Ouverture de session tooyour Dropbox pour le client de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="450e9-157">Sign on tooyour Dropbox for business tenant.</span></span> 
   
    <span data-ttu-id="450e9-158">![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="450e9-158">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="450e9-159">b.</span><span class="sxs-lookup"><span data-stu-id="450e9-159">b.</span></span> <span data-ttu-id="450e9-160">Dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **Console d’administration**.</span><span class="sxs-lookup"><span data-stu-id="450e9-160">In hello navigation pane on hello left side, click **Admin Console**.</span></span> 
   
    <span data-ttu-id="450e9-161">![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="450e9-161">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="450e9-162">c.</span><span class="sxs-lookup"><span data-stu-id="450e9-162">c.</span></span> <span data-ttu-id="450e9-163">Sur hello **Console d’administration**, cliquez sur **authentification** dans le volet de navigation gauche hello.</span><span class="sxs-lookup"><span data-stu-id="450e9-163">On hello **Admin Console**, click **Authentication** in hello left navigation pane.</span></span> 
   
    <span data-ttu-id="450e9-164">![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="450e9-164">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="450e9-165">d.</span><span class="sxs-lookup"><span data-stu-id="450e9-165">d.</span></span> <span data-ttu-id="450e9-166">Bonjour **l’authentification unique** section, sélectionnez **activer l’authentification unique sur**, puis cliquez sur **plus** tooexpand cette section.</span><span class="sxs-lookup"><span data-stu-id="450e9-166">In hello **Single sign-on** section, select **Enable single sign-on**, and then click **More** tooexpand this section.</span></span>  
   
    <span data-ttu-id="450e9-167">![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="450e9-167">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="450e9-168">e.</span><span class="sxs-lookup"><span data-stu-id="450e9-168">e.</span></span> <span data-ttu-id="450e9-169">Copier l’URL de hello ensuite trop**les utilisateurs peuvent se connecter en entrant leur adresse de messagerie ou ils peuvent accéder directement à**.</span><span class="sxs-lookup"><span data-stu-id="450e9-169">Copy hello URL next too**Users can sign in by entering their email address or they can go directly to**.</span></span> 
    
    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    <span data-ttu-id="450e9-171">f.</span><span class="sxs-lookup"><span data-stu-id="450e9-171">f.</span></span> <span data-ttu-id="450e9-172">Sur hello portail Azure, Bonjour **URL de connexion** zone de texte, collez hello URL.</span><span class="sxs-lookup"><span data-stu-id="450e9-172">On hello Azure portal, in hello **Sign-on URL** textbox, paste hello URL.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     <span data-ttu-id="450e9-174">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.dropbox.com/sso/<id>`</span><span class="sxs-lookup"><span data-stu-id="450e9-174">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.dropbox.com/sso/<id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="450e9-175">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="450e9-175">This value is not real value.</span></span> <span data-ttu-id="450e9-176">Mettre à jour la valeur de hello avec hello Sign-on URL réelle vous obtenez à partir de la section de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="450e9-176">Update hello value with hello actual Sign-on URL you get from their Single sign-on section.</span></span> <span data-ttu-id="450e9-177">Contact [Dropbox pour l’équipe de support Client Business](https://www.dropbox.com/business/contact) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="450e9-177">Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact) tooget this value.</span></span> 
 
4. <span data-ttu-id="450e9-178">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="450e9-178">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. <span data-ttu-id="450e9-180">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="450e9-180">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="450e9-182">Sur hello **Dropbox for Business Configuration** , cliquez sur **configurer de Dropbox for Business** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="450e9-182">On hello **Dropbox for Business Configuration** section, click **Configure Dropbox for Business** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="450e9-183">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="450e9-183">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. <span data-ttu-id="450e9-185">tooconfigure l’authentification unique sur **Dropbox for Business** côté, allez sur votre client Dropbox for Business, Bonjour **l’authentification unique** section Hello **authentification** page, Effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="450e9-185">tooconfigure single sign-on on **Dropbox for Business** side, Go on your Dropbox for Business tenant, in hello **Single sign-on** section of hello **Authentication** page, perform hello following steps:</span></span> 
   
    <span data-ttu-id="450e9-186">![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="450e9-186">![Configure single sign-on](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="450e9-187">a.</span><span class="sxs-lookup"><span data-stu-id="450e9-187">a.</span></span> <span data-ttu-id="450e9-188">Cliquez sur **Obligatoire**.</span><span class="sxs-lookup"><span data-stu-id="450e9-188">Click **Required**.</span></span>
   
    <span data-ttu-id="450e9-189">b.</span><span class="sxs-lookup"><span data-stu-id="450e9-189">b.</span></span> <span data-ttu-id="450e9-190">Bonjour portail Azure, sur hello **configurer l’authentification** fenêtre, hello de copie **SAML Sign-On URL du Service unique** valeur, puis collez-le dans hello **URL de connexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="450e9-190">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in URL** textbox.</span></span>

    <span data-ttu-id="450e9-191">c.</span><span class="sxs-lookup"><span data-stu-id="450e9-191">c.</span></span> <span data-ttu-id="450e9-192">Cliquez sur **choisir un certificat**, puis recherchez tooyour **fichier de certificat codé en Base64**.</span><span class="sxs-lookup"><span data-stu-id="450e9-192">Click **Choose certificate**, and then browse tooyour **Base64 encoded certificate file**.</span></span>

    <span data-ttu-id="450e9-193">d.</span><span class="sxs-lookup"><span data-stu-id="450e9-193">d.</span></span> <span data-ttu-id="450e9-194">Cliquez sur **enregistrer les modifications** configuration de hello toocomplete sur votre client DropBox for Business.</span><span class="sxs-lookup"><span data-stu-id="450e9-194">Click **Save changes** toocomplete hello configuration on your DropBox for Business tenant.</span></span>

> [!TIP]
> <span data-ttu-id="450e9-195">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="450e9-195">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="450e9-196">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="450e9-196">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="450e9-197">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="450e9-197">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="450e9-198">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="450e9-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="450e9-199">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="450e9-199">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="450e9-201">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="450e9-201">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="450e9-202">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="450e9-202">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="450e9-204">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="450e9-204">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="450e9-206">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="450e9-206">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="450e9-208">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="450e9-208">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="450e9-210">a.</span><span class="sxs-lookup"><span data-stu-id="450e9-210">a.</span></span> <span data-ttu-id="450e9-211">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="450e9-211">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="450e9-212">b.</span><span class="sxs-lookup"><span data-stu-id="450e9-212">b.</span></span> <span data-ttu-id="450e9-213">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="450e9-213">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="450e9-214">c.</span><span class="sxs-lookup"><span data-stu-id="450e9-214">c.</span></span> <span data-ttu-id="450e9-215">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="450e9-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="450e9-216">d.</span><span class="sxs-lookup"><span data-stu-id="450e9-216">d.</span></span> <span data-ttu-id="450e9-217">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="450e9-217">Click **Create**.</span></span>
 
### <a name="creating-a-dropbox-for-business-test-user"></a><span data-ttu-id="450e9-218">Création d’un utilisateur de test Dropbox for Business</span><span class="sxs-lookup"><span data-stu-id="450e9-218">Creating a Dropbox for Business test user</span></span>

<span data-ttu-id="450e9-219">Dans cette section, un utilisateur appelé Britta Simon est créé dans Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="450e9-219">In this section, a user called Britta Simon is created in Dropbox for Business.</span></span> <span data-ttu-id="450e9-220">Dropbox for Business prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="450e9-220">Dropbox for Business supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="450e9-221">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="450e9-221">There is no action item for you in this section.</span></span> <span data-ttu-id="450e9-222">Si un utilisateur n’existe pas déjà dans Dropbox for Business, un nouveau est créé lorsque vous essayez de tooaccess Dropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="450e9-222">If a user doesn't already exist in Dropbox for Business, a new one is created when you attempt tooaccess Dropbox for Business.</span></span>

>[!Note]
><span data-ttu-id="450e9-223">Si vous avez besoin de toocreate un utilisateur manuellement, contactez [Dropbox pour l’équipe de support Client d’entreprise](https://www.dropbox.com/business/contact)</span><span class="sxs-lookup"><span data-stu-id="450e9-223">If you need toocreate a user manually, Contact [Dropbox for Business Client support team](https://www.dropbox.com/business/contact)</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="450e9-224">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="450e9-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="450e9-225">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooDropbox for Business.</span><span class="sxs-lookup"><span data-stu-id="450e9-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDropbox for Business.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="450e9-227">**tooassign tooDropbox Britta Simon for Business, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="450e9-227">**tooassign Britta Simon tooDropbox for Business, perform hello following steps:**</span></span>

1. <span data-ttu-id="450e9-228">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="450e9-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="450e9-230">Dans la liste des applications hello, sélectionnez **Dropbox for Business**.</span><span class="sxs-lookup"><span data-stu-id="450e9-230">In hello applications list, select **Dropbox for Business**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. <span data-ttu-id="450e9-232">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="450e9-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="450e9-234">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="450e9-234">Click **Add** button.</span></span> <span data-ttu-id="450e9-235">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="450e9-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="450e9-237">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="450e9-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="450e9-238">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="450e9-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="450e9-239">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="450e9-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="450e9-240">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="450e9-240">Testing single sign-on</span></span>

<span data-ttu-id="450e9-241">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="450e9-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="450e9-242">Lorsque vous cliquez sur hello Dropbox de vignette Business Bonjour volet d’accès, vous devez obtenir la page de connexion de votre Dropbox pour l’application d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="450e9-242">When you click hello Dropbox for Business tile in hello Access Panel, you should get login page of your Dropbox for Business application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="450e9-243">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="450e9-243">Additional resources</span></span>

* [<span data-ttu-id="450e9-244">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="450e9-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="450e9-245">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="450e9-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="450e9-246">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="450e9-246">Configure User Provisioning</span></span>](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

