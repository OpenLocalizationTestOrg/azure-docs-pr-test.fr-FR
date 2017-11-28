---
title: "Didacticiel : Intégration d’Azure Active Directory avec Système de surveillance de température sans fil SensoScientific | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et le système de surveillance de température SensoScientific sans fil."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ee9a924d-ccde-45b0-ab40-877f82f5dfa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: jeedes
ms.openlocfilehash: 4eabf7fc6457c217fd5c0c2539ab88c8110055e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sensoscientific-wireless-temperature-monitoring-system"></a><span data-ttu-id="d6ec4-103">Didacticiel : Intégration d’Azure Active Directory avec Système de surveillance de température sans fil SensoScientific</span><span class="sxs-lookup"><span data-stu-id="d6ec4-103">Tutorial: Azure Active Directory integration with SensoScientific Wireless Temperature Monitoring System</span></span>

<span data-ttu-id="d6ec4-104">Dans ce didacticiel, vous apprendrez comment toointegrate SensoScientific sans fil température système de surveillance avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d6ec4-104">In this tutorial, you learn how toointegrate SensoScientific Wireless Temperature Monitoring System with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d6ec4-105">Intégration de système de surveillance de température SensoScientific sans fil auprès d’Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="d6ec4-105">Integrating SensoScientific Wireless Temperature Monitoring System with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d6ec4-106">Vous pouvez contrôler dans Azure AD qui a accès tooSensoScientific système de surveillance de température sans fil</span><span class="sxs-lookup"><span data-stu-id="d6ec4-106">You can control in Azure AD who has access tooSensoScientific Wireless Temperature Monitoring System</span></span>
- <span data-ttu-id="d6ec4-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSensoScientific système de surveillance sans fil température (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6ec4-107">You can enable your users tooautomatically get signed-on tooSensoScientific Wireless Temperature Monitoring System (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d6ec4-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d6ec4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d6ec4-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d6ec4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6ec4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d6ec4-110">Prerequisites</span></span>

<span data-ttu-id="d6ec4-111">tooconfigure intégration d’Azure AD avec le système de surveillance de température SensoScientific sans fil, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d6ec4-111">tooconfigure Azure AD integration with SensoScientific Wireless Temperature Monitoring System, you need hello following items:</span></span>

- <span data-ttu-id="d6ec4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6ec4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d6ec4-113">Un abonnement Système de surveillance de température sans fil SensoScientific pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="d6ec4-113">A SensoScientific Wireless Temperature Monitoring System single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d6ec4-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d6ec4-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="d6ec4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d6ec4-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d6ec4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d6ec4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d6ec4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="d6ec4-118">Scenario description</span></span>
<span data-ttu-id="d6ec4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d6ec4-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="d6ec4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d6ec4-121">Ajout de système de surveillance de température SensoScientific sans fil à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d6ec4-121">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
2. <span data-ttu-id="d6ec4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6ec4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sensoscientific-wireless-temperature-monitoring-system-from-hello-gallery"></a><span data-ttu-id="d6ec4-123">Ajout de système de surveillance de température SensoScientific sans fil à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="d6ec4-123">Adding SensoScientific Wireless Temperature Monitoring System from hello gallery</span></span>
<span data-ttu-id="d6ec4-124">intégration de hello tooconfigure du système de surveillance de température SensoScientific sans fil dans Azure AD, vous devez tooadd système de surveillance de température SensoScientific sans fil à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-124">tooconfigure hello integration of SensoScientific Wireless Temperature Monitoring System into Azure AD, you need tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d6ec4-125">**tooadd SensoScientific sans fil température analyse système à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d6ec4-125">**tooadd SensoScientific Wireless Temperature Monitoring System from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6ec4-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d6ec4-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d6ec4-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d6ec4-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d6ec4-133">Dans la zone de recherche de hello, tapez **système de surveillance de température SensoScientific sans fil**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-133">In hello search box, type **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_search.png)

5. <span data-ttu-id="d6ec4-135">Dans le volet de résultats hello, sélectionnez **système de surveillance de température SensoScientific sans fil**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-135">In hello results panel, select **SensoScientific Wireless Temperature Monitoring System**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d6ec4-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6ec4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d6ec4-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Système de surveillance de température sans fil SensoScientific avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="d6ec4-138">In this section, you configure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d6ec4-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans le système de surveillance de température SensoScientific sans fil est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SensoScientific Wireless Temperature Monitoring System is tooa user in Azure AD.</span></span> <span data-ttu-id="d6ec4-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le système de surveillance de température SensoScientific sans fil hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-140">In other words, a link relationship between an Azure AD user and hello related user in SensoScientific Wireless Temperature Monitoring System needs toobe established.</span></span>

<span data-ttu-id="d6ec4-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans le système de surveillance de température SensoScientific sans fil.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SensoScientific Wireless Temperature Monitoring System.</span></span>

<span data-ttu-id="d6ec4-142">tooconfigure et test Azure AD l’authentification unique avec le système de surveillance de température SensoScientific sans fil, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="d6ec4-142">tooconfigure and test Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d6ec4-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d6ec4-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d6ec4-145">**[Création d’un utilisateur de test du système de surveillance de température SensoScientific sans fil](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)**  -toohave un équivalent de Britta Simon SensoScientific sans fil température analyse système qui est lié à la représentation sous forme de toohello Azure AD de utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-145">**[Creating a SensoScientific Wireless Temperature Monitoring System test user](#creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user)** - toohave a counterpart of Britta Simon in SensoScientific Wireless Temperature Monitoring System that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d6ec4-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d6ec4-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d6ec4-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6ec4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d6ec4-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de système de surveillance de température SensoScientific sans fil.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SensoScientific Wireless Temperature Monitoring System application.</span></span>

<span data-ttu-id="d6ec4-150">**tooconfigure Azure AD l’authentification unique avec SensoScientific sans fil température surveillance système, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d6ec4-150">**tooconfigure Azure AD single sign-on with SensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6ec4-151">Bonjour portail Azure, sur hello **système de surveillance de température SensoScientific sans fil** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-151">In hello Azure portal, on hello **SensoScientific Wireless Temperature Monitoring System** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="d6ec4-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_samlbase.png)

3. <span data-ttu-id="d6ec4-155">Sur hello **URL et le domaine du système d’analyse SensoScientific sans fil température** section, sans tooperform besoin de toutes les étapes en tant qu’application hello est déjà pré-intégration à Azure :</span><span class="sxs-lookup"><span data-stu-id="d6ec4-155">On hello **SensoScientific Wireless Temperature Monitoring System Domain and URLs** section, no need tooperform any steps as hello app is already pre-integrated with Azure:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_url.png)

