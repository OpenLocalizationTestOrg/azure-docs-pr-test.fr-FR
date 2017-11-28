---
title: "Didacticiel : Intégration d’Azure Active Directory dans Atlassian Cloud | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de la société Atlassian Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: f679e8b3306bf0efb9373d8baa0cfe095b760aaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="eb947-103">Didacticiel : Intégration d’Azure Active Directory dans Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="eb947-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="eb947-104">Dans ce didacticiel, vous apprendrez comment toointegrate Atlassian Cloud avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb947-104">In this tutorial, you learn how toointegrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eb947-105">Intégration Atlassian Cloud à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="eb947-105">Integrating Atlassian Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eb947-106">Vous pouvez contrôler dans Azure AD qui a accès tooAtlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="eb947-106">You can control in Azure AD who has access tooAtlassian Cloud</span></span>
- <span data-ttu-id="eb947-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAtlassian Cloud (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb947-107">You can enable your users tooautomatically get signed-on tooAtlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eb947-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="eb947-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eb947-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb947-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb947-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="eb947-110">Prerequisites</span></span>

<span data-ttu-id="eb947-111">tooconfigure intégration d’Azure AD avec Atlassian Cloud, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="eb947-111">tooconfigure Azure AD integration with Atlassian Cloud, you need hello following items:</span></span>

- <span data-ttu-id="eb947-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb947-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eb947-113">Un abonnement Atlassian Cloud pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="eb947-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eb947-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="eb947-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eb947-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="eb947-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb947-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="eb947-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eb947-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb947-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eb947-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="eb947-118">Scenario description</span></span>
<span data-ttu-id="eb947-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="eb947-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eb947-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="eb947-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb947-121">Ajout de Atlassian Cloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="eb947-121">Adding Atlassian Cloud from hello gallery</span></span>
2. <span data-ttu-id="eb947-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb947-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-hello-gallery"></a><span data-ttu-id="eb947-123">Ajout de Atlassian Cloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="eb947-123">Adding Atlassian Cloud from hello gallery</span></span>
<span data-ttu-id="eb947-124">intégration de hello tooconfigure de Atlassian Cloud dans Azure AD, vous devez tooadd Atlassian Cloud à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="eb947-124">tooconfigure hello integration of Atlassian Cloud into Azure AD, you need tooadd Atlassian Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eb947-125">**tooadd Atlassian Cloud à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb947-125">**tooadd Atlassian Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb947-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="eb947-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eb947-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="eb947-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eb947-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="eb947-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="eb947-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="eb947-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="eb947-133">Dans la zone de recherche de hello, tapez **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="eb947-133">In hello search box, type **Atlassian Cloud**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="eb947-135">Dans le volet de résultats hello, sélectionnez **Atlassian Cloud**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="eb947-135">In hello results panel, select **Atlassian Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eb947-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb947-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eb947-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Atlassian Cloud, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="eb947-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eb947-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans le Cloud de Atlassian est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb947-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Atlassian Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="eb947-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le Cloud de Atlassian hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="eb947-140">In other words, a link relationship between an Azure AD user and hello related user in Atlassian Cloud needs toobe established.</span></span>

