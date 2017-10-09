---
title: "Didacticiel : Intégration d’Azure Active Directory à TargetProcess | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et TargetProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 05c574e2c18d7f73edc6c094093a6e59d46b8e6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="76baf-103">Didacticiel : Intégration d’Azure AD à TargetProcess</span><span class="sxs-lookup"><span data-stu-id="76baf-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="76baf-104">Dans ce didacticiel, vous apprendrez comment toointegrate TargetProcess avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="76baf-104">In this tutorial, you learn how toointegrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="76baf-105">Intégration TargetProcess à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="76baf-105">Integrating TargetProcess with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="76baf-106">Vous pouvez contrôler dans Azure AD qui a accès tooTargetProcess</span><span class="sxs-lookup"><span data-stu-id="76baf-106">You can control in Azure AD who has access tooTargetProcess</span></span>
- <span data-ttu-id="76baf-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTargetProcess (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="76baf-107">You can enable your users tooautomatically get signed-on tooTargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="76baf-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="76baf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="76baf-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="76baf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76baf-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="76baf-110">Prerequisites</span></span>

<span data-ttu-id="76baf-111">tooconfigure intégration d’Azure AD avec TargetProcess, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="76baf-111">tooconfigure Azure AD integration with TargetProcess, you need hello following items:</span></span>

