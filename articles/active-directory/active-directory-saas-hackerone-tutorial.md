---
title: "Didacticiel : Intégration d’Azure Active Directory avec HackerOne | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Hackerone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: c9dc033e26e79a7233dcfb3899c62684d4a19652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="dd9c4-103">Didacticiel : Intégration d’Azure Active Directory à HackerOne</span><span class="sxs-lookup"><span data-stu-id="dd9c4-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="dd9c4-104">Dans ce didacticiel, vous apprendrez comment toointegrate HackerOne avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd9c4-104">In this tutorial, you learn how toointegrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dd9c4-105">Intégration HackerOne à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="dd9c4-105">Integrating HackerOne with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dd9c4-106">Vous pouvez contrôler dans Azure AD qui a accès tooHackerOne</span><span class="sxs-lookup"><span data-stu-id="dd9c4-106">You can control in Azure AD who has access tooHackerOne</span></span>
- <span data-ttu-id="dd9c4-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooHackerOne (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd9c4-107">You can enable your users tooautomatically get signed-on tooHackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dd9c4-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="dd9c4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dd9c4-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dd9c4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd9c4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dd9c4-110">Prerequisites</span></span>

<span data-ttu-id="dd9c4-111">tooconfigure intégration d’Azure AD avec HackerOne, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="dd9c4-111">tooconfigure Azure AD integration with HackerOne, you need hello following items:</span></span>

- <span data-ttu-id="dd9c4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd9c4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dd9c4-113">Un abonnement Hackerone pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="dd9c4-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dd9c4-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dd9c4-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="dd9c4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dd9c4-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dd9c4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dd9c4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dd9c4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="dd9c4-118">Scenario description</span></span>
<span data-ttu-id="dd9c4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dd9c4-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="dd9c4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dd9c4-121">Ajout de HackerOne à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="dd9c4-121">Adding HackerOne from hello gallery</span></span>
2. <span data-ttu-id="dd9c4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd9c4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-hello-gallery"></a><span data-ttu-id="dd9c4-123">Ajout de HackerOne à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="dd9c4-123">Adding HackerOne from hello gallery</span></span>
<span data-ttu-id="dd9c4-124">intégration de hello tooconfigure de HackerOne dans Azure AD, vous devez tooadd HackerOne à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-124">tooconfigure hello integration of HackerOne into Azure AD, you need tooadd HackerOne from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dd9c4-125">**tooadd HackerOne à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd9c4-125">**tooadd HackerOne from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd9c4-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dd9c4-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dd9c4-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="dd9c4-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="dd9c4-133">Dans la zone de recherche de hello, tapez **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-133">In hello search box, type **HackerOne**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="dd9c4-135">Dans le volet de résultats hello, sélectionnez **HackerOne**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-135">In hello results panel, select **HackerOne**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dd9c4-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd9c4-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="dd9c4-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec HackerOne avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="dd9c4-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dd9c4-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans HackerOne est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in HackerOne is tooa user in Azure AD.</span></span> <span data-ttu-id="dd9c4-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans HackerOne doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-140">In other words, a link relationship between an Azure AD user and hello related user in HackerOne needs toobe established.</span></span>

