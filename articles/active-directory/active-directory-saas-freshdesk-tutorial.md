---
title: "Didacticiel : Intégration d’Azure Active Directory avec FreshDesk | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de FreshDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 577a5eb6d9b1bc03030a2b47f63d375869c903bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="2e091-103">Didacticiel : Intégration d’Azure Active Directory à FreshDesk</span><span class="sxs-lookup"><span data-stu-id="2e091-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="2e091-104">Dans ce didacticiel, vous apprendrez comment toointegrate FreshDesk avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e091-104">In this tutorial, you learn how toointegrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2e091-105">Intégration de FreshDesk à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2e091-105">Integrating FreshDesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2e091-106">Vous pouvez contrôler dans Azure AD qui a accès tooFreshDesk</span><span class="sxs-lookup"><span data-stu-id="2e091-106">You can control in Azure AD who has access tooFreshDesk</span></span>
- <span data-ttu-id="2e091-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooFreshDesk (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e091-107">You can enable your users tooautomatically get signed-on tooFreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2e091-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="2e091-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="2e091-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2e091-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e091-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2e091-110">Prerequisites</span></span>

<span data-ttu-id="2e091-111">tooconfigure intégration d’Azure AD à FreshDesk, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2e091-111">tooconfigure Azure AD integration with FreshDesk, you need hello following items:</span></span>

