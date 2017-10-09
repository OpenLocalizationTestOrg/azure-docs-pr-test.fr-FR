---
title: "Didacticiel : intégration d’Azure Active Directory à SAP HANA | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et SAP HANA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="71cc3-103">Didacticiel : Intégration d’Azure Active Directory à SAP HANA</span><span class="sxs-lookup"><span data-stu-id="71cc3-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="71cc3-104">Dans ce didacticiel, vous apprendrez comment toointegrate SAP HANA avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="71cc3-104">In this tutorial, you learn how toointegrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="71cc3-105">Intégration de SAP HANA à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="71cc3-105">Integrating SAP HANA with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="71cc3-106">Vous pouvez contrôler dans Azure AD qui a accès tooSAP HANA</span><span class="sxs-lookup"><span data-stu-id="71cc3-106">You can control in Azure AD who has access tooSAP HANA</span></span>
- <span data-ttu-id="71cc3-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSAP HANA (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="71cc3-107">You can enable your users tooautomatically get signed-on tooSAP HANA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="71cc3-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="71cc3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="71cc3-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="71cc3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71cc3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="71cc3-110">Prerequisites</span></span>

<span data-ttu-id="71cc3-111">tooconfigure intégration d’Azure AD avec SAP HANA, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="71cc3-111">tooconfigure Azure AD integration with SAP HANA, you need hello following items:</span></span>

- <span data-ttu-id="71cc3-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="71cc3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="71cc3-113">Un abonnement SAP HANA pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="71cc3-113">A SAP HANA single sign-on enabled subscription</span></span>
- <span data-ttu-id="71cc3-114">Une instance HANA en cours d’exécution sur une IaaS publique, sur site, sur une machine virtuelle Azure ou sur une grande instance SAP dans Azure</span><span class="sxs-lookup"><span data-stu-id="71cc3-114">A running HANA Instance either on any public IaaS, on-premises, Azure VMs or SAP Large Instances in Azure</span></span>
- <span data-ttu-id="71cc3-115">Hello Interface Web d’Administration de XSA ainsi HANA Studio est installé sur l’instance HANA hello.</span><span class="sxs-lookup"><span data-stu-id="71cc3-115">hello XSA Administration Web Interface as well as HANA Studio installed on hello HANA instance.</span></span>