4. <span data-ttu-id="d6ec4-157">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_certificate.png) 

5. <span data-ttu-id="d6ec4-159">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="d6ec4-159">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d6ec4-161">Sur hello **Configuration du système d’analyse SensoScientific sans fil température** , cliquez sur **configurer SensoScientific sans fil température analyse le système** tooopen  **Configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-161">On hello **SensoScientific Wireless Temperature Monitoring System Configuration** section, click **Configure SensoScientific Wireless Temperature Monitoring System** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d6ec4-162">Hello de copie **URL de déconnexion, l’ID d’entité SAML** et **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="d6ec4-162">Copy hello **Sign-Out URL, SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_configure.png) 

7. <span data-ttu-id="d6ec4-164">Ouverture de session tooyour application du système de surveillance de température SensoScientific sans fil en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-164">Sign on tooyour SensoScientific Wireless Temperature Monitoring System application as an administrator.</span></span>

8. <span data-ttu-id="d6ec4-165">Dans le menu de navigation hello en haut de hello, cliquez sur **Configuration** et goto **configurer** sous **Single Sign On** tooopen hello Single Sign On Settings.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-165">In hello navigation menu on hello top, click **Configuration** and goto **Configure** under **Single Sign On** tooopen hello Single Sign On Settings.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_admin.png) 

9. <span data-ttu-id="d6ec4-167">Dans **Single Sign On Settings** formulaire effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d6ec4-167">In **Single Sign On Settings** form perform hello following steps:</span></span>
 
    <span data-ttu-id="d6ec4-168">a.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-168">a.</span></span> <span data-ttu-id="d6ec4-169">Sélectionnez **Nom de l’émetteur** comme Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-169">Select **Issuer Name** as Azure AD.</span></span>
    
    <span data-ttu-id="d6ec4-170">b.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-170">b.</span></span> <span data-ttu-id="d6ec4-171">Hello de coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure, dans la zone de texte URL de l’émetteur.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-171">Paste hello **SAML Entity ID** which you have copied from Azure portal into Issuer URL textbox.</span></span>
    
    <span data-ttu-id="d6ec4-172">c.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-172">c.</span></span> <span data-ttu-id="d6ec4-173">Hello de coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure, dans la zone de texte URL de Service unique Sign-On.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-173">Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal into Single Sign-On Service URL textbox.</span></span>

    <span data-ttu-id="d6ec4-174">d.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-174">d.</span></span> <span data-ttu-id="d6ec4-175">Hello de coller **URL de déconnexion** dont vous avez copié à partir du portail Azure, dans la zone de texte URL de Service de déconnexion unique.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-175">Paste hello **Sign-Out URL** which you have copied from Azure portal into Single Sign-Out Service URL textbox.</span></span>

    <span data-ttu-id="d6ec4-176">e.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-176">e.</span></span> <span data-ttu-id="d6ec4-177">Parcourir les certificats hello que vous avez téléchargé à partir du portail Azure et téléchargez ici.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-177">Browse hello certificate which you have downloaded from Azure portal and upload here.</span></span>
    
    <span data-ttu-id="d6ec4-178">f.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-178">f.</span></span> <span data-ttu-id="d6ec4-179">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-179">Click **Save**.</span></span>
  