- <span data-ttu-id="76baf-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="76baf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="76baf-113">Un abonnement TargetProcess pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="76baf-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="76baf-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="76baf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="76baf-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="76baf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="76baf-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="76baf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="76baf-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="76baf-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="76baf-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="76baf-118">Scenario description</span></span>
<span data-ttu-id="76baf-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="76baf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="76baf-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="76baf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="76baf-121">Ajouter des TargetProcess à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="76baf-121">Add TargetProcess from hello gallery</span></span>
2. <span data-ttu-id="76baf-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="76baf-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-hello-gallery"></a><span data-ttu-id="76baf-123">Ajouter des TargetProcess à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="76baf-123">Add TargetProcess from hello gallery</span></span>
<span data-ttu-id="76baf-124">intégration de hello tooconfigure de TargetProcess dans Azure AD, vous devez tooadd TargetProcess à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="76baf-124">tooconfigure hello integration of TargetProcess into Azure AD, you need tooadd TargetProcess from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="76baf-125">**tooadd TargetProcess à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="76baf-125">**tooadd TargetProcess from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="76baf-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="76baf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="76baf-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="76baf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="76baf-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="76baf-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="76baf-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="76baf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="76baf-133">Dans la zone de recherche de hello, tapez **TargetProcess**, sélectionnez **TargetProcess** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="76baf-133">In hello search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![Ajouter TargetProcess à partir de la galerie](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="76baf-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="76baf-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="76baf-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD auprès de TargetProcess avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="76baf-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="76baf-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans TargetProcess est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="76baf-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TargetProcess is tooa user in Azure AD.</span></span> <span data-ttu-id="76baf-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans TargetProcess doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="76baf-138">In other words, a link relationship between an Azure AD user and hello related user in TargetProcess needs toobe established.</span></span>

<span data-ttu-id="76baf-139">Dans TargetProcess, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="76baf-139">In TargetProcess, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="76baf-140">tooconfigure et test Azure AD l’authentification unique avec TargetProcess, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="76baf-140">tooconfigure and test Azure AD single sign-on with TargetProcess, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="76baf-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="76baf-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="76baf-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="76baf-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="76baf-143">**[Créer un utilisateur de test TargetProcess](#create-a-targetprocess-test-user)**  -toohave un équivalent de Britta Simon dans TargetProcess est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="76baf-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - toohave a counterpart of Britta Simon in TargetProcess that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="76baf-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="76baf-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="76baf-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="76baf-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="76baf-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="76baf-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="76baf-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="76baf-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="76baf-148">**tooconfigure Azure AD single sign-on avec TargetProcess, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="76baf-148">**tooconfigure Azure AD single sign-on with TargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="76baf-149">Bonjour portail Azure, sur hello **TargetProcess** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="76baf-149">In hello Azure portal, on hello **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="76baf-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="76baf-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Authentification basée sur SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="76baf-153">Sur hello **TargetProcess domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="76baf-153">On hello **TargetProcess Domain and URLs** section, perform hello following steps:</span></span>

    ![Section Domaine et URL TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="76baf-155">a.</span><span class="sxs-lookup"><span data-stu-id="76baf-155">a.</span></span> <span data-ttu-id="76baf-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="76baf-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="76baf-157">b.</span><span class="sxs-lookup"><span data-stu-id="76baf-157">b.</span></span> <span data-ttu-id="76baf-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="76baf-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="76baf-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="76baf-159">These values are not real.</span></span> <span data-ttu-id="76baf-160">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="76baf-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="76baf-161">Contact [équipe de support Client de TargetProcess](mailto:support@targetprocess.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="76baf-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="76baf-162">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="76baf-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Section Certificat de signature SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="76baf-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="76baf-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="76baf-166">Sur hello **TargetProcess Configuration** , cliquez sur **TargetProcess de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="76baf-166">On hello **TargetProcess Configuration** section, click **Configure TargetProcess** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="76baf-167">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="76baf-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Section Configuration de TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="76baf-169">Authentification tooyour application TargetProcess en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="76baf-169">Sign-on tooyour TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="76baf-170">Dans le menu hello haut de hello, cliquez sur **le programme d’installation**.</span><span class="sxs-lookup"><span data-stu-id="76baf-170">In hello menu on hello top, click **Setup**.</span></span>
   
    ![Paramétrage](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="76baf-172">Cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="76baf-172">Click **Settings**.</span></span>
   
    ![Paramètres](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="76baf-174">Cliquez sur **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="76baf-174">Click **Single Sign-on**.</span></span>
   
    ![Cliquer sur Authentification unique](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="76baf-176">Sur hello Single Sign-on boîte de dialogue Paramètres, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="76baf-176">On hello Single Sign-on settings dialog, perform hello following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="76baf-178">a.</span><span class="sxs-lookup"><span data-stu-id="76baf-178">a.</span></span> <span data-ttu-id="76baf-179">Cliquez sur **Enable Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="76baf-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="76baf-180">b.</span><span class="sxs-lookup"><span data-stu-id="76baf-180">b.</span></span> <span data-ttu-id="76baf-181">Dans **URL de connexion** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="76baf-181">In **Sign-on URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="76baf-182">c.</span><span class="sxs-lookup"><span data-stu-id="76baf-182">c.</span></span> <span data-ttu-id="76baf-183">Ouvrez votre certificat téléchargé dans le bloc-notes, hello copie le contenu et le coller ensuite dans hello **certificat** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="76baf-183">Open your downloaded certificate in notepad, copy hello content, and then paste it into hello **Certificate** textbox.</span></span>
    
    <span data-ttu-id="76baf-184">d.</span><span class="sxs-lookup"><span data-stu-id="76baf-184">d.</span></span> <span data-ttu-id="76baf-185">Cliquez sur **Activer la configuration JIT**.</span><span class="sxs-lookup"><span data-stu-id="76baf-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="76baf-186">e.</span><span class="sxs-lookup"><span data-stu-id="76baf-186">e.</span></span> <span data-ttu-id="76baf-187">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="76baf-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="76baf-188">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="76baf-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="76baf-189">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="76baf-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="76baf-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="76baf-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="76baf-191">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="76baf-191">Create an Azure AD test user</span></span>
<span data-ttu-id="76baf-192">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="76baf-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="76baf-194">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="76baf-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="76baf-195">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="76baf-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="76baf-197">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="76baf-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![liste de hello toodisplay des utilisateurs](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="76baf-199">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="76baf-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="76baf-201">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="76baf-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Section Utilisateur](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="76baf-203">a.</span><span class="sxs-lookup"><span data-stu-id="76baf-203">a.</span></span> <span data-ttu-id="76baf-204">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="76baf-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="76baf-205">b.</span><span class="sxs-lookup"><span data-stu-id="76baf-205">b.</span></span> <span data-ttu-id="76baf-206">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="76baf-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="76baf-207">c.</span><span class="sxs-lookup"><span data-stu-id="76baf-207">c.</span></span> <span data-ttu-id="76baf-208">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="76baf-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="76baf-209">d.</span><span class="sxs-lookup"><span data-stu-id="76baf-209">d.</span></span> <span data-ttu-id="76baf-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="76baf-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="76baf-211">Créer un utilisateur de test TargetProcess</span><span class="sxs-lookup"><span data-stu-id="76baf-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="76baf-212">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="76baf-212">hello objective of this section is toocreate a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="76baf-213">TargetProcess prend en charge l’approvisionnement juste-à-temps.</span><span class="sxs-lookup"><span data-stu-id="76baf-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="76baf-214">Vous l’avez déjà activé dans [Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="76baf-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="76baf-215">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="76baf-215">There is no action item for you in this section.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="76baf-216">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="76baf-216">Assign hello Azure AD test user</span></span>

<span data-ttu-id="76baf-217">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTargetProcess.</span><span class="sxs-lookup"><span data-stu-id="76baf-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTargetProcess.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="76baf-219">**tooassign Britta Simon tooTargetProcess, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="76baf-219">**tooassign Britta Simon tooTargetProcess, perform hello following steps:**</span></span>

1. <span data-ttu-id="76baf-220">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="76baf-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="76baf-222">Dans la liste des applications hello, sélectionnez **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="76baf-222">In hello applications list, select **TargetProcess**.</span></span>

    ![TargetProcess dans la liste des applications](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="76baf-224">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="76baf-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="76baf-226">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="76baf-226">Click **Add** button.</span></span> <span data-ttu-id="76baf-227">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="76baf-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="76baf-229">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="76baf-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="76baf-230">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="76baf-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="76baf-231">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="76baf-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="76baf-232">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="76baf-232">Test single sign-on</span></span>

<span data-ttu-id="76baf-233">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="76baf-233">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="76baf-234">Lorsque vous cliquez sur hello TargetProcess vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour TargetProcess application.</span><span class="sxs-lookup"><span data-stu-id="76baf-234">When you click hello TargetProcess tile in hello Access Panel, you should get automatically signed-on tooyour TargetProcess application.</span></span> <span data-ttu-id="76baf-235">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="76baf-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="76baf-236">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="76baf-236">Additional resources</span></span>

* [<span data-ttu-id="76baf-237">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76baf-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="76baf-238">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="76baf-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

