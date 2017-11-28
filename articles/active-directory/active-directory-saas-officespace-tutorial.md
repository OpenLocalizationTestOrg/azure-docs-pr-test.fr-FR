---
title: "Didacticiel : Intégration d’Azure Active Directory avec OfficeSpace Software | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory à OfficeSpace Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 95d8413f-db98-4e2c-8097-9142ef1af823
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: b53afb648b8a6057c32c782d857e34c06e152c67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-officespace-software"></a><span data-ttu-id="e3d83-103">Didacticiel : Intégration d’Azure Active Directory avec OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="e3d83-103">Tutorial: Azure Active Directory integration with OfficeSpace Software</span></span>

<span data-ttu-id="e3d83-104">Dans ce didacticiel, vous apprendrez comment toointegrate OfficeSpace Software avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e3d83-104">In this tutorial, you learn how toointegrate OfficeSpace Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e3d83-105">Intégration de OfficeSpace Software à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e3d83-105">Integrating OfficeSpace Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e3d83-106">Vous pouvez contrôler dans Azure AD qui a accès tooOfficeSpace logiciel.</span><span class="sxs-lookup"><span data-stu-id="e3d83-106">You can control in Azure AD who has access tooOfficeSpace Software.</span></span>
- <span data-ttu-id="e3d83-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooOfficeSpace logiciels (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3d83-107">You can enable your users tooautomatically get signed-on tooOfficeSpace Software (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e3d83-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e3d83-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e3d83-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e3d83-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3d83-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e3d83-110">Prerequisites</span></span>

<span data-ttu-id="e3d83-111">tooconfigure intégration d’Azure AD à OfficeSpace Software, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e3d83-111">tooconfigure Azure AD integration with OfficeSpace Software, you need hello following items:</span></span>

- <span data-ttu-id="e3d83-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3d83-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e3d83-113">Un abonnement OfficeSpace Software pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="e3d83-113">A OfficeSpace Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e3d83-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e3d83-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e3d83-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="e3d83-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e3d83-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e3d83-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e3d83-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e3d83-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e3d83-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e3d83-118">Scenario description</span></span>
<span data-ttu-id="e3d83-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e3d83-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e3d83-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="e3d83-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e3d83-121">Ajout de OfficeSpace Software à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e3d83-121">Adding OfficeSpace Software from hello gallery</span></span>
2. <span data-ttu-id="e3d83-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3d83-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-officespace-software-from-hello-gallery"></a><span data-ttu-id="e3d83-123">Ajout de OfficeSpace Software à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e3d83-123">Adding OfficeSpace Software from hello gallery</span></span>
<span data-ttu-id="e3d83-124">intégration de hello tooconfigure de OfficeSpace Software dans Azure AD, vous devez tooadd OfficeSpace Software à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="e3d83-124">tooconfigure hello integration of OfficeSpace Software into Azure AD, you need tooadd OfficeSpace Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e3d83-125">**tooadd OfficeSpace Software à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3d83-125">**tooadd OfficeSpace Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3d83-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e3d83-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="e3d83-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e3d83-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="e3d83-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e3d83-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="e3d83-133">Dans la zone de recherche de hello, tapez **OfficeSpace Software**, sélectionnez **OfficeSpace Software** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e3d83-133">In hello search box, type **OfficeSpace Software**, select **OfficeSpace Software** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste des résultats de OfficeSpace Software Bonjour](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e3d83-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3d83-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e3d83-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec OfficeSpace Software avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e3d83-136">In this section, you configure and test Azure AD single sign-on with OfficeSpace Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e3d83-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans OfficeSpace Software est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e3d83-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in OfficeSpace Software is tooa user in Azure AD.</span></span> <span data-ttu-id="e3d83-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans OfficeSpace Software doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="e3d83-138">In other words, a link relationship between an Azure AD user and hello related user in OfficeSpace Software needs toobe established.</span></span>

<span data-ttu-id="e3d83-139">Dans OfficeSpace Software, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="e3d83-139">In OfficeSpace Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e3d83-140">tooconfigure et test Azure AD l’authentification unique à OfficeSpace Software, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="e3d83-140">tooconfigure and test Azure AD single sign-on with OfficeSpace Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e3d83-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e3d83-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e3d83-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e3d83-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e3d83-143">**[Créer un utilisateur de test de OfficeSpace Software](#create-a-officespace-software-test-user)**  -toohave un équivalent de Britta Simon dans OfficeSpace Software qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e3d83-143">**[Create a OfficeSpace Software test user](#create-a-officespace-software-test-user)** - toohave a counterpart of Britta Simon in OfficeSpace Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e3d83-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e3d83-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e3d83-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="e3d83-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e3d83-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3d83-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e3d83-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="e3d83-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your OfficeSpace Software application.</span></span>

<span data-ttu-id="e3d83-148">**tooconfigure Azure AD single sign-on avec OfficeSpace Software, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3d83-148">**tooconfigure Azure AD single sign-on with OfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3d83-149">Bonjour portail Azure, sur hello **OfficeSpace Software** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-149">In hello Azure portal, on hello **OfficeSpace Software** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="e3d83-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e3d83-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_samlbase.png)

3. <span data-ttu-id="e3d83-153">Sur hello **OfficeSpace Software domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3d83-153">On hello **OfficeSpace Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_url.png)

    <span data-ttu-id="e3d83-155">a.</span><span class="sxs-lookup"><span data-stu-id="e3d83-155">a.</span></span> <span data-ttu-id="e3d83-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.officespacesoftware.com/users/sign_in/saml`</span><span class="sxs-lookup"><span data-stu-id="e3d83-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.officespacesoftware.com/users/sign_in/saml`</span></span>

    <span data-ttu-id="e3d83-157">b.</span><span class="sxs-lookup"><span data-stu-id="e3d83-157">b.</span></span> <span data-ttu-id="e3d83-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`<company name>.officespacesoftware.com`</span><span class="sxs-lookup"><span data-stu-id="e3d83-158">In hello **Identifier** textbox, type a URL using hello following pattern: `<company name>.officespacesoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e3d83-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="e3d83-159">These values are not real.</span></span> <span data-ttu-id="e3d83-160">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="e3d83-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e3d83-161">Contact [équipe de support Client de OfficeSpace Software](mailto:support@officespacesoftware.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="e3d83-161">Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) tooget these values.</span></span> 

4. <span data-ttu-id="e3d83-162">Application OfficeSpace Software attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="e3d83-162">OfficeSpace Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="e3d83-163">Veuillez configurer hello suivant des revendications pour cette application.</span><span class="sxs-lookup"><span data-stu-id="e3d83-163">Please configure hello following claims for this application.</span></span> <span data-ttu-id="e3d83-164">Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="e3d83-164">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="e3d83-165">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="e3d83-165">hello following screenshot shows an example for this.</span></span>
    
    ![Configurer l’attribut](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_attribute.png)

5. <span data-ttu-id="e3d83-167">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, sélectionnez **user.mail** en tant que **identificateur d’utilisateur** et pour chaque ligne indiqué dans le tableau hello ci-dessous, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3d83-167">In hello **User Attributes** section on hello **Single sign-on** dialog, select **user.mail**  as **User Identifier** and for each row shown in hello table below, perform hello following steps:</span></span>
    
    | <span data-ttu-id="e3d83-168">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="e3d83-168">Attribute Name</span></span> | <span data-ttu-id="e3d83-169">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="e3d83-169">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="e3d83-170">email</span><span class="sxs-lookup"><span data-stu-id="e3d83-170">email</span></span> | <span data-ttu-id="e3d83-171">user.mail</span><span class="sxs-lookup"><span data-stu-id="e3d83-171">user.mail</span></span> |
    | <span data-ttu-id="e3d83-172">name</span><span class="sxs-lookup"><span data-stu-id="e3d83-172">name</span></span> | <span data-ttu-id="e3d83-173">user.displayname</span><span class="sxs-lookup"><span data-stu-id="e3d83-173">user.displayname</span></span> |
    | <span data-ttu-id="e3d83-174">first_name</span><span class="sxs-lookup"><span data-stu-id="e3d83-174">first_name</span></span> | <span data-ttu-id="e3d83-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="e3d83-175">user.givenname</span></span> |
    | <span data-ttu-id="e3d83-176">last_name</span><span class="sxs-lookup"><span data-stu-id="e3d83-176">last_name</span></span> | <span data-ttu-id="e3d83-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="e3d83-177">user.surname</span></span> |

    <span data-ttu-id="e3d83-178">a.</span><span class="sxs-lookup"><span data-stu-id="e3d83-178">a.</span></span> <span data-ttu-id="e3d83-179">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e3d83-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![<span data-ttu-id="e3d83-180">Configurer l’ajout</span><span class="sxs-lookup"><span data-stu-id="e3d83-180">Configure Add</span></span> ](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_04.png)

    ![Configurer l’attribut](./media/active-directory-saas-officespace-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="e3d83-182">b.</span><span class="sxs-lookup"><span data-stu-id="e3d83-182">b.</span></span> <span data-ttu-id="e3d83-183">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="e3d83-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="e3d83-184">c.</span><span class="sxs-lookup"><span data-stu-id="e3d83-184">c.</span></span> <span data-ttu-id="e3d83-185">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="e3d83-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="e3d83-186">d.</span><span class="sxs-lookup"><span data-stu-id="e3d83-186">d.</span></span> <span data-ttu-id="e3d83-187">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-187">Click **Ok**</span></span>
 
6. <span data-ttu-id="e3d83-188">Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur du certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="e3d83-188">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of hello certificate.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_certificate.png) 

7. <span data-ttu-id="e3d83-190">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e3d83-190">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-officespace-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e3d83-192">Sur hello **OfficeSpace Software Configuration** , cliquez sur **configurer OfficeSpace Software** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e3d83-192">On hello **OfficeSpace Software Configuration** section, click **Configure OfficeSpace Software** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e3d83-193">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="e3d83-193">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration d’OfficeSpace Software](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_configure.png) 