> [!TIP]
> <span data-ttu-id="d6ec4-180">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="d6ec4-180">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d6ec4-181">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-181">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d6ec4-182">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d6ec4-182">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d6ec4-183">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6ec4-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="d6ec4-184">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-184">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="d6ec4-186">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d6ec4-186">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6ec4-187">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-187">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d6ec4-189">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-189">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d6ec4-191">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-191">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d6ec4-193">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d6ec4-193">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sensoscientific-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d6ec4-195">a.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-195">a.</span></span> <span data-ttu-id="d6ec4-196">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-196">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d6ec4-197">b.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-197">b.</span></span> <span data-ttu-id="d6ec4-198">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-198">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d6ec4-199">c.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-199">c.</span></span> <span data-ttu-id="d6ec4-200">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-200">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d6ec4-201">d.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-201">d.</span></span> <span data-ttu-id="d6ec4-202">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-202">Click **Create**.</span></span>
 
### <a name="creating-a-sensoscientific-wireless-temperature-monitoring-system-test-user"></a><span data-ttu-id="d6ec4-203">Création d’un utilisateur de test Système de surveillance de température sans fil SensoScientific</span><span class="sxs-lookup"><span data-stu-id="d6ec4-203">Creating a SensoScientific Wireless Temperature Monitoring System test user</span></span>

<span data-ttu-id="d6ec4-204">tooenable Azure AD les utilisateurs toolog dans tooSensoScientific système de surveillance de température sans fil, vous devez les configurer dans le système de surveillance de température SensoScientific sans fil.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-204">tooenable Azure AD users toolog in tooSensoScientific Wireless Temperature Monitoring System, they must be provisioned into SensoScientific Wireless Temperature Monitoring System.</span></span> <span data-ttu-id="d6ec4-205">Travailler avec [équipe de support technique de système de surveillance de température SensoScientific sans fil](https://www.sensoscientific.com/contact-us/) pour ajouter des utilisateurs de hello de plate-forme de système de surveillance de température SensoScientific sans fil hello.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-205">Work with [SensoScientific Wireless Temperature Monitoring System support team](https://www.sensoscientific.com/contact-us/) to add hello users in hello SensoScientific Wireless Temperature Monitoring System platform.</span></span> <span data-ttu-id="d6ec4-206">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-206">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d6ec4-207">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d6ec4-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d6ec4-208">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSensoScientific système de surveillance de température sans fil.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSensoScientific Wireless Temperature Monitoring System.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="d6ec4-210">**tooassign Britta Simon tooSensoScientific système de surveillance de température sans fil, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d6ec4-210">**tooassign Britta Simon tooSensoScientific Wireless Temperature Monitoring System, perform hello following steps:**</span></span>

1. <span data-ttu-id="d6ec4-211">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="d6ec4-213">Dans la liste des applications hello, sélectionnez **système de surveillance de température SensoScientific sans fil**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-213">In hello applications list, select **SensoScientific Wireless Temperature Monitoring System**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sensoscientific-tutorial/tutorial_sensoscientificwtms_app.png) 

3. <span data-ttu-id="d6ec4-215">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="d6ec4-217">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-217">Click **Add** button.</span></span> <span data-ttu-id="d6ec4-218">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="d6ec4-220">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d6ec4-221">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d6ec4-222">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d6ec4-223">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d6ec4-223">Testing single sign-on</span></span>

<span data-ttu-id="d6ec4-224">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="d6ec4-225">Cliquez sur la vignette du système de surveillance de température SensoScientific sans fil hello Bonjour volet d’accès, vous serez application du système de surveillance de température SensoScientific sans fil automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="d6ec4-225">Click hello SensoScientific Wireless Temperature Monitoring System tile in hello Access Panel, you will be automatically signed-on tooyour SensoScientific Wireless Temperature Monitoring System application.</span></span> <span data-ttu-id="d6ec4-226">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="d6ec4-226">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d6ec4-227">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d6ec4-227">Additional resources</span></span>

* [<span data-ttu-id="d6ec4-228">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d6ec4-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d6ec4-229">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="d6ec4-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sensoscientific-tutorial/tutorial_general_203.png

