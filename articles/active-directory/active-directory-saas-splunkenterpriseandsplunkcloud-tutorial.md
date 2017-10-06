---
title: "Didacticiel : intégration d’Azure Active Directory à Splunk Enterprise et Splunk Cloud | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Splunk Enterprise et Splunk Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 848e0485131321479f2375501b330c798627e7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="60f39-103">Didacticiel : Intégration d’Azure Active Directory avec Splunk Enterprise et Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="60f39-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="60f39-104">Dans ce didacticiel, vous apprendrez comment toointegrate Splunk entreprise et Splunk Cloud avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="60f39-104">In this tutorial, you learn how toointegrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="60f39-105">Intégration Splunk Enterprise et Splunk Cloud à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="60f39-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="60f39-106">Vous pouvez contrôler dans Azure AD qui a accès tooSplunk Enterprise et Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="60f39-106">You can control in Azure AD who has access tooSplunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="60f39-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSplunk entreprise et le Splunk Cloud (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="60f39-107">You can enable your users tooautomatically get signed-on tooSplunk Enterprise and Splunk Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="60f39-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="60f39-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="60f39-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="60f39-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60f39-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="60f39-110">Prerequisites</span></span>

<span data-ttu-id="60f39-111">tooconfigure intégration d’Azure AD avec Splunk Enterprise et Splunk Cloud, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="60f39-111">tooconfigure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need hello following items:</span></span>

- <span data-ttu-id="60f39-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="60f39-112">An Azure AD subscription</span></span>
- <span data-ttu-id="60f39-113">Un abonnement Splunk Enterprise et Splunk Cloud avec l’authentification unique activée</span><span class="sxs-lookup"><span data-stu-id="60f39-113">A Splunk Enterprise and Splunk Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="60f39-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="60f39-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="60f39-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="60f39-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="60f39-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="60f39-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="60f39-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60f39-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="60f39-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="60f39-118">Scenario description</span></span>
<span data-ttu-id="60f39-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="60f39-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="60f39-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="60f39-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="60f39-121">Ajout de Splunk Enterprise et Splunk Cloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="60f39-121">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
2. <span data-ttu-id="60f39-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="60f39-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a><span data-ttu-id="60f39-123">Ajout de Splunk Enterprise et Splunk Cloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="60f39-123">Adding Splunk Enterprise and Splunk Cloud from hello gallery</span></span>
<span data-ttu-id="60f39-124">tooconfigure hello intégration d’entreprise de Splunk et Splunk Cloud dans Azure AD, vous devez tooadd Splunk Enterprise Splunk Cloud de liste de tooyour hello galerie des applications et gérées SaaS.</span><span class="sxs-lookup"><span data-stu-id="60f39-124">tooconfigure hello integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need tooadd Splunk Enterprise and Splunk Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="60f39-125">**tooadd Splunk entreprise et Splunk Cloud à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="60f39-125">**tooadd Splunk Enterprise and Splunk Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="60f39-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="60f39-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="60f39-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="60f39-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="60f39-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="60f39-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="60f39-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="60f39-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="60f39-133">Dans la zone de recherche de hello, tapez **Splunk Enterprise et Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="60f39-133">In hello search box, type **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_search.png)

5. <span data-ttu-id="60f39-135">Dans le volet de résultats hello, sélectionnez **Splunk Enterprise et Splunk Cloud**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="60f39-135">In hello results panel, select **Splunk Enterprise and Splunk Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="60f39-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="60f39-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="60f39-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Splunk Enterprise et Splunk Cloud, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="60f39-138">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="60f39-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur hello équivalent Splunk Enterprise et Splunk Cloud est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60f39-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Splunk Enterprise and Splunk Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="60f39-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Splunk Enterprise et Splunk Cloud doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="60f39-140">In other words, a link relationship between an Azure AD user and hello related user in Splunk Enterprise and Splunk Cloud needs toobe established.</span></span>

<span data-ttu-id="60f39-141">Dans Splunk Enterprise et Splunk Cloud, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="60f39-141">In Splunk Enterprise and Splunk Cloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="60f39-142">tooconfigure et test Azure AD l’authentification unique avec Splunk Enterprise et Splunk Cloud, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="60f39-142">tooconfigure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="60f39-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="60f39-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="60f39-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60f39-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="60f39-145">**[Création d’un utilisateur de test Splunk Enterprise et Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave un équivalent de Britta Simon dans Splunk entreprise et Splunk Cloud qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="60f39-145">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - toohave a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="60f39-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="60f39-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="60f39-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="60f39-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="60f39-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="60f39-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="60f39-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application d’entreprise de Splunk et Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="60f39-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Splunk Enterprise and Splunk Cloud application.</span></span>

<span data-ttu-id="60f39-150">**tooconfigure Azure AD l’authentification unique avec Splunk Enterprise et Splunk nuage, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="60f39-150">**tooconfigure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="60f39-151">Bonjour portail Azure, sur hello **Splunk Enterprise et Splunk Cloud** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="60f39-151">In hello Azure portal, on hello **Splunk Enterprise and Splunk Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="60f39-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="60f39-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_samlbase.png)