9. <span data-ttu-id="e3d83-195">Dans une autre fenêtre de navigateur web, connectez-vous à votre locataire OfficeSpace Software en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="e3d83-195">In a different web browser window, log into your OfficeSpace Software tenant as an administrator.</span></span>

10. <span data-ttu-id="e3d83-196">Accédez trop**paramètres** et cliquez sur **connecteurs**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-196">Go too**Settings** and click **Connectors**.</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_002.png)

11. <span data-ttu-id="e3d83-198">Cliquez sur **Authentication SAML**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-198">Click **SAML Authentication**.</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_003.png)

12. <span data-ttu-id="e3d83-200">Bonjour **l’authentification SAML** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3d83-200">In hello **SAML Authentication** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_004.png)

    <span data-ttu-id="e3d83-202">a.</span><span class="sxs-lookup"><span data-stu-id="e3d83-202">a.</span></span> <span data-ttu-id="e3d83-203">Bonjour **url du fournisseur de déconnexion** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e3d83-203">In hello **Logout provider url** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e3d83-204">b.</span><span class="sxs-lookup"><span data-stu-id="e3d83-204">b.</span></span> <span data-ttu-id="e3d83-205">Bonjour **Client idp target url** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e3d83-205">In hello **Client idp target url** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e3d83-206">c.</span><span class="sxs-lookup"><span data-stu-id="e3d83-206">c.</span></span> <span data-ttu-id="e3d83-207">Hello de coller **l’empreinte numérique** valeur sur laquelle vous avez copié à partir du portail Azure, dans hello **empreinte numérique du certificat Client IDP** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="e3d83-207">Paste hello **Thumbprint** value which you have copied from Azure portal, into hello **Client IDP certificate fingerprint** textbox.</span></span> 

    <span data-ttu-id="e3d83-208">d.</span><span class="sxs-lookup"><span data-stu-id="e3d83-208">d.</span></span> <span data-ttu-id="e3d83-209">Cliquez sur **Save Settings**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-209">Click **Save Settings**.</span></span>


