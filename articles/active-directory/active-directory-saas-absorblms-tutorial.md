---
title: "Didacticiel : Intégration d’Azure Active Directory à Absorb LMS | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et absorber les LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="28a3f-103">Didacticiel : Intégration d’Azure Active Directory avec Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="28a3f-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="28a3f-104">Dans ce didacticiel, vous apprendrez comment toointegrate absorber LMS avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="28a3f-104">In this tutorial, you learn how toointegrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="28a3f-105">L’intégration d’absorber les LMS avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="28a3f-105">Integrating Absorb LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="28a3f-106">Vous pouvez contrôler dans Azure AD qui a accès tooAbsorb LMS</span><span class="sxs-lookup"><span data-stu-id="28a3f-106">You can control in Azure AD who has access tooAbsorb LMS</span></span>
- <span data-ttu-id="28a3f-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAbsorb LMS (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="28a3f-107">You can enable your users tooautomatically get signed-on tooAbsorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="28a3f-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="28a3f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="28a3f-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez.</span><span class="sxs-lookup"><span data-stu-id="28a3f-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="28a3f-110">[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="28a3f-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28a3f-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="28a3f-111">Prerequisites</span></span>

<span data-ttu-id="28a3f-112">tooconfigure intégration d’Azure AD à absorber les LMS, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="28a3f-112">tooconfigure Azure AD integration with Absorb LMS, you need hello following items:</span></span>