<span data-ttu-id="eb947-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans le Cloud de la société Atlassian.</span><span class="sxs-lookup"><span data-stu-id="eb947-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="eb947-142">tooconfigure et test Azure AD l’authentification unique avec Atlassian Cloud, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="eb947-142">tooconfigure and test Azure AD single sign-on with Atlassian Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eb947-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="eb947-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eb947-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb947-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb947-145">**[Création d’un utilisateur de test de Cloud de Atlassian](#creating-an-atlassian-cloud-test-user)**  -toohave un équivalent de Britta Simon dans le Cloud de Atlassian est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="eb947-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - toohave a counterpart of Britta Simon in Atlassian Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eb947-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="eb947-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb947-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="eb947-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eb947-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb947-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eb947-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Cloud de la société Atlassian.</span><span class="sxs-lookup"><span data-stu-id="eb947-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="eb947-150">**tooconfigure Azure AD single sign-on avec Atlassian Cloud, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb947-150">**tooconfigure Azure AD single sign-on with Atlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb947-151">Bonjour portail Azure, sur hello **Atlassian Cloud** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="eb947-151">In hello Azure portal, on hello **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="eb947-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="eb947-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="eb947-155">Sur hello **Atlassian Cloud domaine et les URL** section, effectuer hello comme suit si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="eb947-155">On hello **Atlassian Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="eb947-157">a.</span><span class="sxs-lookup"><span data-stu-id="eb947-157">a.</span></span> <span data-ttu-id="eb947-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="eb947-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="eb947-159">b.</span><span class="sxs-lookup"><span data-stu-id="eb947-159">b.</span></span> <span data-ttu-id="eb947-160">Bonjour **URL de réponse** zone de texte, tapez une URL en tant que :`https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="eb947-160">In hello **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="eb947-161">Vérifiez **afficher les paramètres d’URL avancés** et effectuer hello suivant l’étape si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="eb947-161">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="eb947-163">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="eb947-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eb947-164">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="eb947-164">These values are not real.</span></span> <span data-ttu-id="eb947-165">Mettre à jour les valeurs de hello réel identificateur et l’URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="eb947-165">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="eb947-166">Vous pouvez obtenir les valeurs exactes hello à partir de l’écran de Configuration de SAML Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="eb947-166">You can get hello exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="eb947-167">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="eb947-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="eb947-169">Sur hello **Configuration du Cloud Atlassian** , cliquez sur **configurer le nuage Atlassian** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="eb947-169">On hello **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eb947-170">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="eb947-170">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="eb947-172">tooget SSO configuré pour votre application, la connexion toohello Portal Atlassian à l’aide de droits d’administrateur hello.</span><span class="sxs-lookup"><span data-stu-id="eb947-172">tooget SSO configured for your application, login toohello Atlassian Portal using hello administrator rights.</span></span>

8. <span data-ttu-id="eb947-173">Dans la section d’authentification hello Hello barre de navigation gauche, cliquez sur **domaines**.</span><span class="sxs-lookup"><span data-stu-id="eb947-173">In hello Authentication section of hello left navigation click **Domains**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="eb947-175">a.</span><span class="sxs-lookup"><span data-stu-id="eb947-175">a.</span></span> <span data-ttu-id="eb947-176">Dans la zone de texte hello, tapez votre nom de domaine, puis cliquez sur **ajouter un domaine**.</span><span class="sxs-lookup"><span data-stu-id="eb947-176">In hello textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Configurer l’authentification unique](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="eb947-178">b.</span><span class="sxs-lookup"><span data-stu-id="eb947-178">b.</span></span> <span data-ttu-id="eb947-179">domaine de hello tooverify, cliquez sur **Vérifiez**.</span><span class="sxs-lookup"><span data-stu-id="eb947-179">tooverify hello domain, click **Verify**.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="eb947-181">c.</span><span class="sxs-lookup"><span data-stu-id="eb947-181">c.</span></span> <span data-ttu-id="eb947-182">Télécharger le fichier html de vérification de domaine hello, téléchargez-le dossier racine de toohello de site Web de votre domaine, puis cliquez sur **vérifier le domaine**.</span><span class="sxs-lookup"><span data-stu-id="eb947-182">Download hello domain verification html file, upload it toohello root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="eb947-184">d.</span><span class="sxs-lookup"><span data-stu-id="eb947-184">d.</span></span> <span data-ttu-id="eb947-185">Une fois que hello est vérifié, hello valeur Hello **état** champ est **vérifié**.</span><span class="sxs-lookup"><span data-stu-id="eb947-185">Once hello domain is verified, hello value of hello **Status** field is **Verified**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="eb947-187">Dans la barre de navigation gauche hello, cliquez sur **SAML**.</span><span class="sxs-lookup"><span data-stu-id="eb947-187">In hello left navigation bar, click **SAML**.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="eb947-189">Créer une Configuration de SAML et ajouter la configuration du fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="eb947-189">Create a SAML Configuration and add hello Identity provider configuration.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="eb947-191">a.</span><span class="sxs-lookup"><span data-stu-id="eb947-191">a.</span></span> <span data-ttu-id="eb947-192">Bonjour **fournisseur d’identité de l’entité** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="eb947-192">In hello **Identity provider Entity ID** text box, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="eb947-193">b.</span><span class="sxs-lookup"><span data-stu-id="eb947-193">b.</span></span> <span data-ttu-id="eb947-194">Bonjour **fournisseur d’identité URL SSO** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="eb947-194">In hello **Identity provider SSO URL** text box, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="eb947-195">c.</span><span class="sxs-lookup"><span data-stu-id="eb947-195">c.</span></span> <span data-ttu-id="eb947-196">Ouvrez le certificat hello téléchargé à partir de Azure portal et copie les valeurs de hello sans hello début et fin des lignes et les coller dans hello **X509 Public certificat** boîte.</span><span class="sxs-lookup"><span data-stu-id="eb947-196">Open hello downloaded certificate from Azure portal and copy hello values without hello Begin and End lines and paste it in hello **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="eb947-197">d.</span><span class="sxs-lookup"><span data-stu-id="eb947-197">d.</span></span> <span data-ttu-id="eb947-198">Cliquez sur **enregistrer la Configuration** tooSave les paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="eb947-198">Click **Save Configuration**  tooSave hello settings.</span></span>
     
11. <span data-ttu-id="eb947-199">Mettre à jour toomake de paramètres hello Azure AD que vous avez hello du programme d’installation corriger les URL d’identificateur.</span><span class="sxs-lookup"><span data-stu-id="eb947-199">Update hello Azure AD settings toomake sure that you have setup hello correct Identifier URL.</span></span>
  
    <span data-ttu-id="eb947-200">a.</span><span class="sxs-lookup"><span data-stu-id="eb947-200">a.</span></span> <span data-ttu-id="eb947-201">Hello de copie **ID d’identité SP** hello SAML à partir de l’écran et la coller dans Azure AD en tant que hello **identificateur** valeur.</span><span class="sxs-lookup"><span data-stu-id="eb947-201">Copy hello **SP Identity ID** from hello SAML screen and paste it in Azure AD as hello **Identifier** value.</span></span>

    <span data-ttu-id="eb947-202">b.</span><span class="sxs-lookup"><span data-stu-id="eb947-202">b.</span></span> <span data-ttu-id="eb947-203">URL de connexion est URL hello du client de votre Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="eb947-203">Sign On URL is hello tenant URL of your Atlassian Cloud.</span></span>     

     ![Configurer l’authentification unique](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="eb947-205">Bonjour portail Azure, cliquez sur **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="eb947-205">In hello Azure portal, Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="eb947-207">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="eb947-207">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eb947-208">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="eb947-208">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eb947-209">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eb947-209">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eb947-210">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb947-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="eb947-211">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="eb947-211">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="eb947-213">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb947-213">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb947-214">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="eb947-214">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eb947-216">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="eb947-216">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eb947-218">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="eb947-218">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eb947-220">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="eb947-220">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eb947-222">a.</span><span class="sxs-lookup"><span data-stu-id="eb947-222">a.</span></span> <span data-ttu-id="eb947-223">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb947-223">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb947-224">b.</span><span class="sxs-lookup"><span data-stu-id="eb947-224">b.</span></span> <span data-ttu-id="eb947-225">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eb947-225">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eb947-226">c.</span><span class="sxs-lookup"><span data-stu-id="eb947-226">c.</span></span> <span data-ttu-id="eb947-227">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="eb947-227">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eb947-228">d.</span><span class="sxs-lookup"><span data-stu-id="eb947-228">d.</span></span> <span data-ttu-id="eb947-229">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="eb947-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="eb947-230">Création d’un utilisateur de test Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="eb947-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="eb947-231">tooenable Azure AD les utilisateurs toolog dans tooAtlassian Cloud, vous devez les configurer dans le Cloud de la société Atlassian.</span><span class="sxs-lookup"><span data-stu-id="eb947-231">tooenable Azure AD users toolog in tooAtlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="eb947-232">Pour Atlassian Cloud, cette attribution est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="eb947-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="eb947-233">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb947-233">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb947-234">Dans la section administration de Site de hello, cliquez sur hello **utilisateurs** bouton</span><span class="sxs-lookup"><span data-stu-id="eb947-234">In hello Site administration section, click hello **Users** button</span></span>

    ![Créer un utilisateur Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="eb947-236">Cliquez sur hello **Create User** bouton toocreate un utilisateur Bonjour Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="eb947-236">Click hello **Create User** button toocreate a user in hello Atlassian Cloud</span></span>

    ![Créer un utilisateur Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="eb947-238">Entrez l’utilisateur hello **adresse de messagerie**, **nom d’utilisateur**, et **nom complet** et affecter l’accès à l’application hello.</span><span class="sxs-lookup"><span data-stu-id="eb947-238">Enter hello user's **Email address**, **Username**, and **Full Name** and assign hello application access.</span></span> 

    ![Créer un utilisateur Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="eb947-240">Cliquez sur **créer un utilisateur** bouton, hello e-mail d’invitation toohello que l’utilisateur est envoyé et après acceptation utilisateur de hello hello invitation sera active dans le système de hello.</span><span class="sxs-lookup"><span data-stu-id="eb947-240">Click **Create user** button, it will send hello email invitation toohello user and after accepting hello invitation hello user will be active in hello system.</span></span> 

>[!NOTE] 
><span data-ttu-id="eb947-241">Vous pouvez également créer des utilisateurs de bloc hello en cliquant sur hello **en bloc créer** bouton Bonjour section utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="eb947-241">You can also create hello bulk users by clicking hello **Bulk Create** button in hello Users section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eb947-242">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb947-242">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eb947-243">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAtlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="eb947-243">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAtlassian Cloud.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="eb947-245">**tooassign Britta Simon tooAtlassian nuage, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="eb947-245">**tooassign Britta Simon tooAtlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb947-246">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="eb947-246">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="eb947-248">Dans la liste des applications hello, sélectionnez **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="eb947-248">In hello applications list, select **Atlassian Cloud**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="eb947-250">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="eb947-250">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="eb947-252">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="eb947-252">Click **Add** button.</span></span> <span data-ttu-id="eb947-253">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="eb947-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="eb947-255">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="eb947-255">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eb947-256">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="eb947-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eb947-257">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="eb947-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eb947-258">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="eb947-258">Testing single sign-on</span></span>

<span data-ttu-id="eb947-259">Dans cette section, vous tester votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="eb947-259">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="eb947-260">Lorsque vous cliquez sur hello Atlassian Cloud vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="eb947-260">When you click hello Atlassian Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Atlassian Cloud application.</span></span> <span data-ttu-id="eb947-261">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eb947-261">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="eb947-262">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="eb947-262">Additional resources</span></span>

* [<span data-ttu-id="eb947-263">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb947-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb947-264">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="eb947-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