> [!TIP]
> <span data-ttu-id="e3d83-210">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="e3d83-210">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e3d83-211">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="e3d83-211">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e3d83-212">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e3d83-212">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e3d83-213">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3d83-213">Create an Azure AD test user</span></span>

<span data-ttu-id="e3d83-214">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="e3d83-214">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="e3d83-216">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3d83-216">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3d83-217">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="e3d83-217">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-officespace-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e3d83-219">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-219">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-officespace-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e3d83-221">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="e3d83-221">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-officespace-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e3d83-223">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3d83-223">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-officespace-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e3d83-225">a.</span><span class="sxs-lookup"><span data-stu-id="e3d83-225">a.</span></span> <span data-ttu-id="e3d83-226">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-226">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e3d83-227">b.</span><span class="sxs-lookup"><span data-stu-id="e3d83-227">b.</span></span> <span data-ttu-id="e3d83-228">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e3d83-228">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e3d83-229">c.</span><span class="sxs-lookup"><span data-stu-id="e3d83-229">c.</span></span> <span data-ttu-id="e3d83-230">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="e3d83-230">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e3d83-231">d.</span><span class="sxs-lookup"><span data-stu-id="e3d83-231">d.</span></span> <span data-ttu-id="e3d83-232">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-232">Click **Create**.</span></span>
 
