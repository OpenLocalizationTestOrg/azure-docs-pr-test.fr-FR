---
title: "Didacticiel : Intégration d’Azure Active Directory à Qlik Sense Enterprise | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Qlik Sense Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="4b869-103">Didacticiel : Intégration d’Azure Active Directory à Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="4b869-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="4b869-104">Dans ce didacticiel, vous apprendrez comment toointegrate Qlik Sense Enterprise avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4b869-104">In this tutorial, you learn how toointegrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b869-105">Intégration Qlik Sense Enterprise à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4b869-105">Integrating Qlik Sense Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4b869-106">Vous pouvez contrôler dans Azure AD qui a accès tooQlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="4b869-106">You can control in Azure AD who has access tooQlik Sense Enterprise.</span></span>
- <span data-ttu-id="4b869-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooQlik Sense Enterprise (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b869-107">You can enable your users tooautomatically get signed-on tooQlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4b869-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4b869-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="4b869-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4b869-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b869-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4b869-110">Prerequisites</span></span>

<span data-ttu-id="4b869-111">tooconfigure intégration d’Azure AD avec Qlik logique d’entreprise, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4b869-111">tooconfigure Azure AD integration with Qlik Sense Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="4b869-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b869-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b869-113">Un abonnement Qlik Sense Enterprise pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4b869-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b869-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4b869-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b869-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="4b869-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b869-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4b869-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b869-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b869-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b869-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4b869-118">Scenario description</span></span>
<span data-ttu-id="4b869-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4b869-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b869-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="4b869-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b869-121">Ajout de Qlik Sense Enterprise à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4b869-121">Adding Qlik Sense Enterprise from hello gallery</span></span>
2. <span data-ttu-id="4b869-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b869-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a><span data-ttu-id="4b869-123">Ajout de Qlik Sense Enterprise à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4b869-123">Adding Qlik Sense Enterprise from hello gallery</span></span>
<span data-ttu-id="4b869-124">tooconfigure hello intégration d’entreprise de sens Qlik dans Azure AD, vous devez tooadd Qlik Sense Enterprise à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4b869-124">tooconfigure hello integration of Qlik Sense Enterprise into Azure AD, you need tooadd Qlik Sense Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4b869-125">**tooadd Qlik Sense Enterprise à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4b869-125">**tooadd Qlik Sense Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b869-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4b869-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="4b869-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4b869-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4b869-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4b869-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="4b869-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4b869-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="4b869-133">Dans la zone de recherche de hello, tapez **Qlik Sense Enterprise**, sélectionnez **Qlik Sense Enterprise** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4b869-133">In hello search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Qlik Sense Enterprise dans la liste des résultats hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4b869-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b869-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4b869-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Qlik Sense Enterprise avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4b869-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4b869-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Qlik Sense Enterprise est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b869-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Qlik Sense Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="4b869-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Qlik Sense Enterprise doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="4b869-138">In other words, a link relationship between an Azure AD user and hello related user in Qlik Sense Enterprise needs toobe established.</span></span>