- <span data-ttu-id="2e091-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e091-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2e091-113">Un abonnement FreshDesk pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2e091-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2e091-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2e091-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2e091-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="2e091-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2e091-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2e091-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2e091-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2e091-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2e091-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2e091-118">Scenario description</span></span>
<span data-ttu-id="2e091-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2e091-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2e091-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="2e091-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2e091-121">Ajout de FreshDesk à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="2e091-121">Adding FreshDesk from hello gallery</span></span>
2. <span data-ttu-id="2e091-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e091-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-hello-gallery"></a><span data-ttu-id="2e091-123">Ajout de FreshDesk à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="2e091-123">Adding FreshDesk from hello gallery</span></span>
<span data-ttu-id="2e091-124">intégration de hello tooconfigure de FreshDesk dans Azure AD, vous devez tooadd FreshDesk à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2e091-124">tooconfigure hello integration of FreshDesk into Azure AD, you need tooadd FreshDesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2e091-125">**tooadd FreshDesk à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2e091-125">**tooadd FreshDesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e091-126">Bonjour ** [portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="2e091-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2e091-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2e091-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2e091-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2e091-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2e091-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="2e091-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2e091-133">Dans la zone de recherche de hello, tapez **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="2e091-133">In hello search box, type **FreshDesk**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="2e091-135">Dans le volet de résultats hello, sélectionnez **FreshDesk**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2e091-135">In hello results panel, select **FreshDesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2e091-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e091-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2e091-138">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec FreshDesk avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2e091-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2e091-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans FreshDesk est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2e091-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshDesk is tooa user in Azure AD.</span></span> <span data-ttu-id="2e091-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans FreshDesk doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="2e091-140">In other words, a link relationship between an Azure AD user and hello related user in FreshDesk needs toobe established.</span></span>

<span data-ttu-id="2e091-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="2e091-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FreshDesk.</span></span>

<span data-ttu-id="2e091-142">tooconfigure et test Azure AD l’authentification unique à FreshDesk, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="2e091-142">tooconfigure and test Azure AD single sign-on with FreshDesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2e091-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2e091-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2e091-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e091-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2e091-145">**[Création d’un utilisateur de test de FreshDesk](#creating-a-freshdesk-test-user) ** -toohave de Britta Simon dans FreshDesk qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="2e091-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - toohave a counterpart of Britta Simon in FreshDesk that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="2e091-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2e091-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2e091-147">**[Test de l’authentification unique sur](#testing-single-sign-on) ** -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="2e091-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2e091-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e091-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2e091-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="2e091-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="2e091-150">**tooconfigure Azure AD single sign-on avec FreshDesk, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2e091-150">**tooconfigure Azure AD single sign-on with FreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e091-151">Dans le portail de gestion Azure hello, sur hello **FreshDesk** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2e091-151">In hello Azure Management portal, on hello **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="2e091-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2e091-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="2e091-155">Sur hello **FreshDesk domaine et les URL** section, Veuillez entrer hello **URL de connexion** en tant que : `https://<tenant-name>.freshdesk.com` ou toute autre valeur Freshdesk a suggéré.</span><span class="sxs-lookup"><span data-stu-id="2e091-155">On hello **FreshDesk Domain and URLs** section, please enter hello **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="2e091-157">Notez qu’il ne s’agit pas de la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="2e091-157">Please note that this is not the real value.</span></span> <span data-ttu-id="2e091-158">Vous devez mettre à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="2e091-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="2e091-159">Contactez [l’équipe de support FreshDesk](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) pour obtenir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="2e091-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="2e091-160">Sur hello **le certificat de signature SAML** , cliquez sur **certificat** , puis enregistrez le certificat de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2e091-160">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="2e091-162">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="2e091-162">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2e091-164">Sur hello **FreshDesk Configuration** , cliquez sur **FreshDesk de configuration** tooopen configurer l’authentification sur fenêtre.</span><span class="sxs-lookup"><span data-stu-id="2e091-164">On hello **FreshDesk Configuration** section, click **Configure FreshDesk** tooopen Configure sign-on window.</span></span> <span data-ttu-id="2e091-165">Copier hello SAML Sign-On URL du Service unique et les URL de déconnexion de hello **aide-mémoire** section.</span><span class="sxs-lookup"><span data-stu-id="2e091-165">Copy hello SAML Single Sign-On Service URL and Sign-Out URL from hello **Quick Reference** section.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="2e091-167">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Freshdesk en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2e091-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="2e091-168">Dans le menu hello haut de hello, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="2e091-168">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="2e091-169">![Administrateur](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="2e091-169">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="2e091-170">Bonjour **paramètres généraux** , cliquez sur **sécurité**.</span><span class="sxs-lookup"><span data-stu-id="2e091-170">In hello **General Settings** tab, click **Security**.</span></span>
   
   <span data-ttu-id="2e091-171">![Sécurité](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Sécurité")</span><span class="sxs-lookup"><span data-stu-id="2e091-171">![Security](./media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="2e091-172">Bonjour **sécurité** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2e091-172">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="2e091-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span><span class="sxs-lookup"><span data-stu-id="2e091-173">![Single Sign On](./media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="2e091-174">a.</span><span class="sxs-lookup"><span data-stu-id="2e091-174">a.</span></span> <span data-ttu-id="2e091-175">Pour **Single Sign On (SSO)**, sélectionnez **On**.</span><span class="sxs-lookup"><span data-stu-id="2e091-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="2e091-176">b.</span><span class="sxs-lookup"><span data-stu-id="2e091-176">b.</span></span> <span data-ttu-id="2e091-177">Sélectionnez **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="2e091-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="2e091-178">c.</span><span class="sxs-lookup"><span data-stu-id="2e091-178">c.</span></span> <span data-ttu-id="2e091-179">Hello de type **SAML Sign-On URL du Service unique** vous avez copié à partir du portail Azure dans hello **URL de connexion SAML** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="2e091-179">Type hello **SAML Single Sign-On Service URL** you copied from Azure portal into hello **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="2e091-180">d.</span><span class="sxs-lookup"><span data-stu-id="2e091-180">d.</span></span> <span data-ttu-id="2e091-181">Hello de type **URL de déconnexion** vous avez copié à partir du portail Azure dans hello **URL de déconnexion** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="2e091-181">Type hello **Sign-Out URL**  you copied from Azure portal into hello **Logout URL** textbox.</span></span>

    <span data-ttu-id="2e091-182">e.</span><span class="sxs-lookup"><span data-stu-id="2e091-182">e.</span></span> <span data-ttu-id="2e091-183">Hello de copie **l’empreinte numérique** à partir du certificat hello téléchargé à partir du portail Azure et collez-le dans hello **Security Certificate Fingerprint** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="2e091-183">Copy hello **Thumbprint** value from hello downloaded certificate from Azure portal and paste it into hello **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="2e091-184">Pour plus d’informations, consultez [comment tooretrieve valeur d’empreinte numérique d’un certificat](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="2e091-184">For more details, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="2e091-185">f.</span><span class="sxs-lookup"><span data-stu-id="2e091-185">f.</span></span> <span data-ttu-id="2e091-186">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="2e091-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2e091-187">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e091-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="2e091-188">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2e091-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="2e091-190">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2e091-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e091-191">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="2e091-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2e091-193">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2e091-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2e091-195">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2e091-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2e091-197">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2e091-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2e091-199">a.</span><span class="sxs-lookup"><span data-stu-id="2e091-199">a.</span></span> <span data-ttu-id="2e091-200">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2e091-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2e091-201">b.</span><span class="sxs-lookup"><span data-stu-id="2e091-201">b.</span></span> <span data-ttu-id="2e091-202">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2e091-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2e091-203">c.</span><span class="sxs-lookup"><span data-stu-id="2e091-203">c.</span></span> <span data-ttu-id="2e091-204">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2e091-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2e091-205">d.</span><span class="sxs-lookup"><span data-stu-id="2e091-205">d.</span></span> <span data-ttu-id="2e091-206">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2e091-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="2e091-207">Création d’un utilisateur de test FreshDesk</span><span class="sxs-lookup"><span data-stu-id="2e091-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="2e091-208">Dans l’ordre tooenable le toolog d’utilisateurs Azure AD à FreshDesk, vous devez les configurer dans FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="2e091-208">In order tooenable Azure AD users toolog into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="2e091-209">Dans les cas de hello de FreshDesk, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="2e091-209">In hello case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="2e091-210">**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2e091-210">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e091-211">Connectez-vous à tooyour **Freshdesk** client.</span><span class="sxs-lookup"><span data-stu-id="2e091-211">Log in tooyour **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="2e091-212">Dans le menu hello haut de hello, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="2e091-212">In hello menu on hello top, click **Admin**.</span></span>
   
   <span data-ttu-id="2e091-213">![Administrateur](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Administrateur")</span><span class="sxs-lookup"><span data-stu-id="2e091-213">![Admin](./media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="2e091-214">Bonjour **paramètres généraux** , cliquez sur **Agents**.</span><span class="sxs-lookup"><span data-stu-id="2e091-214">In hello **General Settings** tab, click **Agents**.</span></span>
   
   <span data-ttu-id="2e091-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span><span class="sxs-lookup"><span data-stu-id="2e091-215">![Agents](./media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="2e091-216">Cliquez sur **New Agent**.</span><span class="sxs-lookup"><span data-stu-id="2e091-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="2e091-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span><span class="sxs-lookup"><span data-stu-id="2e091-217">![New Agent](./media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="2e091-218">Dans la boîte de dialogue informations d’Agent hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2e091-218">On hello Agent Information dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="2e091-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span><span class="sxs-lookup"><span data-stu-id="2e091-219">![Agent Information](./media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
   <span data-ttu-id="2e091-220">a.</span><span class="sxs-lookup"><span data-stu-id="2e091-220">a.</span></span> <span data-ttu-id="2e091-221">Bonjour **nom complet** zone de texte, nom du compte Azure AD de hello tooprovision hello du type.</span><span class="sxs-lookup"><span data-stu-id="2e091-221">In hello **Full Name** textbox, type hello name of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="2e091-222">b.</span><span class="sxs-lookup"><span data-stu-id="2e091-222">b.</span></span> <span data-ttu-id="2e091-223">Bonjour **messagerie** zone de texte, hello de type Azure AD adresse de messagerie du compte Azure AD de hello tooprovision.</span><span class="sxs-lookup"><span data-stu-id="2e091-223">In hello **Email** textbox, type hello Azure AD email address of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="2e091-224">c.</span><span class="sxs-lookup"><span data-stu-id="2e091-224">c.</span></span> <span data-ttu-id="2e091-225">Bonjour **titre** zone de texte, taper un titre du compte Azure AD de hello tooprovision hello.</span><span class="sxs-lookup"><span data-stu-id="2e091-225">In hello **Title** textbox, type hello title of hello Azure AD account you want tooprovision.</span></span>

   <span data-ttu-id="2e091-226">d.</span><span class="sxs-lookup"><span data-stu-id="2e091-226">d.</span></span> <span data-ttu-id="2e091-227">Sélectionnez **Agents role**, puis cliquez sur **Assign**.</span><span class="sxs-lookup"><span data-stu-id="2e091-227">Select **Agents role**, and then click **Assign**.</span></span>
       
   <span data-ttu-id="2e091-228">e.</span><span class="sxs-lookup"><span data-stu-id="2e091-228">e.</span></span> <span data-ttu-id="2e091-229">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2e091-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="2e091-230">détenteur du compte de Hello Azure AD reçoit un message électronique qui inclut un compte de hello tooconfirm lien avant d’être activé.</span><span class="sxs-lookup"><span data-stu-id="2e091-230">hello Azure AD account holder will get an email that includes a link tooconfirm hello account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="2e091-231">Vous pouvez utiliser n’importe quel autre Freshdesk utilisateur compte outil de création ou API fournie par Freshdesk tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="2e091-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk tooprovision AAD user accounts.</span></span> <span data-ttu-id="2e091-232">tooFreshDesk.</span><span class="sxs-lookup"><span data-stu-id="2e091-232">tooFreshDesk.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2e091-233">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2e091-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2e091-234">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooBox de son accès.</span><span class="sxs-lookup"><span data-stu-id="2e091-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBox.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="2e091-236">**tooassign Britta Simon tooFreshDesk, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2e091-236">**tooassign Britta Simon tooFreshDesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="2e091-237">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2e091-237">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2e091-239">Dans la liste des applications hello, sélectionnez **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="2e091-239">In hello applications list, select **FreshDesk**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="2e091-241">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2e091-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="2e091-243">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2e091-243">Click **Add** button.</span></span> <span data-ttu-id="2e091-244">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2e091-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="2e091-246">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="2e091-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2e091-247">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2e091-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2e091-248">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2e091-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2e091-249">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2e091-249">Testing single sign-on</span></span>

<span data-ttu-id="2e091-250">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="2e091-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2e091-251">Lorsque vous cliquez sur mosaïque FreshDesk hello hello volet d’accès, vous devez obtenir login page tooget connecté tooyour leur application FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="2e091-251">When you click hello FreshDesk tile in hello Access Panel, you should get login page tooget signed-on tooyour FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2e091-252">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2e091-252">Additional resources</span></span>

* [<span data-ttu-id="2e091-253">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e091-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2e091-254">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2e091-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png

