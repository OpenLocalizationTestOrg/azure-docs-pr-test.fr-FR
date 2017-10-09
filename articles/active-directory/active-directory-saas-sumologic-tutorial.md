---
title: "Didacticiel : Intégration d’Azure Active Directory à SumoLogic | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de SumoLogic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 2ef1bd329f5db8899f0b57744e4c0f6eed1c532f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="dc056-103">Didacticiel : Intégration d’Azure Active Directory à SumoLogic</span><span class="sxs-lookup"><span data-stu-id="dc056-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="dc056-104">Dans ce didacticiel, vous apprendrez comment toointegrate SumoLogic avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc056-104">In this tutorial, you learn how toointegrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc056-105">Intégration de SumoLogic à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="dc056-105">Integrating SumoLogic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dc056-106">Vous pouvez contrôler dans Azure AD qui a accès tooSumoLogic</span><span class="sxs-lookup"><span data-stu-id="dc056-106">You can control in Azure AD who has access tooSumoLogic</span></span>
- <span data-ttu-id="dc056-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSumoLogic (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc056-107">You can enable your users tooautomatically get signed-on tooSumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dc056-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="dc056-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dc056-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dc056-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc056-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dc056-110">Prerequisites</span></span>

<span data-ttu-id="dc056-111">tooconfigure intégration d’Azure AD à SumoLogic, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="dc056-111">tooconfigure Azure AD integration with SumoLogic, you need hello following items:</span></span>

- <span data-ttu-id="dc056-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc056-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc056-113">Un abonnement SumoLogic pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="dc056-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc056-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="dc056-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dc056-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="dc056-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dc056-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="dc056-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dc056-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc056-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc056-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="dc056-118">Scenario description</span></span>
<span data-ttu-id="dc056-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="dc056-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc056-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="dc056-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc056-121">Ajout de SumoLogic à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="dc056-121">Adding SumoLogic from hello gallery</span></span>
2. <span data-ttu-id="dc056-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc056-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-hello-gallery"></a><span data-ttu-id="dc056-123">Ajout de SumoLogic à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="dc056-123">Adding SumoLogic from hello gallery</span></span>
<span data-ttu-id="dc056-124">intégration de hello tooconfigure de SumoLogic dans Azure AD, vous devez tooadd SumoLogic à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="dc056-124">tooconfigure hello integration of SumoLogic into Azure AD, you need tooadd SumoLogic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dc056-125">**tooadd SumoLogic à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dc056-125">**tooadd SumoLogic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc056-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="dc056-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dc056-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="dc056-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dc056-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dc056-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="dc056-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="dc056-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="dc056-133">Dans la zone de recherche de hello, tapez **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="dc056-133">In hello search box, type **SumoLogic**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="dc056-135">Dans le volet de résultats hello, sélectionnez **SumoLogic**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="dc056-135">In hello results panel, select **SumoLogic**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dc056-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc056-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dc056-138">Dans cette section, vous configurez et vous testez l’authentification unique Azure AD avec SumoLogic, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="dc056-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dc056-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SumoLogic est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc056-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SumoLogic is tooa user in Azure AD.</span></span> <span data-ttu-id="dc056-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans SumoLogic doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="dc056-140">In other words, a link relationship between an Azure AD user and hello related user in SumoLogic needs toobe established.</span></span>