### <a name="create-a-officespace-software-test-user"></a><span data-ttu-id="e3d83-233">Créer un utilisateur de test OfficeSpace Software</span><span class="sxs-lookup"><span data-stu-id="e3d83-233">Create a OfficeSpace Software test user</span></span>

<span data-ttu-id="e3d83-234">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="e3d83-234">hello objective of this section is toocreate a user called Britta Simon in OfficeSpace Software.</span></span> <span data-ttu-id="e3d83-235">OfficeSpace Software prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="e3d83-235">OfficeSpace Software supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="e3d83-236">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="e3d83-236">There is no action item for you in this section.</span></span> <span data-ttu-id="e3d83-237">Un nouvel utilisateur s’affichera pendant une tentative de tooaccess OfficeSpace Software, s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="e3d83-237">A new user will be created during an attempt tooaccess OfficeSpace Software if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="e3d83-238">Si vous devez manuellement toocreate un utilisateur, vous devez tooContact [équipe de support technique de OfficeSpace Software](mailto:support@officespacesoftware.com).</span><span class="sxs-lookup"><span data-stu-id="e3d83-238">If you need toocreate an user manually, you need tooContact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e3d83-239">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e3d83-239">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e3d83-240">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooOfficeSpace logiciel.</span><span class="sxs-lookup"><span data-stu-id="e3d83-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOfficeSpace Software.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="e3d83-242">**tooassign Britta Simon tooOfficeSpace logiciel, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e3d83-242">**tooassign Britta Simon tooOfficeSpace Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="e3d83-243">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e3d83-245">Dans la liste des applications hello, sélectionnez **OfficeSpace Software**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-245">In hello applications list, select **OfficeSpace Software**.</span></span>

    ![Hello lien OfficeSpace Software dans la liste des Applications hello](./media/active-directory-saas-officespace-tutorial/tutorial_officespace_app.png)  

3. <span data-ttu-id="e3d83-247">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="e3d83-249">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-249">Click **Add** button.</span></span> <span data-ttu-id="e3d83-250">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="e3d83-252">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="e3d83-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e3d83-253">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e3d83-254">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e3d83-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e3d83-255">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e3d83-255">Test single sign-on</span></span>

<span data-ttu-id="e3d83-256">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="e3d83-256">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e3d83-257">Lorsque vous cliquez sur hello OfficeSpace Software vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application OfficeSpace Software.</span><span class="sxs-lookup"><span data-stu-id="e3d83-257">When you click hello OfficeSpace Software tile in hello Access Panel, you should get automatically signed-on tooyour OfficeSpace Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e3d83-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e3d83-258">Additional resources</span></span>

* [<span data-ttu-id="e3d83-259">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3d83-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e3d83-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e3d83-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-officespace-tutorial/tutorial_general_203.png