- <span data-ttu-id="28a3f-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="28a3f-113">An Azure AD subscription</span></span>
- <span data-ttu-id="28a3f-114">Un abonnement Absorb LMS pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="28a3f-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="28a3f-115">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="28a3f-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="28a3f-116">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="28a3f-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="28a3f-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="28a3f-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="28a3f-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28a3f-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="28a3f-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="28a3f-119">Scenario description</span></span>
<span data-ttu-id="28a3f-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="28a3f-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="28a3f-121">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="28a3f-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="28a3f-122">Ajout LMS absorber à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="28a3f-122">Adding Absorb LMS from hello gallery</span></span>
2. <span data-ttu-id="28a3f-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="28a3f-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-hello-gallery"></a><span data-ttu-id="28a3f-124">Ajout LMS absorber à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="28a3f-124">Adding Absorb LMS from hello gallery</span></span>
<span data-ttu-id="28a3f-125">tooconfigure hello intégration d’absorber les LMS dans tooAzure AD, vous devez tooadd absorber LMS à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="28a3f-125">tooconfigure hello integration of Absorb LMS in tooAzure AD, you need tooadd Absorb LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="28a3f-126">**tooadd absorber LMS à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="28a3f-126">**tooadd Absorb LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="28a3f-127">Bonjour ** [portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="28a3f-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="28a3f-129">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="28a3f-130">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-130">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="28a3f-132">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="28a3f-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="28a3f-134">Dans la zone de recherche de hello, tapez **absorber les LMS**, sélectionnez **absorber les LMS** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="28a3f-134">In hello search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Absorber LMS dans la liste des résultats hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="28a3f-136">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="28a3f-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="28a3f-137">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Absorb LMS, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="28a3f-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="28a3f-138">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans absorber les LMS est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28a3f-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Absorb LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="28a3f-139">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans absorber les LMS doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="28a3f-139">In other words, a link relationship between an Azure AD user and hello related user in Absorb LMS needs toobe established.</span></span>

<span data-ttu-id="28a3f-140">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans absorber les LMS.</span><span class="sxs-lookup"><span data-stu-id="28a3f-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Absorb LMS.</span></span>

<span data-ttu-id="28a3f-141">tooconfigure et test Azure AD l’authentification unique avec absorber les LMS, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="28a3f-141">tooconfigure and test Azure AD single sign-on with Absorb LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="28a3f-142">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="28a3f-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="28a3f-143">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user) ** -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28a3f-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="28a3f-144">**[Créer un utilisateur de test absorber les LMS](#create-an-absorb-lms-test-user) ** -toohave un équivalent de Britta Simon dans LMS absorber qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="28a3f-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - toohave a counterpart of Britta Simon in Absorb LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="28a3f-145">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="28a3f-145">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="28a3f-146">**[Tester l’authentification unique sur](#test-single-sign-on) ** -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="28a3f-146">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="28a3f-147">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="28a3f-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="28a3f-148">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application absorber les LMS.</span><span class="sxs-lookup"><span data-stu-id="28a3f-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="28a3f-149">**tooconfigure Azure AD single sign-on avec absorber LMS, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="28a3f-149">**tooconfigure Azure AD single sign-on with Absorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="28a3f-150">Bonjour portail Azure, sur hello **absorber les LMS** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-150">In hello Azure portal, on hello **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="28a3f-152">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="28a3f-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="28a3f-154">Sur hello **absorber le domaine LMS et URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="28a3f-154">On hello **Absorb LMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="28a3f-156">a.</span><span class="sxs-lookup"><span data-stu-id="28a3f-156">a.</span></span> <span data-ttu-id="28a3f-157">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="28a3f-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="28a3f-158">b.</span><span class="sxs-lookup"><span data-stu-id="28a3f-158">b.</span></span> <span data-ttu-id="28a3f-159">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="28a3f-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="28a3f-160">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="28a3f-160">These values are not hello real.</span></span> <span data-ttu-id="28a3f-161">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="28a3f-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="28a3f-162">Contact [équipe de support Client de LMS absorber](https://www.absorblms.com/support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="28a3f-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) tooget these values.</span></span> 

4. <span data-ttu-id="28a3f-163">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="28a3f-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="28a3f-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="28a3f-165">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="28a3f-167">Sur hello **absorber les Configuration LMS** , cliquez sur **configurer un LMS absorber** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="28a3f-167">On hello **Absorb LMS Configuration** section, click **Configure Absorb LMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="28a3f-168">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="28a3f-168">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration d’Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="28a3f-170">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise absorber les LMS tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="28a3f-170">In a different web browser window, log in tooyour Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="28a3f-171">Cliquez sur hello **icône compte** sur l’interface d’administration hello.</span><span class="sxs-lookup"><span data-stu-id="28a3f-171">Click hello **Account Icon** on hello admin interface.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="28a3f-173">Cliquez sur **Paramètres du portail**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-173">Click **Portal Settings**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="28a3f-175">Cliquez sur hello **utilisateurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="28a3f-175">Click hello **Users** tab.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="28a3f-177">Effectuez hello suivant les étapes tooaccess hello l’authentification unique sur les champs de configuration :</span><span class="sxs-lookup"><span data-stu-id="28a3f-177">Perform hello following steps tooaccess hello Single Sign-On configuration fields:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="28a3f-179">a.</span><span class="sxs-lookup"><span data-stu-id="28a3f-179">a.</span></span> <span data-ttu-id="28a3f-180">Sélectionnez hello approprié **Mode**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-180">Select hello appropriate **Mode**.</span></span>

    <span data-ttu-id="28a3f-181">b.</span><span class="sxs-lookup"><span data-stu-id="28a3f-181">b.</span></span> <span data-ttu-id="28a3f-182">Ouvrez hello de certificat que vous avez téléchargé à partir de hello portail Azure dans le bloc-notes, supprimez hello **---BEGIN CERTIFICATE---** et **---END CERTIFICATE---** balise, puis collez hello restant contenu dans Hello **clé** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="28a3f-182">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Key** textbox.</span></span>
    
    <span data-ttu-id="28a3f-183">c.</span><span class="sxs-lookup"><span data-stu-id="28a3f-183">c.</span></span> <span data-ttu-id="28a3f-184">Bonjour **Id de propriété**, sélectionnez hello attribut approprié que vous avez configurée comme hello identificateur utilisateur Bonjour Azure AD (par exemple, si le nom d’utilisateur principal hello est sélectionné dans Azure AD, puis le nom d’utilisateur soit sélectionnée ici.)</span><span class="sxs-lookup"><span data-stu-id="28a3f-184">In hello **Id Property**, select hello appropriate attribute which you have configured as hello user identifier in hello Azure AD (For example, If hello userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="28a3f-185">d.</span><span class="sxs-lookup"><span data-stu-id="28a3f-185">d.</span></span> <span data-ttu-id="28a3f-186">Bonjour **URL de connexion**, collez hello **« SAML Sign-On URL du Service unique »** valeur que vous avez copié à partir de hello **configurer l’authentification** fenêtre Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="28a3f-186">In hello **Login URL**, paste hello **“SAML Single Sign-On Service URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="28a3f-187">e.</span><span class="sxs-lookup"><span data-stu-id="28a3f-187">e.</span></span> <span data-ttu-id="28a3f-188">Bonjour **URL de déconnexion**, collez hello **« URL de déconnexion »** valeur que vous avez copié à partir de hello **configurer l’authentification** fenêtre Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="28a3f-188">In hello **Logout URL**, paste hello **“Sign-Out URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

13. <span data-ttu-id="28a3f-189">Activez **« Autoriser uniquement la connexion SSO »**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="28a3f-191">Cliquez sur **Save** (Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="28a3f-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="28a3f-192">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="28a3f-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="28a3f-193">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello ** Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="28a3f-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="28a3f-194">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="28a3f-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="28a3f-195">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="28a3f-195">Create an Azure AD test user</span></span>

<span data-ttu-id="28a3f-196">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="28a3f-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="28a3f-198">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="28a3f-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="28a3f-199">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="28a3f-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="28a3f-201">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="28a3f-203">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="28a3f-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="28a3f-205">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="28a3f-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="28a3f-207">a.</span><span class="sxs-lookup"><span data-stu-id="28a3f-207">a.</span></span> <span data-ttu-id="28a3f-208">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="28a3f-209">b.</span><span class="sxs-lookup"><span data-stu-id="28a3f-209">b.</span></span> <span data-ttu-id="28a3f-210">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="28a3f-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="28a3f-211">c.</span><span class="sxs-lookup"><span data-stu-id="28a3f-211">c.</span></span> <span data-ttu-id="28a3f-212">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="28a3f-213">d.</span><span class="sxs-lookup"><span data-stu-id="28a3f-213">d.</span></span> <span data-ttu-id="28a3f-214">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="28a3f-215">Créer un utilisateur de test Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="28a3f-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="28a3f-216">tooenable Azure AD les utilisateurs toolog dans tooAbsorb LMS, ils doivent être configurés dans tooAbsorb LMS.</span><span class="sxs-lookup"><span data-stu-id="28a3f-216">tooenable Azure AD users toolog in tooAbsorb LMS, they must be provisioned in tooAbsorb LMS.</span></span>  
<span data-ttu-id="28a3f-217">Pour Absorb LMS, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="28a3f-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="28a3f-218">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="28a3f-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="28a3f-219">Ouvrez une session dans tooyour site d’entreprise absorber les LMS en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="28a3f-219">Log in tooyour Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="28a3f-220">Cliquez sur l’onglet **Users** (Utilisateurs).</span><span class="sxs-lookup"><span data-stu-id="28a3f-220">Click **Users** tab.</span></span>

    ![Inviter des personnes](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="28a3f-222">Cliquez sur **utilisateurs** sous hello **utilisateurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="28a3f-222">Click **Users** under hello **Users** tab.</span></span>

    ![Inviter des personnes](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="28a3f-224">Sélectionnez **User** (Utilisateur) dans la liste déroulante **Add New** (Ajouter nouveau).</span><span class="sxs-lookup"><span data-stu-id="28a3f-224">Select **User** from **Add New** drop-down.</span></span>

    ![Inviter des personnes](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="28a3f-226">Sur hello **ajouter un utilisateur** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="28a3f-226">On hello **Add User** page, perform hello following steps:</span></span>

    ![Inviter des personnes](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="28a3f-228">a.</span><span class="sxs-lookup"><span data-stu-id="28a3f-228">a.</span></span> <span data-ttu-id="28a3f-229">Bonjour **prénom** zone de texte, nom du premier type hello comme Brian.</span><span class="sxs-lookup"><span data-stu-id="28a3f-229">In hello **First Name** textbox, type hello first name like Britta.</span></span>

    <span data-ttu-id="28a3f-230">b.</span><span class="sxs-lookup"><span data-stu-id="28a3f-230">b.</span></span> <span data-ttu-id="28a3f-231">Bonjour **nom** zone de texte, tapez nom de famille hello comme Simon.</span><span class="sxs-lookup"><span data-stu-id="28a3f-231">In hello **Last Name** textbox, type hello last name like Simon.</span></span>
    
    <span data-ttu-id="28a3f-232">c.</span><span class="sxs-lookup"><span data-stu-id="28a3f-232">c.</span></span> <span data-ttu-id="28a3f-233">Bonjour **nom d’utilisateur** zone de texte, nom d’utilisateur de type hello comme Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28a3f-233">In hello **Username** textbox, type hello user name like Britta Simon.</span></span>

    <span data-ttu-id="28a3f-234">d.</span><span class="sxs-lookup"><span data-stu-id="28a3f-234">d.</span></span> <span data-ttu-id="28a3f-235">Bonjour **mot de passe** zone de texte, un mot de passe type hello de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28a3f-235">In hello **Password** textbox, type hello password of Britta Simon.</span></span>

    <span data-ttu-id="28a3f-236">e.</span><span class="sxs-lookup"><span data-stu-id="28a3f-236">e.</span></span> <span data-ttu-id="28a3f-237">Bonjour **confirmer le mot de passe** hello de type zone de texte mot de passe.</span><span class="sxs-lookup"><span data-stu-id="28a3f-237">In hello **Confirm Password** textbox, type hello same password.</span></span>
    
    <span data-ttu-id="28a3f-238">f.</span><span class="sxs-lookup"><span data-stu-id="28a3f-238">f.</span></span> <span data-ttu-id="28a3f-239">Définissez-le comme **ACTIVE** (Actif).</span><span class="sxs-lookup"><span data-stu-id="28a3f-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="28a3f-240">Cliquez sur **Save** (Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="28a3f-240">Click **"Save."**</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="28a3f-241">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="28a3f-241">Assign hello Azure AD test user</span></span>

<span data-ttu-id="28a3f-242">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAbsorb LMS.</span><span class="sxs-lookup"><span data-stu-id="28a3f-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAbsorb LMS.</span></span>

![Attribuer le rôle d’utilisateur hello][200]

<span data-ttu-id="28a3f-244">**tooassign Britta Simon tooAbsorb LMS, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="28a3f-244">**tooassign Britta Simon tooAbsorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="28a3f-245">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="28a3f-247">Dans la liste des applications hello, sélectionnez **absorber les LMS**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-247">In hello applications list, select **Absorb LMS**.</span></span>

    ![lien d’absorber les LMS Hello dans la liste des Applications hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="28a3f-249">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. <span data-ttu-id="28a3f-251">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-251">Click **Add** button.</span></span> <span data-ttu-id="28a3f-252">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="28a3f-254">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="28a3f-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="28a3f-255">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="28a3f-256">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="28a3f-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="28a3f-257">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="28a3f-257">Test single sign-on</span></span>

<span data-ttu-id="28a3f-258">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="28a3f-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="28a3f-259">Cliquez sur hello absorber les LMS vignette Bonjour volet d’accès, vous obtiendrez une application d’absorber les LMS automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="28a3f-259">Click hello Absorb LMS tile in hello Access Panel, you will get automatically signed-on tooyour Absorb LMS application.</span></span> <span data-ttu-id="28a3f-260">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="28a3f-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="28a3f-261">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="28a3f-261">Additional resources</span></span>

* [<span data-ttu-id="28a3f-262">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="28a3f-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="28a3f-263">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="28a3f-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