<span data-ttu-id="dc056-141">Dans SumoLogic, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="dc056-141">In SumoLogic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="dc056-142">tooconfigure et test Azure AD l’authentification unique à SumoLogic, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="dc056-142">tooconfigure and test Azure AD single sign-on with SumoLogic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dc056-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="dc056-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dc056-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc056-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dc056-145">**[Création d’un utilisateur de test de SumoLogic](#creating-a-sumologic-test-user)**  -toohave un équivalent de Britta Simon dans SumoLogic est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dc056-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - toohave a counterpart of Britta Simon in SumoLogic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="dc056-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dc056-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dc056-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="dc056-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dc056-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc056-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dc056-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="dc056-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="dc056-150">**tooconfigure Azure AD single sign-on avec SumoLogic, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dc056-150">**tooconfigure Azure AD single sign-on with SumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc056-151">Bonjour portail Azure, sur hello **SumoLogic** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="dc056-151">In hello Azure portal, on hello **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="dc056-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dc056-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="dc056-155">Sur hello **SumoLogic domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc056-155">On hello **SumoLogic Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="dc056-157">a.</span><span class="sxs-lookup"><span data-stu-id="dc056-157">a.</span></span> <span data-ttu-id="dc056-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="dc056-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="dc056-159">b.</span><span class="sxs-lookup"><span data-stu-id="dc056-159">b.</span></span> <span data-ttu-id="dc056-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="dc056-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="dc056-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="dc056-161">These values are not real.</span></span> <span data-ttu-id="dc056-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="dc056-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dc056-163">Contact [équipe de support Client de SumoLogic](https://www.sumologic.com/contact-us/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="dc056-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="dc056-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dc056-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="dc056-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="dc056-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dc056-168">Sur hello **SumoLogic Configuration** , cliquez sur **configurer de SumoLogic** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="dc056-168">On hello **SumoLogic Configuration** section, click **Configure SumoLogic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dc056-169">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="dc056-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="dc056-171">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise SumoLogic tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dc056-171">In a different web browser window, log in tooyour SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="dc056-172">Accédez trop**gérer \> sécurité**.</span><span class="sxs-lookup"><span data-stu-id="dc056-172">Go too**Manage \> Security**.</span></span>
   
    <span data-ttu-id="dc056-173">![Gestion](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Gestion")</span><span class="sxs-lookup"><span data-stu-id="dc056-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="dc056-174">Cliquez sur **SAML**.</span><span class="sxs-lookup"><span data-stu-id="dc056-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="dc056-175">![Paramètres de sécurité globaux](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Paramètres de sécurité globaux")</span><span class="sxs-lookup"><span data-stu-id="dc056-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="dc056-176">À partir de hello **sélectionner une configuration ou de créer un nouveau** , sélectionnez **Azure AD**, puis cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="dc056-176">From hello **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="dc056-177">![Configurer SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configurer SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="dc056-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="dc056-178">Sur hello **configurer SAML 2.0** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc056-178">On hello **Configure SAML 2.0** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="dc056-179">![Configurer SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configurer SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="dc056-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="dc056-180">a.</span><span class="sxs-lookup"><span data-stu-id="dc056-180">a.</span></span> <span data-ttu-id="dc056-181">Bonjour **nom de la Configuration** zone de texte, type **AD Azure**.</span><span class="sxs-lookup"><span data-stu-id="dc056-181">In hello **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="dc056-182">b.</span><span class="sxs-lookup"><span data-stu-id="dc056-182">b.</span></span> <span data-ttu-id="dc056-183">Sélectionnez **Debug Mode**.</span><span class="sxs-lookup"><span data-stu-id="dc056-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="dc056-184">c.</span><span class="sxs-lookup"><span data-stu-id="dc056-184">c.</span></span> <span data-ttu-id="dc056-185">Bonjour **émetteur** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dc056-185">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="dc056-186">d.</span><span class="sxs-lookup"><span data-stu-id="dc056-186">d.</span></span> <span data-ttu-id="dc056-187">Bonjour **URL de demande d’authentification** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dc056-187">In hello **Authn Request URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dc056-188">e.</span><span class="sxs-lookup"><span data-stu-id="dc056-188">e.</span></span> <span data-ttu-id="dc056-189">Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et collez hello l’intégralité du certificat dans **certificat X.509** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="dc056-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="dc056-190">f.</span><span class="sxs-lookup"><span data-stu-id="dc056-190">f.</span></span> <span data-ttu-id="dc056-191">Dans **Email Attribute**, sélectionnez **Use SAML subject**.</span><span class="sxs-lookup"><span data-stu-id="dc056-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="dc056-192">g.</span><span class="sxs-lookup"><span data-stu-id="dc056-192">g.</span></span> <span data-ttu-id="dc056-193">Sélectionnez **SP initiated Login Configuration**.</span><span class="sxs-lookup"><span data-stu-id="dc056-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="dc056-194">h.</span><span class="sxs-lookup"><span data-stu-id="dc056-194">h.</span></span> <span data-ttu-id="dc056-195">Bonjour **chemin d’accès de connexion** zone de texte, type **Azure** et cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="dc056-195">In hello **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="dc056-196">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="dc056-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dc056-197">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="dc056-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dc056-198">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dc056-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dc056-199">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc056-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="dc056-200">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="dc056-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="dc056-202">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dc056-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc056-203">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="dc056-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dc056-205">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dc056-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dc056-207">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="dc056-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dc056-209">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc056-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dc056-211">a.</span><span class="sxs-lookup"><span data-stu-id="dc056-211">a.</span></span> <span data-ttu-id="dc056-212">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dc056-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dc056-213">b.</span><span class="sxs-lookup"><span data-stu-id="dc056-213">b.</span></span> <span data-ttu-id="dc056-214">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dc056-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dc056-215">c.</span><span class="sxs-lookup"><span data-stu-id="dc056-215">c.</span></span> <span data-ttu-id="dc056-216">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="dc056-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dc056-217">d.</span><span class="sxs-lookup"><span data-stu-id="dc056-217">d.</span></span> <span data-ttu-id="dc056-218">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="dc056-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="dc056-219">Création d’un utilisateur de test SumoLogic</span><span class="sxs-lookup"><span data-stu-id="dc056-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="dc056-220">Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooSumoLogic, ils doivent être tooSumoLogic mis en service.</span><span class="sxs-lookup"><span data-stu-id="dc056-220">In order tooenable Azure AD users toolog in tooSumoLogic, they must be provisioned tooSumoLogic.</span></span>  

* <span data-ttu-id="dc056-221">Dans les cas de hello de SumoLogic, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="dc056-221">In hello case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="dc056-222">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dc056-222">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc056-223">Connectez-vous à tooyour **SumoLogic** client.</span><span class="sxs-lookup"><span data-stu-id="dc056-223">Log in tooyour **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="dc056-224">Accédez trop**gérer \> utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="dc056-224">Go too**Manage \> Users**.</span></span>
   
    <span data-ttu-id="dc056-225">![Utilisateurs](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="dc056-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="dc056-226">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="dc056-226">Click **Add**.</span></span>
   
    <span data-ttu-id="dc056-227">![Utilisateurs](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="dc056-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="dc056-228">Sur hello **nouvel utilisateur** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dc056-228">On hello **New User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="dc056-229">![Nouvel utilisateur](./media/active-directory-saas-sumologic-tutorial/ic778563.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="dc056-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="dc056-230">a.</span><span class="sxs-lookup"><span data-stu-id="dc056-230">a.</span></span> <span data-ttu-id="dc056-231">Hello de type associées du compte hello Azure AD vous voulez tooprovision dans hello **prénom**, **nom**, et **messagerie** zones de texte.</span><span class="sxs-lookup"><span data-stu-id="dc056-231">Type hello related information of hello Azure AD account you want tooprovision into hello **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="dc056-232">b.</span><span class="sxs-lookup"><span data-stu-id="dc056-232">b.</span></span> <span data-ttu-id="dc056-233">Sélectionnez un rôle</span><span class="sxs-lookup"><span data-stu-id="dc056-233">Select a role.</span></span>
  
    <span data-ttu-id="dc056-234">c.</span><span class="sxs-lookup"><span data-stu-id="dc056-234">c.</span></span> <span data-ttu-id="dc056-235">Pour **Status (Statut)**, sélectionnez **Active (Actif)**.</span><span class="sxs-lookup"><span data-stu-id="dc056-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="dc056-236">d.</span><span class="sxs-lookup"><span data-stu-id="dc056-236">d.</span></span> <span data-ttu-id="dc056-237">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="dc056-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="dc056-238">Vous pouvez utiliser n’importe quel autre SumoLogic utilisateur compte outil de création ou API fournie par SumoLogic tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="dc056-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dc056-239">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc056-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dc056-240">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSumoLogic.</span><span class="sxs-lookup"><span data-stu-id="dc056-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSumoLogic.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="dc056-242">**tooassign Britta Simon tooSumoLogic, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dc056-242">**tooassign Britta Simon tooSumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc056-243">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dc056-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="dc056-245">Dans la liste des applications hello, sélectionnez **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="dc056-245">In hello applications list, select **SumoLogic**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="dc056-247">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dc056-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="dc056-249">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="dc056-249">Click **Add** button.</span></span> <span data-ttu-id="dc056-250">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dc056-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="dc056-252">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="dc056-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dc056-253">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dc056-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dc056-254">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dc056-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dc056-255">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="dc056-255">Testing single sign-on</span></span>

<span data-ttu-id="dc056-256">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="dc056-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dc056-257">Lorsque vous cliquez sur mosaïque SumoLogic hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour SumoLogic application.</span><span class="sxs-lookup"><span data-stu-id="dc056-257">When you click hello SumoLogic tile in hello Access Panel, you should get automatically signed-on tooyour SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dc056-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="dc056-258">Additional resources</span></span>

* [<span data-ttu-id="dc056-259">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc056-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dc056-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="dc056-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