<span data-ttu-id="4b869-139">Dans Qlik Sense Enterprise, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="4b869-139">In Qlik Sense Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4b869-140">tooconfigure et test Azure AD l’authentification unique avec Qlik logique d’entreprise, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="4b869-140">tooconfigure and test Azure AD single sign-on with Qlik Sense Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4b869-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4b869-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4b869-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b869-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b869-143">**[Créer un utilisateur de test Qlik Sense Enterprise](#create-a-qlik-sense-enterprise-test-user)**  -toohave un équivalent de Britta Simon dans Qlik Sense Enterprise est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b869-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - toohave a counterpart of Britta Simon in Qlik Sense Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b869-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4b869-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b869-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="4b869-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4b869-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b869-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4b869-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application d’entreprise de sens Qlik.</span><span class="sxs-lookup"><span data-stu-id="4b869-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="4b869-148">**tooconfigure Azure AD l’authentification unique avec Qlik logique d’entreprise, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4b869-148">**tooconfigure Azure AD single sign-on with Qlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b869-149">Bonjour portail Azure, sur hello **Qlik Sense Enterprise** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4b869-149">In hello Azure portal, on hello **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="4b869-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4b869-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="4b869-153">Sur hello **URL et le domaine d’entreprise logique Qlik** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b869-153">On hello **Qlik Sense Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique de domaine et d’URL Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="4b869-155">a.</span><span class="sxs-lookup"><span data-stu-id="4b869-155">a.</span></span> <span data-ttu-id="4b869-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="4b869-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4b869-157">Notez hello oblique à fin hello de cet URI.</span><span class="sxs-lookup"><span data-stu-id="4b869-157">Note hello trailing slash at hello end of this URI.</span></span> <span data-ttu-id="4b869-158">Elle est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="4b869-158">It is required.</span></span>
    
    <span data-ttu-id="4b869-159">b.</span><span class="sxs-lookup"><span data-stu-id="4b869-159">b.</span></span> <span data-ttu-id="4b869-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="4b869-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="4b869-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="4b869-161">These values are not real.</span></span> <span data-ttu-id="4b869-162">Mise à jour ces valeurs avec hello réel Sign-On URL et l’identificateur, qui vous seront expliquées plus loin dans ce didacticiel ou le contact [équipe de support Client d’entreprise logique Qlik](https://www.qlik.com/us/services/support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="4b869-162">Update these values with hello actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="4b869-163">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4b869-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="4b869-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4b869-165">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4b869-167">Préparez le fichier XML des métadonnées de fédération de hello afin que vous pouvez télécharger ce serveur de détection tooQlik.</span><span class="sxs-lookup"><span data-stu-id="4b869-167">Prepare hello Federation Metadata XML file so that you can upload that tooQlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="4b869-168">Avant de télécharger hello IdP métadonnées toohello serveur de détection de Qlik, fichier de hello doit toobe modifié tooremove informations tooensure un bon fonctionnement entre Azure AD et le serveur de détection de Qlik.</span><span class="sxs-lookup"><span data-stu-id="4b869-168">Before uploading hello IdP metadata toohello Qlik Sense server, hello file needs toobe edited tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="4b869-170">a.</span><span class="sxs-lookup"><span data-stu-id="4b869-170">a.</span></span> <span data-ttu-id="4b869-171">Ouvrez le fichier FederationMetaData.xml hello, qui vous avez téléchargé à partir du portail Azure dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="4b869-171">Open hello FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="4b869-172">b.</span><span class="sxs-lookup"><span data-stu-id="4b869-172">b.</span></span> <span data-ttu-id="4b869-173">Recherchez la valeur de hello **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="4b869-173">Search for hello value **RoleDescriptor**.</span></span>  <span data-ttu-id="4b869-174">Il en existe quatre entrées (deux paires de balises d’élément d’ouverture et de fermeture).</span><span class="sxs-lookup"><span data-stu-id="4b869-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="4b869-175">c.</span><span class="sxs-lookup"><span data-stu-id="4b869-175">c.</span></span> <span data-ttu-id="4b869-176">Supprimez les balises RoleDescriptor hello et toutes les informations entre hello fichier.</span><span class="sxs-lookup"><span data-stu-id="4b869-176">Delete hello RoleDescriptor tags and all information in between from hello file.</span></span>
   
    <span data-ttu-id="4b869-177">d.</span><span class="sxs-lookup"><span data-stu-id="4b869-177">d.</span></span> <span data-ttu-id="4b869-178">Enregistrez le fichier de hello et conserver à proximité pour l’utiliser ultérieurement dans ce document.</span><span class="sxs-lookup"><span data-stu-id="4b869-178">Save hello file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="4b869-179">Accédez toohello Qlik sens Qlik Management Console (QMC) en tant qu’utilisateur qui peut créer des configurations de proxy virtuel.</span><span class="sxs-lookup"><span data-stu-id="4b869-179">Navigate toohello Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="4b869-180">Bonjour QMC, cliquez sur hello **proxys virtuel** élément de menu.</span><span class="sxs-lookup"><span data-stu-id="4b869-180">In hello QMC, click on hello **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="4b869-182">Bas hello écran hello, cliquez sur hello **nouvel** bouton.</span><span class="sxs-lookup"><span data-stu-id="4b869-182">At hello bottom of hello screen, click hello **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="4b869-184">écran de modification du proxy Hello virtuel s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4b869-184">hello Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="4b869-185">Sur hello à droite de l’écran hello est un menu pour rendre des options de configuration visibles.</span><span class="sxs-lookup"><span data-stu-id="4b869-185">On hello right side of hello screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="4b869-187">Avec l’option de menu hello d’Identification vérifiée, entrez les informations d’identification pour la configuration de proxy virtuel Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="4b869-187">With hello Identification menu option checked, enter hello identifying information for hello Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="4b869-189">a.</span><span class="sxs-lookup"><span data-stu-id="4b869-189">a.</span></span> <span data-ttu-id="4b869-190">Hello **Description** champ est un nom convivial pour la configuration du proxy virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="4b869-190">hello **Description** field is a friendly name for hello virtual proxy configuration.</span></span>  <span data-ttu-id="4b869-191">Entrez une valeur pour la description.</span><span class="sxs-lookup"><span data-stu-id="4b869-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="4b869-192">b.</span><span class="sxs-lookup"><span data-stu-id="4b869-192">b.</span></span> <span data-ttu-id="4b869-193">Hello **préfixe** champ identifie le point de terminaison de proxy virtuel hello pour la connexion tooQlik sens avec Azure AD Single Sign-On.</span><span class="sxs-lookup"><span data-stu-id="4b869-193">hello **Prefix** field identifies hello virtual proxy endpoint for connecting tooQlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="4b869-194">Entrez un nom de préfixe unique pour ce proxy virtuel.</span><span class="sxs-lookup"><span data-stu-id="4b869-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="4b869-195">c.</span><span class="sxs-lookup"><span data-stu-id="4b869-195">c.</span></span> <span data-ttu-id="4b869-196">**Délai d’inactivité de session (minutes)** est le délai d’attente hello pour les connexions via ce proxy virtuel.</span><span class="sxs-lookup"><span data-stu-id="4b869-196">**Session inactivity timeout (minutes)** is hello timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="4b869-197">d.</span><span class="sxs-lookup"><span data-stu-id="4b869-197">d.</span></span> <span data-ttu-id="4b869-198">Hello **nom d’en-tête de cookie de Session** est un stockage de nom de cookie hello hello identificateur de session pour hello session Qlik sens un utilisateur reçoit après une authentification réussie.</span><span class="sxs-lookup"><span data-stu-id="4b869-198">hello **Session cookie header name** is hello cookie name storing hello session identifier for hello Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="4b869-199">Ce nom doit être unique.</span><span class="sxs-lookup"><span data-stu-id="4b869-199">This name must be unique.</span></span>

12. <span data-ttu-id="4b869-200">Cliquez sur hello authentification menu option toomake il est visible.</span><span class="sxs-lookup"><span data-stu-id="4b869-200">Click on hello Authentication menu option toomake it visible.</span></span>  <span data-ttu-id="4b869-201">écran de l’authentification Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4b869-201">hello Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="4b869-203">a.</span><span class="sxs-lookup"><span data-stu-id="4b869-203">a.</span></span> <span data-ttu-id="4b869-204">Hello **mode d’accès anonyme** liste déroulante détermine si les utilisateurs anonymes peuvent accéder Qlik sens via le proxy virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="4b869-204">hello **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through hello virtual proxy.</span></span>  <span data-ttu-id="4b869-205">option de Hello par défaut n’est aucun utilisateur anonyme.</span><span class="sxs-lookup"><span data-stu-id="4b869-205">hello default option is No anonymous user.</span></span>
    
    <span data-ttu-id="4b869-206">b.</span><span class="sxs-lookup"><span data-stu-id="4b869-206">b.</span></span> <span data-ttu-id="4b869-207">Hello **méthode d’authentification** déroulante détermine hello authentification schéma hello virtuel proxy utilisera.</span><span class="sxs-lookup"><span data-stu-id="4b869-207">hello **Authentication method** drop-down determines hello authentication scheme hello virtual proxy will use.</span></span>  <span data-ttu-id="4b869-208">Sélectionnez SAML à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="4b869-208">Select SAML from hello drop-down list.</span></span>  <span data-ttu-id="4b869-209">À la suite de cette sélection, d’autres options s’affichent.</span><span class="sxs-lookup"><span data-stu-id="4b869-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="4b869-210">c.</span><span class="sxs-lookup"><span data-stu-id="4b869-210">c.</span></span> <span data-ttu-id="4b869-211">Bonjour **champ URI de l’hôte SAML**, les utilisateurs du nom d’hôte d’entrée hello entrent tooaccess Qlik sens via ce proxy virtuel SAML.</span><span class="sxs-lookup"><span data-stu-id="4b869-211">In hello **SAML host URI field**, input hello hostname users enter tooaccess Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="4b869-212">nom d’hôte Hello est uri hello Hello serveur de détection de Qlik.</span><span class="sxs-lookup"><span data-stu-id="4b869-212">hello hostname is hello uri of hello Qlik Sense server.</span></span>
    
    <span data-ttu-id="4b869-213">d.</span><span class="sxs-lookup"><span data-stu-id="4b869-213">d.</span></span> <span data-ttu-id="4b869-214">Bonjour **ID d’entité SAML**, entrez hello même valeur entrée pour le champ URI de hello SAML hôte.</span><span class="sxs-lookup"><span data-stu-id="4b869-214">In hello **SAML entity ID**, enter hello same value entered for hello SAML host URI field.</span></span>
    
    <span data-ttu-id="4b869-215">e.</span><span class="sxs-lookup"><span data-stu-id="4b869-215">e.</span></span> <span data-ttu-id="4b869-216">Hello **SAML IdP metadata** est le fichier hello modifié précédemment dans hello **modifier les métadonnées de fédération à partir de la Configuration d’Azure AD** section.</span><span class="sxs-lookup"><span data-stu-id="4b869-216">hello **SAML IdP metadata** is hello file edited earlier in hello **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="4b869-217">**Avant de télécharger des métadonnées IdP de hello, fichier de hello doit toobe modifié** tooremove informations tooensure fonctionnement entre Azure AD et le serveur de détection de Qlik.</span><span class="sxs-lookup"><span data-stu-id="4b869-217">**Before uploading hello IdP metadata, hello file needs toobe edited** tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="4b869-218">**Si les fichiers hello a encore toobe modifié, consultez instructions toohello ci-dessus.**</span><span class="sxs-lookup"><span data-stu-id="4b869-218">**Please refer toohello instructions above if hello file has yet toobe edited.**</span></span>  <span data-ttu-id="4b869-219">Si hello fichier a été modifié cliquez sur Parcourir hello et tooupload de fichier de métadonnées modifiées hello sélectionnez il configuration du proxy virtuel toohello.</span><span class="sxs-lookup"><span data-stu-id="4b869-219">If hello file has been edited click on hello Browse button and select hello edited metadata file tooupload it toohello virtual proxy configuration.</span></span>
    
    <span data-ttu-id="4b869-220">f.</span><span class="sxs-lookup"><span data-stu-id="4b869-220">f.</span></span> <span data-ttu-id="4b869-221">Entrez la référence de schéma ou le nom de l’attribut hello pour l’attribut SAML de hello représentant hello **UserID** Azure AD envoie toohello serveur de détection de Qlik.</span><span class="sxs-lookup"><span data-stu-id="4b869-221">Enter hello attribute name or schema reference for hello SAML attribute representing hello **UserID** Azure AD sends toohello Qlik Sense server.</span></span>  <span data-ttu-id="4b869-222">Informations de référence de schéma sont disponibles dans hello application Azure écrans après la configuration.</span><span class="sxs-lookup"><span data-stu-id="4b869-222">Schema reference information is available in hello Azure app screens post configuration.</span></span>  <span data-ttu-id="4b869-223">attribut de nom hello toouse, entrez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="4b869-223">toouse hello name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="4b869-224">g.</span><span class="sxs-lookup"><span data-stu-id="4b869-224">g.</span></span> <span data-ttu-id="4b869-225">Entrez la valeur de hello pour hello **répertoire utilisateur** qui sera jointe toousers lors de l’authentification du serveur de détection de tooQlik via Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b869-225">Enter hello value for hello **user directory** that will be attached toousers when they authenticate tooQlik Sense server through Azure AD.</span></span>  <span data-ttu-id="4b869-226">Les valeurs codées en dur doivent être entourées de **crochets []**.</span><span class="sxs-lookup"><span data-stu-id="4b869-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="4b869-227">toouse un attribut envoyé Bonjour assertion Azure AD SAML, entrez le nom hello d’attribut de hello dans cette zone de texte **sans** entre crochets.</span><span class="sxs-lookup"><span data-stu-id="4b869-227">toouse an attribute sent in hello Azure AD SAML assertion, enter hello name of hello attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="4b869-228">h.</span><span class="sxs-lookup"><span data-stu-id="4b869-228">h.</span></span> <span data-ttu-id="4b869-229">Hello **algorithme de signature SAML** jeux hello pour la configuration du proxy virtuel hello de signature de certificat de fournisseur (dans ce cas server de Qlik sens) de service.</span><span class="sxs-lookup"><span data-stu-id="4b869-229">hello **SAML signing algorithm** sets hello service provider (in this case Qlik Sense server) certificate signing for hello virtual proxy configuration.</span></span>  <span data-ttu-id="4b869-230">Si le serveur de détection de Qlik utilise un certificat approuvé est généré à l’aide de Microsoft Enhanced RSA et AES Cryptographic Provider, algorithme de signature SAML hello également modifier**SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="4b869-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change hello SAML signing algorithm too**SHA-256**.</span></span>
    
    <span data-ttu-id="4b869-231">i.</span><span class="sxs-lookup"><span data-stu-id="4b869-231">i.</span></span> <span data-ttu-id="4b869-232">Hello section de mappage d’attribut SAML permet des attributs supplémentaires tels que des groupes toobe envoyé tooQlik sens pour une utilisation dans les règles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="4b869-232">hello SAML attribute mapping section allows for additional attributes like groups toobe sent tooQlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="4b869-233">Cliquez sur hello **l’équilibrage de charge** toomake d’option de menu il est visible.</span><span class="sxs-lookup"><span data-stu-id="4b869-233">Click on hello **LOAD BALANCING** menu option toomake it visible.</span></span>  <span data-ttu-id="4b869-234">écran de l’équilibrage de charge Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4b869-234">hello Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="4b869-236">Cliquez sur hello **ajouter un nœud de serveur** sélectionnez moteur nœud, du bouton ou nœuds Qlik sens envoyer à des fins d’équilibrage de la charge de sessions toofor, cliquez sur hello **ajouter** bouton.</span><span class="sxs-lookup"><span data-stu-id="4b869-236">Click on hello **Add new server node** button, select engine node or nodes Qlik Sense will send sessions toofor load balancing purposes, and click hello **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="4b869-238">Cliquez sur hello menu Avancé option toomake il est visible.</span><span class="sxs-lookup"><span data-stu-id="4b869-238">Click on hello Advanced menu option toomake it visible.</span></span> <span data-ttu-id="4b869-239">écran Avancé Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4b869-239">hello Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="4b869-241">liste d’autorisation Hello hôte identifie les noms d’hôtes qui sont acceptées lors de la connexion toohello serveur de détection de Qlik.</span><span class="sxs-lookup"><span data-stu-id="4b869-241">hello Host white list identifies hostnames that are accepted when connecting toohello Qlik Sense server.</span></span>  <span data-ttu-id="4b869-242">**Entrez le nom d’hôte de l’hello les utilisateurs spécifieront lors de la connexion du serveur de détection de tooQlik.**</span><span class="sxs-lookup"><span data-stu-id="4b869-242">**Enter hello hostname users will specify when connecting tooQlik Sense server.**</span></span> <span data-ttu-id="4b869-243">nom d’hôte Hello est hello même valeur que hello SAML uri de l’hôte sans hello https://.</span><span class="sxs-lookup"><span data-stu-id="4b869-243">hello hostname is hello same value as hello SAML host uri without hello https://.</span></span>

16. <span data-ttu-id="4b869-244">Cliquez sur hello **appliquer** bouton.</span><span class="sxs-lookup"><span data-stu-id="4b869-244">Click hello **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="4b869-246">Cliquez sur OK tooaccept hello avertissement indiquant des proxys toohello lié des proxy virtuel doit être redémarré.</span><span class="sxs-lookup"><span data-stu-id="4b869-246">Click OK tooaccept hello warning message that states proxies linked toohello virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="4b869-248">Sur la droite de l’écran hello hello hello associés éléments apparaît.</span><span class="sxs-lookup"><span data-stu-id="4b869-248">On hello right side of hello screen, hello Associated items menu appears.</span></span>  <span data-ttu-id="4b869-249">Cliquez sur hello **proxys** option de menu.</span><span class="sxs-lookup"><span data-stu-id="4b869-249">Click on hello **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="4b869-251">écran de proxy Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4b869-251">hello proxy screen appears.</span></span>  <span data-ttu-id="4b869-252">Cliquez sur hello **lien** bouton à hello bas toolink un toohello virtuel le proxy.</span><span class="sxs-lookup"><span data-stu-id="4b869-252">Click hello **Link** button at hello bottom toolink a proxy toohello virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="4b869-254">Nœud de proxy hello SELECT qui prend en charge cette connexion proxy virtuel cliquez sur hello **lien** bouton.</span><span class="sxs-lookup"><span data-stu-id="4b869-254">Select hello proxy node that will support this virtual proxy connection and click hello **Link** button.</span></span>  <span data-ttu-id="4b869-255">Après la liaison, le proxy de hello s’afficheront sous proxys associés.</span><span class="sxs-lookup"><span data-stu-id="4b869-255">After linking, hello proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="4b869-258">Après que environ cinq secondes de tooten, hello message d’actualisation de QMC seront affiche.</span><span class="sxs-lookup"><span data-stu-id="4b869-258">After about five tooten seconds, hello Refresh QMC message will appear.</span></span>  <span data-ttu-id="4b869-259">Cliquez sur hello **QMC d’actualiser** bouton.</span><span class="sxs-lookup"><span data-stu-id="4b869-259">Click hello **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="4b869-261">Lorsque hello QMC est actualisé, cliquez sur hello **virtuel proxys** élément de menu.</span><span class="sxs-lookup"><span data-stu-id="4b869-261">When hello QMC refreshes, click on hello **Virtual proxies** menu item.</span></span> <span data-ttu-id="4b869-262">nouvelle entrée de proxy virtuel SAML Hello est répertoriée dans la table hello sur l’écran hello.</span><span class="sxs-lookup"><span data-stu-id="4b869-262">hello new SAML virtual proxy entry is listed in hello table on hello screen.</span></span>  <span data-ttu-id="4b869-263">Clic sur l’entrée de proxy virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="4b869-263">Single click on hello virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="4b869-265">Bouton de métadonnées de télécharger le Service Pack hello activera bas hello écran hello.</span><span class="sxs-lookup"><span data-stu-id="4b869-265">At hello bottom of hello screen, hello Download SP metadata button will activate.</span></span>  <span data-ttu-id="4b869-266">Cliquez sur hello **SP de télécharger des métadonnées** fichier tooa de bouton toosave hello métadonnées.</span><span class="sxs-lookup"><span data-stu-id="4b869-266">Click hello **Download SP metadata** button toosave hello metadata tooa file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="4b869-268">Fichier de métadonnées sp hello ouvert.</span><span class="sxs-lookup"><span data-stu-id="4b869-268">Open hello sp metadata file.</span></span>  <span data-ttu-id="4b869-269">Observez hello **entityID** entrée et hello **AssertionConsumerService** entrée.</span><span class="sxs-lookup"><span data-stu-id="4b869-269">Observe hello **entityID** entry and hello **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="4b869-270">Ces valeurs sont équivalent toohello **identificateur** et hello **URL de connexion** dans la configuration de l’application hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b869-270">These values are equivalent toohello **Identifier** and hello **Sign on URL** in hello Azure AD application configuration.</span></span> <span data-ttu-id="4b869-271">Collez ces valeurs Bonjour **URL et le domaine d’entreprise logique Qlik** section de configuration de l’application hello Azure AD si elles ne correspondent pas, puis vous devez les remplacer dans l’Assistant de configuration de l’application Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="4b869-271">Paste these values in hello **Qlik Sense Enterprise Domain and URLs** section in hello Azure AD application configuration if they are not matching, then you should replace them in hello Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="4b869-273">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="4b869-273">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4b869-274">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="4b869-274">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4b869-275">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b869-275">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4b869-276">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b869-276">Create an Azure AD test user</span></span>
<span data-ttu-id="4b869-277">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="4b869-277">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="4b869-279">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4b869-279">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b869-280">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="4b869-280">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

   ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4b869-282">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4b869-282">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

   ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4b869-284">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4b869-284">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

   ![bouton Ajouter de Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4b869-286">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b869-286">In hello **User** dialog box, perform hello following steps:</span></span>

   ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="4b869-288">a.</span><span class="sxs-lookup"><span data-stu-id="4b869-288">a.</span></span> <span data-ttu-id="4b869-289">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4b869-289">In hello **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="4b869-290">b.</span><span class="sxs-lookup"><span data-stu-id="4b869-290">b.</span></span> <span data-ttu-id="4b869-291">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4b869-291">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

   <span data-ttu-id="4b869-292">c.</span><span class="sxs-lookup"><span data-stu-id="4b869-292">c.</span></span> <span data-ttu-id="4b869-293">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="4b869-293">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

   <span data-ttu-id="4b869-294">d.</span><span class="sxs-lookup"><span data-stu-id="4b869-294">d.</span></span> <span data-ttu-id="4b869-295">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4b869-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="4b869-296">Créer un utilisateur de test Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="4b869-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="4b869-297">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="4b869-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="4b869-298">Travailler avec [équipe de support Client d’entreprise logique Qlik](https://www.qlik.com/us/services/support) pour ajouter des utilisateurs de hello en hello Qlik sens plate-forme.</span><span class="sxs-lookup"><span data-stu-id="4b869-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add hello users in hello Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="4b869-299">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4b869-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4b869-300">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b869-300">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4b869-301">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooQlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="4b869-301">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQlik Sense Enterprise.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="4b869-303">**tooassign Britta Simon tooQlik Sense Enterprise, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4b869-303">**tooassign Britta Simon tooQlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="4b869-304">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4b869-304">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4b869-306">Dans la liste des applications hello, sélectionnez **Qlik Sense Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="4b869-306">In hello applications list, select **Qlik Sense Enterprise**.</span></span>

    ![lien d’entreprise de sens Qlik Hello dans la liste des Applications hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="4b869-308">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4b869-308">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="4b869-310">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4b869-310">Click **Add** button.</span></span> <span data-ttu-id="4b869-311">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4b869-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="4b869-313">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="4b869-313">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4b869-314">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4b869-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b869-315">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4b869-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4b869-316">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4b869-316">Test single sign-on</span></span>

<span data-ttu-id="4b869-317">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="4b869-317">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4b869-318">Lorsque vous cliquez sur mosaïque Qlik Sense Enterprise hello hello volet d’accès, vous devez obtenir l’application d’entreprise de sens de Qlik automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="4b869-318">When you click hello Qlik Sense Enterprise tile in hello Access Panel, you should get automatically signed-on tooyour Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4b869-319">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4b869-319">Additional resources</span></span>

* [<span data-ttu-id="4b869-320">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b869-320">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b869-321">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4b869-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