<span data-ttu-id="dd9c4-141">Dans HackerOne, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-141">In HackerOne, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dd9c4-142">tooconfigure et test Azure AD l’authentification unique avec HackerOne, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="dd9c4-142">tooconfigure and test Azure AD single sign-on with HackerOne, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dd9c4-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dd9c4-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dd9c4-145">**[Création d’un utilisateur de test HackerOne](#creating-a-hackerone-test-user)**  -toohave un équivalent de Britta Simon dans HackerOne est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - toohave a counterpart of Britta Simon in HackerOne that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dd9c4-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dd9c4-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dd9c4-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd9c4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dd9c4-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application HackerOne.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="dd9c4-150">**tooconfigure Azure AD single sign-on avec HackerOne, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd9c4-150">**tooconfigure Azure AD single sign-on with HackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd9c4-151">Bonjour portail Azure, sur hello **HackerOne** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-151">In hello Azure portal, on hello **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="dd9c4-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="dd9c4-155">Sur hello **HackerOne Single sign-on URL et l’identificateur** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd9c4-155">On hello **HackerOne Single sign-on URL and Identifier** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="dd9c4-157">a.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-157">a.</span></span> <span data-ttu-id="dd9c4-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="dd9c4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="dd9c4-159">b.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-159">b.</span></span> <span data-ttu-id="dd9c4-160">Bonjour **identificateur** zone de texte, tapez une URL en tant que :`https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="dd9c4-160">In hello **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="dd9c4-161">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-161">This value is not real.</span></span> <span data-ttu-id="dd9c4-162">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="dd9c4-163">Contact [équipe de support HackerOne](mailto:support@hackerone.com) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-163">Contact [HackerOne support team](mailto:support@hackerone.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="dd9c4-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="dd9c4-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="dd9c4-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dd9c4-168">Sur hello **HackerOne Configuration** , cliquez sur **HackerOne de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-168">On hello **HackerOne Configuration** section, click **Configure HackerOne** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dd9c4-169">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="dd9c4-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="dd9c4-171">Authentification tooyour HackerOne client en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-171">Sign On tooyour HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="dd9c4-172">Dans le menu hello haut de hello, cliquez sur hello »**paramètres**. »</span><span class="sxs-lookup"><span data-stu-id="dd9c4-172">In hello menu on hello top, click hello "**Settings**."</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="dd9c4-174">Accédez trop »**authentification**« et cliquez sur »**ajouter des paramètres SAML**. »</span><span class="sxs-lookup"><span data-stu-id="dd9c4-174">Navigate too"**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="dd9c4-176">Sur hello **paramètres SAML** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd9c4-176">On hello **SAML Settings** dialog, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="dd9c4-178">a.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-178">a.</span></span> <span data-ttu-id="dd9c4-179">Bonjour **domaine de messagerie** zone de texte, tapez un domaine enregistré.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-179">In hello **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="dd9c4-180">b.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-180">b.</span></span> <span data-ttu-id="dd9c4-181">Dans **URL d’authentification unique** zones de texte, collez la valeur hello **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-181">In  **Single Sign On URL** textboxes, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dd9c4-182">c.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-182">c.</span></span> <span data-ttu-id="dd9c4-183">Ouvrez votre **fichier de certificat** dans le bloc-notes est téléchargé à partir du portail Azure, copiez le contenu de hello de celui-ci dans le Presse-papiers, puis collez-la toohello **X509 certificat** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="dd9c4-184">d.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-184">d.</span></span> <span data-ttu-id="dd9c4-185">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-185">Click **Save**.</span></span>

11. <span data-ttu-id="dd9c4-186">Dans la boîte de dialogue Paramètres d’authentification hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd9c4-186">On hello Authentication Settings dialog, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="dd9c4-188">a.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-188">a.</span></span> <span data-ttu-id="dd9c4-189">Cliquez sur **Run test**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-189">Click **Run test**.</span></span>

    <span data-ttu-id="dd9c4-190">b.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-190">b.</span></span> <span data-ttu-id="dd9c4-191">Si hello valeur Hello **état** ont la valeur **dernier état du test : créé**, contactez votre [équipe de support HackerOne](mailto:support@hackerone.com) toorequest une révision de votre configuration.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-191">If hello value of hello **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) toorequest a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="dd9c4-192">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="dd9c4-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dd9c4-193">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dd9c4-194">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dd9c4-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dd9c4-195">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd9c4-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="dd9c4-196">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="dd9c4-198">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd9c4-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd9c4-199">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dd9c4-201">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dd9c4-203">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-203">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dd9c4-205">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd9c4-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dd9c4-207">a.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-207">a.</span></span> <span data-ttu-id="dd9c4-208">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dd9c4-209">b.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-209">b.</span></span> <span data-ttu-id="dd9c4-210">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dd9c4-211">c.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-211">c.</span></span> <span data-ttu-id="dd9c4-212">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dd9c4-213">d.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-213">d.</span></span> <span data-ttu-id="dd9c4-214">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="dd9c4-215">Création d'un utilisateur de test HackerOne</span><span class="sxs-lookup"><span data-stu-id="dd9c4-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="dd9c4-216">Vous allez maintenant créer un utilisateur nommé Britta Simon dans HackerOne.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="dd9c4-217">HackerOne prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="dd9c4-218">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-218">There is no action item for you in this section.</span></span> <span data-ttu-id="dd9c4-219">Lorsque vous accédez à HackerOne, un nouvel utilisateur est créé s'il n'existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="dd9c4-220">Si vous devez manuellement toocreate un utilisateur, vous avez besoin d’équipe de support technique de certifier toocontact hello.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-220">If you need toocreate a user manually, you need toocontact hello Certify support team.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dd9c4-221">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dd9c4-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dd9c4-222">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooHackerOne.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHackerOne.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="dd9c4-224">**tooassign Britta Simon tooHackerOne, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dd9c4-224">**tooassign Britta Simon tooHackerOne, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd9c4-225">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="dd9c4-227">Dans la liste des applications hello, sélectionnez **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-227">In hello applications list, select **HackerOne**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="dd9c4-229">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="dd9c4-231">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-231">Click **Add** button.</span></span> <span data-ttu-id="dd9c4-232">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="dd9c4-234">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dd9c4-235">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dd9c4-236">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dd9c4-237">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="dd9c4-237">Testing single sign-on</span></span>

<span data-ttu-id="dd9c4-238">Enfin, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-238">Finally, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="dd9c4-239">Lorsque vous cliquez sur mosaïque HackerOne hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour HackerOne application.</span><span class="sxs-lookup"><span data-stu-id="dd9c4-239">When you click hello HackerOne tile in hello Access Panel, you should get automatically signed-on tooyour HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dd9c4-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="dd9c4-240">Additional resources</span></span>

* [<span data-ttu-id="dd9c4-241">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dd9c4-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dd9c4-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="dd9c4-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