> [!NOTE]
> <span data-ttu-id="71cc3-116">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="71cc3-116">tootest hello steps in this tutorial, we do not recommend using a production environment of SAP HANA.</span></span> <span data-ttu-id="71cc3-117">Tester l’intégration hello d’abord dans le développement ou l’environnement d’application hello, puis utilisez hello production environnement de mise en lots.</span><span class="sxs-lookup"><span data-stu-id="71cc3-117">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="71cc3-118">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="71cc3-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="71cc3-119">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="71cc3-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="71cc3-120">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="71cc3-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="71cc3-121">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="71cc3-121">Scenario description</span></span>
<span data-ttu-id="71cc3-122">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="71cc3-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="71cc3-123">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="71cc3-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="71cc3-124">Ajout de SAP HANA à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="71cc3-124">Adding SAP HANA from hello gallery</span></span>
2. <span data-ttu-id="71cc3-125">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="71cc3-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-hana-from-hello-gallery"></a><span data-ttu-id="71cc3-126">Ajout de SAP HANA à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="71cc3-126">Adding SAP HANA from hello gallery</span></span>
<span data-ttu-id="71cc3-127">tooconfigure hello intégration de SAP HANA dans Azure AD, vous devez tooadd SAP HANA à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="71cc3-127">tooconfigure hello integration of SAP HANA into Azure AD, you need tooadd SAP HANA from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="71cc3-128">**tooadd SAP HANA à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="71cc3-128">**tooadd SAP HANA from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="71cc3-129">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="71cc3-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="71cc3-131">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="71cc3-132">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-132">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="71cc3-134">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="71cc3-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="71cc3-136">Dans la zone de recherche de hello, tapez **SAP HANA**, sélectionnez **SAP HANA** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="71cc3-136">In hello search box, type **SAP HANA**, select **SAP HANA** from result panel then click **Add** button tooadd hello application.</span></span> 

    ![Hello nouvelle application](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="71cc3-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="71cc3-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="71cc3-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP HANA, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="71cc3-139">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="71cc3-140">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SAP HANA est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71cc3-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA is tooa user in Azure AD.</span></span> <span data-ttu-id="71cc3-141">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans SAP HANA doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="71cc3-141">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA needs toobe established.</span></span>

<span data-ttu-id="71cc3-142">Dans SAP HANA, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="71cc3-142">In SAP HANA, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="71cc3-143">tooconfigure et test Azure AD l’authentification unique avec SAP HANA, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="71cc3-143">tooconfigure and test Azure AD single sign-on with SAP HANA, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="71cc3-144">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="71cc3-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="71cc3-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="71cc3-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="71cc3-146">**[Création d’un utilisateur de test SAP HANA](#creating-a-sap-hana-test-user)**  -toohave un équivalent de Britta Simon dans SAP HANA qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="71cc3-146">**[Creating a SAP HANA test user](#creating-a-sap-hana-test-user)** - toohave a counterpart of Britta Simon in SAP HANA that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="71cc3-147">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="71cc3-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="71cc3-148">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="71cc3-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="71cc3-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="71cc3-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="71cc3-150">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="71cc3-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="71cc3-151">**tooconfigure Azure AD single sign-on avec SAP HANA, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="71cc3-151">**tooconfigure Azure AD single sign-on with SAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="71cc3-152">Bonjour portail Azure, sur hello **SAP HANA** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-152">In hello Azure portal, on hello **SAP HANA** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="71cc3-154">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="71cc3-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. <span data-ttu-id="71cc3-156">Sur hello **SAP HANA domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="71cc3-156">On hello **SAP HANA Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="71cc3-158">a.</span><span class="sxs-lookup"><span data-stu-id="71cc3-158">a.</span></span> <span data-ttu-id="71cc3-159">Bonjour **identificateur** type en tant que zone de texte :`HA100`</span><span class="sxs-lookup"><span data-stu-id="71cc3-159">In hello **Identifier** textbox, type as: `HA100`</span></span> 

    <span data-ttu-id="71cc3-160">b.</span><span class="sxs-lookup"><span data-stu-id="71cc3-160">b.</span></span> <span data-ttu-id="71cc3-161">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span><span class="sxs-lookup"><span data-stu-id="71cc3-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="71cc3-162">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="71cc3-162">These values are not real.</span></span> <span data-ttu-id="71cc3-163">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="71cc3-163">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="71cc3-164">Contact [équipe de support SAP HANA Client](https://cloudplatform.sap.com/contact.html) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="71cc3-164">Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="71cc3-165">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="71cc3-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="71cc3-167">Si le certificat n’est pas actif puis activez-le en cliquant sur hello Vérifiez de nouveau certificat » active » la case à cocher Bonjour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71cc3-167">If certificate is not active then make it active by clicking hello “Make new certificate active” checkbox in hello Azure AD.</span></span> 

5. <span data-ttu-id="71cc3-168">Les applications SAP HANA attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="71cc3-168">SAP HANA application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="71cc3-169">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="71cc3-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="71cc3-170">Ici, nous avons mappé hello **identificateur de l’utilisateur** avec **ExtractMailPrefix()** fonction de **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-170">Here we have mapped hello **User Identifier** with **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="71cc3-171">Cela donne la valeur hello préfixe par courrier électronique des utilisateur hello qui est hello ID utilisateur unique.</span><span class="sxs-lookup"><span data-stu-id="71cc3-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="71cc3-172">Ceci est envoyé toohello les applications SAP HANA chaque réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="71cc3-172">This is sent toohello SAP HANA application in every successful response.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. <span data-ttu-id="71cc3-174">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="71cc3-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="71cc3-175">a.</span><span class="sxs-lookup"><span data-stu-id="71cc3-175">a.</span></span> <span data-ttu-id="71cc3-176">Bonjour **identificateur de l’utilisateur** liste déroulante, sélectionnez **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-176">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="71cc3-177">b.</span><span class="sxs-lookup"><span data-stu-id="71cc3-177">b.</span></span> <span data-ttu-id="71cc3-178">Bonjour **Mail** liste déroulante, sélectionnez **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-178">In hello **Mail** dropdown list, select **user.mail**.</span></span>

7. <span data-ttu-id="71cc3-179">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="71cc3-179">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="71cc3-181">tooconfigure l’authentification unique sur **SAP HANA** côté, connexion tooyour **HANA XSA Web Console** en parcourant toohello respectif-point de terminaison HTTPS.</span><span class="sxs-lookup"><span data-stu-id="71cc3-181">tooconfigure single sign-on on **SAP HANA** side, login tooyour **HANA XSA Web Console**  by browsing toohello respective HTTPS-endpoint.</span></span>

    > [!Note]
    > <span data-ttu-id="71cc3-182">Dans la configuration par défaut de hello, URL de hello redirige hello demande tooa écran de connexion, ce qui nécessite des informations d’identification hello d’un processus d’ouverture de session utilisateur toocomplete hello SAP HANA de base de données authentifié.</span><span class="sxs-lookup"><span data-stu-id="71cc3-182">In hello default configuration, hello URL redirects hello request tooa logon screen, which requires hello credentials of an authenticated SAP HANA database user toocomplete hello logon process.</span></span> <span data-ttu-id="71cc3-183">utilisateur de Hello qui se connecte doit disposer des tâches d’administration hello des privilèges requis tooperform SAML.</span><span class="sxs-lookup"><span data-stu-id="71cc3-183">hello user who logs on must have hello privileges required tooperform SAML administration tasks.</span></span>

9. <span data-ttu-id="71cc3-184">Dans l’Interface Web XSA de hello, accédez trop**fournisseur d’identité SAML** à partir de là, cliquez sur hello **« + »** -bouton bas hello du volet de hello écran toodisplay hello ajouter les informations sur le fournisseur d’identité et d’effectuer Hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="71cc3-184">In hello XSA Web Interface, navigate too**SAML Identity Provider** and from there, click hello **“+”** -button on hello bottom of hello screen toodisplay hello Add Identity Provider Info pane and perform hello following steps:</span></span>

    ![Ajouter un fournisseur d’identité](./media/active-directory-saas-saphana-tutorial/sap1.png)

    <span data-ttu-id="71cc3-186">a.</span><span class="sxs-lookup"><span data-stu-id="71cc3-186">a.</span></span> <span data-ttu-id="71cc3-187">Bonjour **ajouter les informations sur le fournisseur d’identité** volet, le contenu de hello coller Hello Metadata XML, que vous avez téléchargé à partir du portail Azure en hello **métadonnées** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="71cc3-187">In hello **Add Identity Provider Info** pane, paste hello contents of hello Metadata XML, which you have downloaded from Azure portal into hello **Metadata** textbox.</span></span>

    ![Paramètres d’ajout d’un fournisseur d’identité](./media/active-directory-saas-saphana-tutorial/sap2.png)

    <span data-ttu-id="71cc3-189">b.</span><span class="sxs-lookup"><span data-stu-id="71cc3-189">b.</span></span> <span data-ttu-id="71cc3-190">Si le contenu de hello du document XML de hello est valides, hello l’analyse de processus extrait tooinsert des informations requises hello dans hello **sujet, ID d’entité et l’émetteur** champs Bonjour données générales zone d’écran et hello champs URL Bonjour Zone d’écran de destination, par exemple,  **URL de Base et SingleSignOn (*)**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-190">If hello contents of hello XML document are valid, hello parsing process extracts hello information required tooinsert into hello **Subject, Entity ID, and Issuer** fields in hello General Data screen area, and hello URL fields in hello Destination screen area, for example, **Base URL and SingleSignOn URL (*)**.</span></span>

    ![Paramètres d’ajout d’un fournisseur d’identité](./media/active-directory-saas-saphana-tutorial/sap3.png)

    <span data-ttu-id="71cc3-192">c.</span><span class="sxs-lookup"><span data-stu-id="71cc3-192">c.</span></span> <span data-ttu-id="71cc3-193">Dans la zone de nom hello Hello données générales écran zone, entrez un nom pour le nouveau fournisseur d’identité SAML SSO hello.</span><span class="sxs-lookup"><span data-stu-id="71cc3-193">In hello Name box of hello General Data screen area, enter a name for hello new SAML SSO identity provider.</span></span>

    > [!Note]
    > <span data-ttu-id="71cc3-194">nom de Hello Hello SAML IDP est obligatoire et doit être unique ; il apparaît dans la liste hello de IDPs SAML disponibles qui s’affiche, si vous sélectionnez SAML comme méthode d’authentification hello pour toouse d’applications SAP HANA XS, par exemple, dans la zone d’écran hello d’authentification de l’outil d’Administration d’artefact XS hello.</span><span class="sxs-lookup"><span data-stu-id="71cc3-194">hello name of hello SAML IDP is mandatory and must be unique; it appears in hello list of available SAML IDPs that is displayed, if you select SAML as hello authentication method for SAP HANA XS applications toouse, for example, in hello Authentication screen area of hello XS Artifact Administration tool.</span></span>

10. <span data-ttu-id="71cc3-195">Enregistrer les détails de hello du nouveau fournisseur d’identité SAML hello.</span><span class="sxs-lookup"><span data-stu-id="71cc3-195">Save hello details of hello new SAML identity provider.</span></span> <span data-ttu-id="71cc3-196">Choisissez **enregistrer** toosave hello détails du fournisseur d’identité SAML hello et ajouter hello SAML IDP toohello liste de connus SAML IDPs.</span><span class="sxs-lookup"><span data-stu-id="71cc3-196">Choose **Save** toosave hello details of hello SAML identity provider and add hello new SAML IDP toohello list of known SAML IDPs.</span></span>

    ![Bouton Enregistrer](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. <span data-ttu-id="71cc3-198">Dans Studio HANA dans Propriétés du système hello Hello **Configuration** , onglet de la filtrer uniquement les paramètres par **saml** et ajustez hello **assertion_timeout** de **10 s** trop**120 s**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-198">In HANA Studio within hello system properties of hello **Configuration** tab, just filter settings by **saml** and adjust hello **assertion_timeout** from **10 sec** too**120 sec**.</span></span>

    ![Paramètre assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="71cc3-200">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="71cc3-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="71cc3-201">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="71cc3-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="71cc3-202">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="71cc3-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="71cc3-203">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="71cc3-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="71cc3-204">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="71cc3-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="71cc3-206">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="71cc3-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="71cc3-207">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="71cc3-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="71cc3-209">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="71cc3-211">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="71cc3-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="71cc3-213">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="71cc3-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="71cc3-215">a.</span><span class="sxs-lookup"><span data-stu-id="71cc3-215">a.</span></span> <span data-ttu-id="71cc3-216">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="71cc3-217">b.</span><span class="sxs-lookup"><span data-stu-id="71cc3-217">b.</span></span> <span data-ttu-id="71cc3-218">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="71cc3-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="71cc3-219">c.</span><span class="sxs-lookup"><span data-stu-id="71cc3-219">c.</span></span> <span data-ttu-id="71cc3-220">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="71cc3-221">d.</span><span class="sxs-lookup"><span data-stu-id="71cc3-221">d.</span></span> <span data-ttu-id="71cc3-222">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-222">Click **Create**.</span></span>
 
### <a name="creating-a-sap-hana-test-user"></a><span data-ttu-id="71cc3-223">Création d’un utilisateur de test SAP HANA</span><span class="sxs-lookup"><span data-stu-id="71cc3-223">Creating a SAP HANA test user</span></span>

<span data-ttu-id="71cc3-224">tooenable Azure AD les utilisateurs toolog dans tooSAP HANA, vous devez les configurer dans SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="71cc3-224">tooenable Azure AD users toolog in tooSAP HANA, they must be provisioned into SAP HANA.</span></span>
<span data-ttu-id="71cc3-225">SAP HANA prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="71cc3-225">SAP HANA supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="71cc3-226">Si vous devez manuellement toocreate un utilisateur, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="71cc3-226">If you need toocreate a user manually, perform hello following steps:</span></span>

>[!Note]
><span data-ttu-id="71cc3-227">Vous pouvez modifier l’authentification externe hello utilisée par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="71cc3-227">You can change hello external authentication used by hello user.</span></span>
<span data-ttu-id="71cc3-228">Les utilisateurs externes sont authentifiés à l’aide d’un système externe, par exemple un système Kerberos.</span><span class="sxs-lookup"><span data-stu-id="71cc3-228">External users are authenticated using an external system, for example a Kerberos system.</span></span> <span data-ttu-id="71cc3-229">Pour plus d’informations sur les identités externes, contactez votre [administrateur de domaine](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="71cc3-229">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="71cc3-230">Ouvrez hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) comme administrateur et activer hello utilisateur de base de données de SSO SAML.</span><span class="sxs-lookup"><span data-stu-id="71cc3-230">Open hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator and enable hello DB-User for SAML SSO.</span></span>

    ![créer un utilisateur](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. <span data-ttu-id="71cc3-232">Toohello de graduation hello invisible de case à cocher à gauche de **SAML** et suivez le lien de configurer hello.</span><span class="sxs-lookup"><span data-stu-id="71cc3-232">Tick hello invisible checkbox toohello left of **SAML** and follow hello Configure link.</span></span>

3. <span data-ttu-id="71cc3-233">Cliquez sur **ajouter** tooadd hello SAML IDP, puis cliquez sur **OK** en sélectionnant hello fournisseur d’identité SAML approprié.</span><span class="sxs-lookup"><span data-stu-id="71cc3-233">Click **Add** tooadd hello SAML IDP and click **OK** selecting hello appropriate SAML IDP.</span></span>

4. <span data-ttu-id="71cc3-234">Ajouter hello **identité externe** (ex.</span><span class="sxs-lookup"><span data-stu-id="71cc3-234">Add hello **External Identity** (ex.</span></span> <span data-ttu-id="71cc3-235">BrittaSimon dans le cas présent) ou choisissez **« Quelconque »** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-235">BrittaSimon here) or choose **"Any"** and click **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="71cc3-236">Si « Tout » case à cocher n’est pas activée, puis nom d’utilisateur hello HANA a besoin de nom de hello tooexactly correspondance d’utilisateur hello Bonjour UPN avant le suffixe de domaine hello (c'est-à-dire BrittaSimon@contoso.com deviendrait BrittaSimon dans HANA).</span><span class="sxs-lookup"><span data-stu-id="71cc3-236">If "ANY" check-box is not checked, then hello user name in HANA needs tooexactly match hello name of hello user in hello UPN before hello domain suffix (i.e. BrittaSimon@contoso.com would become BrittaSimon in HANA).</span></span>

5. <span data-ttu-id="71cc3-237">À des fins de test, affectez-les **« XS »** utilisateur toohello de rôles.</span><span class="sxs-lookup"><span data-stu-id="71cc3-237">For testing purposes, assign all **"XS"** roles toohello user.</span></span>

    ![attribution de rôles](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="71cc3-239">Vous devez donner les autorisations appropriées pour vos cas d’usage, uniquement.</span><span class="sxs-lookup"><span data-stu-id="71cc3-239">You should give those permissions appropriate for your use cases, only.</span></span>

6. <span data-ttu-id="71cc3-240">Enregistrer l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="71cc3-240">Save hello user.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="71cc3-241">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="71cc3-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="71cc3-242">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSAP HANA.</span><span class="sxs-lookup"><span data-stu-id="71cc3-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP HANA.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="71cc3-244">**tooassign Britta Simon tooSAP HANA, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="71cc3-244">**tooassign Britta Simon tooSAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="71cc3-245">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="71cc3-247">Dans la liste des applications hello, sélectionnez **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-247">In hello applications list, select **SAP HANA**.</span></span>

    ![Affecter des utilisateurs](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. <span data-ttu-id="71cc3-249">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. <span data-ttu-id="71cc3-251">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-251">Click **Add** button.</span></span> <span data-ttu-id="71cc3-252">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="71cc3-254">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="71cc3-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="71cc3-255">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="71cc3-256">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="71cc3-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="71cc3-257">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="71cc3-257">Testing single sign-on</span></span>

<span data-ttu-id="71cc3-258">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="71cc3-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="71cc3-259">Lorsque vous cliquez sur mosaïque de SAP HANA hello Bonjour volet d’accès, vous devez obtenir l’application de SAP HANA automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="71cc3-259">When you click hello SAP HANA tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA application.</span></span>
<span data-ttu-id="71cc3-260">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="71cc3-260">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="71cc3-261">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="71cc3-261">Additional resources</span></span>

* [<span data-ttu-id="71cc3-262">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71cc3-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="71cc3-263">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="71cc3-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