3. <span data-ttu-id="60f39-155">Sur hello **Splunk Enterprise, le domaine de Cloud Splunk et URL** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="60f39-155">On hello **Splunk Enterprise and Splunk Cloud Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_url.png)

    <span data-ttu-id="60f39-157">a.</span><span class="sxs-lookup"><span data-stu-id="60f39-157">a.</span></span> <span data-ttu-id="60f39-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="60f39-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
    
    <span data-ttu-id="60f39-159">b.</span><span class="sxs-lookup"><span data-stu-id="60f39-159">b.</span></span> <span data-ttu-id="60f39-160">Bonjour **identificateur** zone de texte, tapez l’URL de votre serveur Splunk hello.</span><span class="sxs-lookup"><span data-stu-id="60f39-160">In hello **Identifier** textbox, type hello URL of your Splunk Server.</span></span>

    <span data-ttu-id="60f39-161">c.</span><span class="sxs-lookup"><span data-stu-id="60f39-161">c.</span></span> <span data-ttu-id="60f39-162">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="60f39-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<splunkserver>/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="60f39-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="60f39-163">These values are not real.</span></span> <span data-ttu-id="60f39-164">Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="60f39-164">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="60f39-165">Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur.</span><span class="sxs-lookup"><span data-stu-id="60f39-165">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="60f39-166">Contact [Splunk entreprise et le Client de Cloud Splunk équipe de support technique](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="60f39-166">Contact [Splunk Enterprise and Splunk Cloud Client support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooget these values.</span></span> 

4. <span data-ttu-id="60f39-167">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="60f39-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_certificate.png) 

5. <span data-ttu-id="60f39-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="60f39-169">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="60f39-171">tooconfigure l’authentification unique sur **Splunk Enterprise et Splunk Cloud** côté, vous devez hello toosend téléchargé **Metadata XML** trop[Splunk Enterprise et Splunk Cloud prennent en charge team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span><span class="sxs-lookup"><span data-stu-id="60f39-171">tooconfigure single sign-on on **Splunk Enterprise and Splunk Cloud** side, you need toosend hello downloaded **Metadata XML** too[Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span></span>

> [!TIP]
> <span data-ttu-id="60f39-172">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="60f39-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="60f39-173">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="60f39-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="60f39-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="60f39-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="60f39-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="60f39-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="60f39-176">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="60f39-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="60f39-178">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="60f39-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="60f39-179">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="60f39-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="60f39-181">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="60f39-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="60f39-183">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="60f39-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="60f39-185">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="60f39-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="60f39-187">a.</span><span class="sxs-lookup"><span data-stu-id="60f39-187">a.</span></span> <span data-ttu-id="60f39-188">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="60f39-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="60f39-189">b.</span><span class="sxs-lookup"><span data-stu-id="60f39-189">b.</span></span> <span data-ttu-id="60f39-190">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="60f39-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="60f39-191">c.</span><span class="sxs-lookup"><span data-stu-id="60f39-191">c.</span></span> <span data-ttu-id="60f39-192">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="60f39-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="60f39-193">d.</span><span class="sxs-lookup"><span data-stu-id="60f39-193">d.</span></span> <span data-ttu-id="60f39-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="60f39-194">Click **Create**.</span></span>
 
### <a name="creating-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="60f39-195">Création d’un utilisateur de test Splunk Enterprise and Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="60f39-195">Creating a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="60f39-196">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Splunk Enterprise et Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="60f39-196">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="60f39-197">Travailler avec [Splunk Enterprise et Splunk Cloud équipe de support technique](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) utilisateurs hello tooadd hello Splunk Enterprise et Splunk Cloud platform.</span><span class="sxs-lookup"><span data-stu-id="60f39-197">Work with  [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) tooadd hello users in hello Splunk Enterprise and Splunk Cloud platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="60f39-198">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="60f39-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="60f39-199">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSplunk Enterprise et Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="60f39-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSplunk Enterprise and Splunk Cloud.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="60f39-201">**tooassign Britta Simon tooSplunk Enterprise et Splunk nuage, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="60f39-201">**tooassign Britta Simon tooSplunk Enterprise and Splunk Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="60f39-202">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="60f39-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="60f39-204">Dans la liste des applications hello, sélectionnez **Splunk Enterprise et Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="60f39-204">In hello applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_app.png) 

3. <span data-ttu-id="60f39-206">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="60f39-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="60f39-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="60f39-208">Click **Add** button.</span></span> <span data-ttu-id="60f39-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="60f39-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="60f39-211">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="60f39-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="60f39-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="60f39-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="60f39-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="60f39-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="60f39-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="60f39-214">Testing single sign-on</span></span>

<span data-ttu-id="60f39-215">Dans cette section, vous testez votre SSOonfiguration d’Active Directory Azure à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="60f39-215">In this section, you test your Azure AD SSOonfiguration using hello Access Panel.</span></span>

<span data-ttu-id="60f39-216">Lorsque vous cliquez sur hello Splunk Enterprise et vignette Splunk Cloud Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Splunk Enterprise et Splunk Cloud une application.</span><span class="sxs-lookup"><span data-stu-id="60f39-216">When you click hello Splunk Enterprise and Splunk Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Splunk Enterprise and Splunk Cloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="60f39-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="60f39-217">Additional resources</span></span>

* [<span data-ttu-id="60f39-218">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60f39-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="60f39-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="60f39-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_203.png

