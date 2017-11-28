---
title: "Didacticiel : intégration d’Azure Active Directory à SAP HANA | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et SAP HANA."
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
ms.openlocfilehash: a7e73f6ee763d1005ad85935cf2d8f6b24ecf116
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="030f7-103">Didacticiel : Intégration d’Azure Active Directory à SAP HANA</span><span class="sxs-lookup"><span data-stu-id="030f7-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="030f7-104">Dans ce didacticiel, vous allez apprendre à intégrer SAP HANA à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="030f7-104">In this tutorial, you learn how to integrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="030f7-105">L’intégration de SAP HANA à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="030f7-105">Integrating SAP HANA with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="030f7-106">Dans Azure AD, vous pouvez contrôler qui a accès à SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="030f7-106">You can control in Azure AD who has access to SAP HANA</span></span>
- <span data-ttu-id="030f7-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à SAP HANA (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="030f7-107">You can enable your users to automatically get signed-on to SAP HANA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="030f7-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="030f7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="030f7-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="030f7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="030f7-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="030f7-110">Prerequisites</span></span>

<span data-ttu-id="030f7-111">Pour configurer l’intégration d’Azure AD avec SAP HANA, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="030f7-111">To configure Azure AD integration with SAP HANA, you need the following items:</span></span>

- <span data-ttu-id="030f7-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="030f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="030f7-113">Un abonnement SAP HANA pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="030f7-113">A SAP HANA single sign-on enabled subscription</span></span>
- <span data-ttu-id="030f7-114">Une instance HANA en cours d’exécution sur une IaaS publique, sur site, sur une machine virtuelle Azure ou sur une grande instance SAP dans Azure</span><span class="sxs-lookup"><span data-stu-id="030f7-114">A running HANA Instance either on any public IaaS, on-premises, Azure VMs or SAP Large Instances in Azure</span></span>
- <span data-ttu-id="030f7-115">L’interface Web d’administration XSA ainsi que HANA Studio, installés sur l’instance HANA</span><span class="sxs-lookup"><span data-stu-id="030f7-115">The XSA Administration Web Interface as well as HANA Studio installed on the HANA instance.</span></span>

> [!NOTE]
> <span data-ttu-id="030f7-116">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production de SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="030f7-116">To test the steps in this tutorial, we do not recommend using a production environment of SAP HANA.</span></span> <span data-ttu-id="030f7-117">Testez d’abord l’intégration dans l’environnement de développement ou l’environnement intermédiaire de l’application, puis passez à l’environnement de production.</span><span class="sxs-lookup"><span data-stu-id="030f7-117">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="030f7-118">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="030f7-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="030f7-119">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="030f7-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="030f7-120">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="030f7-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="030f7-121">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="030f7-121">Scenario description</span></span>
<span data-ttu-id="030f7-122">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="030f7-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="030f7-123">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="030f7-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="030f7-124">Ajout de SAP HANA à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="030f7-124">Adding SAP HANA from the gallery</span></span>
2. <span data-ttu-id="030f7-125">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="030f7-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-hana-from-the-gallery"></a><span data-ttu-id="030f7-126">Ajout de SAP HANA à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="030f7-126">Adding SAP HANA from the gallery</span></span>
<span data-ttu-id="030f7-127">Pour configurer l’intégration de SAP HANA à Azure AD, vous devez ajouter SAP HANA à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="030f7-127">To configure the integration of SAP HANA into Azure AD, you need to add SAP HANA from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="030f7-128">**Pour ajouter SAP HANA à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="030f7-128">**To add SAP HANA from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="030f7-129">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="030f7-129">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="030f7-131">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="030f7-131">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="030f7-132">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="030f7-132">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="030f7-134">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="030f7-134">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="030f7-136">Dans la zone de recherche, tapez **SAP HANA**, sélectionnez **SAP HANA** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="030f7-136">In the search box, type **SAP HANA**, select **SAP HANA** from result panel then click **Add** button to add the application.</span></span> 

    ![Nouvelle application](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="030f7-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="030f7-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="030f7-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP HANA, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="030f7-139">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="030f7-140">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur SAP HANA équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="030f7-140">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP HANA is to a user in Azure AD.</span></span> <span data-ttu-id="030f7-141">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur SAP HANA associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="030f7-141">In other words, a link relationship between an Azure AD user and the related user in SAP HANA needs to be established.</span></span>

<span data-ttu-id="030f7-142">Dans SAP HANA, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="030f7-142">In SAP HANA, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="030f7-143">Pour configurer et tester l’authentification unique Azure AD avec SAP HANA, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="030f7-143">To configure and test Azure AD single sign-on with SAP HANA, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="030f7-144">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="030f7-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="030f7-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="030f7-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="030f7-146">**[Création d’un utilisateur de test SAP HANA](#creating-a-sap-hana-test-user)** pour avoir un équivalent de Britta Simon dans SAP HANA lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="030f7-146">**[Creating a SAP HANA test user](#creating-a-sap-hana-test-user)** - to have a counterpart of Britta Simon in SAP HANA that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="030f7-147">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="030f7-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="030f7-148">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="030f7-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="030f7-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="030f7-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="030f7-150">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="030f7-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="030f7-151">**Pour configurer l’authentification unique Azure AD avec SAP HANA, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="030f7-151">**To configure Azure AD single sign-on with SAP HANA, perform the following steps:**</span></span>

1. <span data-ttu-id="030f7-152">Dans le portail Azure, sur la page d’intégration de l’application **SAP HANA**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="030f7-152">In the Azure portal, on the **SAP HANA** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="030f7-154">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="030f7-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. <span data-ttu-id="030f7-156">Dans la section **Domaine et URL SAP HANA**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="030f7-156">On the **SAP HANA Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="030f7-158">a.</span><span class="sxs-lookup"><span data-stu-id="030f7-158">a.</span></span> <span data-ttu-id="030f7-159">Dans la zone de texte **Identificateur**, tapez : `HA100`</span><span class="sxs-lookup"><span data-stu-id="030f7-159">In the **Identifier** textbox, type as: `HA100`</span></span> 

    <span data-ttu-id="030f7-160">b.</span><span class="sxs-lookup"><span data-stu-id="030f7-160">b.</span></span> <span data-ttu-id="030f7-161">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span><span class="sxs-lookup"><span data-stu-id="030f7-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="030f7-162">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="030f7-162">These values are not real.</span></span> <span data-ttu-id="030f7-163">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="030f7-163">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="030f7-164">Pour obtenir ces valeurs, contactez l’[équipe de support technique SAP HANA](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="030f7-164">Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) to get these values.</span></span> 

4. <span data-ttu-id="030f7-165">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="030f7-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="030f7-167">Si le certificat n’est pas actif, activez-le en cochant la case « Activer le nouveau certificat » dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="030f7-167">If certificate is not active then make it active by clicking the “Make new certificate active” checkbox in the Azure AD.</span></span> 

5. <span data-ttu-id="030f7-168">L’application SAP HANA attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="030f7-168">SAP HANA application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="030f7-169">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="030f7-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="030f7-170">Ici, nous avons mappé **l’identificateur d’utilisateur** avec la fonction **ExtractMailPrefix()** de **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="030f7-170">Here we have mapped the **User Identifier** with **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="030f7-171">Cela donne la valeur de préfixe de l’adresse de messagerie de l’utilisateur qui est l’ID d’utilisateur unique.</span><span class="sxs-lookup"><span data-stu-id="030f7-171">This gives the prefix value of email of the user which is the unique User ID.</span></span> <span data-ttu-id="030f7-172">Celle-ci est envoyée à l’application SAP HANA pour chaque réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="030f7-172">This is sent to the SAP HANA application in every successful response.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. <span data-ttu-id="030f7-174">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique** :</span><span class="sxs-lookup"><span data-stu-id="030f7-174">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="030f7-175">a.</span><span class="sxs-lookup"><span data-stu-id="030f7-175">a.</span></span> <span data-ttu-id="030f7-176">Dans la liste déroulante **Identificateur de l’utilisateur**, sélectionnez **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="030f7-176">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="030f7-177">b.</span><span class="sxs-lookup"><span data-stu-id="030f7-177">b.</span></span> <span data-ttu-id="030f7-178">Dans la liste déroulante **E-mail**, sélectionnez **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="030f7-178">In the **Mail** dropdown list, select **user.mail**.</span></span>

7. <span data-ttu-id="030f7-179">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="030f7-179">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="030f7-181">Pour configurer l’authentification unique côté **SAP HANA**, connectez-vous à votre **console web HANA XSA** en accédant au point de terminaison HTTPS correspondant.</span><span class="sxs-lookup"><span data-stu-id="030f7-181">To configure single sign-on on **SAP HANA** side, login to your **HANA XSA Web Console**  by browsing to the respective HTTPS-endpoint.</span></span>

    > [!Note]
    > <span data-ttu-id="030f7-182">Dans la configuration par défaut, l’URL redirige la requête vers un écran d’ouverture de session, où les informations d’identification d’un utilisateur de la base de données SAP HANA agréé sont nécessaires pour terminer le processus d’ouverture de session.</span><span class="sxs-lookup"><span data-stu-id="030f7-182">In the default configuration, the URL redirects the request to a logon screen, which requires the credentials of an authenticated SAP HANA database user to complete the logon process.</span></span> <span data-ttu-id="030f7-183">L’utilisateur qui se connecte doit disposer des privilèges requis pour effectuer des tâches d’administration SAML.</span><span class="sxs-lookup"><span data-stu-id="030f7-183">The user who logs on must have the privileges required to perform SAML administration tasks.</span></span>

9. <span data-ttu-id="030f7-184">Dans l’interface web XSA, accédez à **Fournisseur d’identité SAML**, puis cliquez sur le bouton **« + »** en bas de l’écran pour afficher le volet d’ajout des informations sur le fournisseur d’identité et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="030f7-184">In the XSA Web Interface, navigate to **SAML Identity Provider** and from there, click the **“+”** -button on the bottom of the screen to display the Add Identity Provider Info pane and perform the following steps:</span></span>

    ![Ajouter un fournisseur d’identité](./media/active-directory-saas-saphana-tutorial/sap1.png)

    <span data-ttu-id="030f7-186">a.</span><span class="sxs-lookup"><span data-stu-id="030f7-186">a.</span></span> <span data-ttu-id="030f7-187">Dans le volet d’**ajout des informations sur le fournisseur d’identité**, collez le contenu du fichier XML de métadonnées que vous avez téléchargé à partir du portail Azure dans la zone de texte **Métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="030f7-187">In the **Add Identity Provider Info** pane, paste the contents of the Metadata XML, which you have downloaded from Azure portal into the **Metadata** textbox.</span></span>

    ![Paramètres d’ajout d’un fournisseur d’identité](./media/active-directory-saas-saphana-tutorial/sap2.png)

    <span data-ttu-id="030f7-189">b.</span><span class="sxs-lookup"><span data-stu-id="030f7-189">b.</span></span> <span data-ttu-id="030f7-190">Si le contenu du document XML est valide, le processus d’analyse extrait les informations requises pour les insérer dans les champs **Sujet, ID d’entité et Émetteur** de la zone Données générales, et dans les champs URL de la zone Écran de destination, par exemple, **URL de base et URL d’authentification unique (*)**.</span><span class="sxs-lookup"><span data-stu-id="030f7-190">If the contents of the XML document are valid, the parsing process extracts the information required to insert into the **Subject, Entity ID, and Issuer** fields in the General Data screen area, and the URL fields in the Destination screen area, for example, **Base URL and SingleSignOn URL (*)**.</span></span>

    ![Paramètres d’ajout d’un fournisseur d’identité](./media/active-directory-saas-saphana-tutorial/sap3.png)

    <span data-ttu-id="030f7-192">c.</span><span class="sxs-lookup"><span data-stu-id="030f7-192">c.</span></span> <span data-ttu-id="030f7-193">Dans la zone Nom de la zone de l’écran Données générales, entrez un nom pour le nouveau fournisseur d’identité d’authentification unique SAML.</span><span class="sxs-lookup"><span data-stu-id="030f7-193">In the Name box of the General Data screen area, enter a name for the new SAML SSO identity provider.</span></span>

    > [!Note]
    > <span data-ttu-id="030f7-194">Le nom du fournisseur d’identité SAML est obligatoire et doit être unique ; il apparaît dans la liste des fournisseurs d’identité SAML disponibles qui s’affiche, si vous sélectionnez SAML comme méthode d’authentification pour les applications SAP HANA XS à utiliser, par exemple, dans la zone Écran d’authentification de l’outil d’administration d’artefact XS.</span><span class="sxs-lookup"><span data-stu-id="030f7-194">The name of the SAML IDP is mandatory and must be unique; it appears in the list of available SAML IDPs that is displayed, if you select SAML as the authentication method for SAP HANA XS applications to use, for example, in the Authentication screen area of the XS Artifact Administration tool.</span></span>

10. <span data-ttu-id="030f7-195">Enregistrez les détails du nouveau fournisseur d’identité SAML.</span><span class="sxs-lookup"><span data-stu-id="030f7-195">Save the details of the new SAML identity provider.</span></span> <span data-ttu-id="030f7-196">Choisissez **Enregistrer** pour enregistrer les détails du fournisseur d’identité SAML et ajoutez le nouveau fournisseur d’identité SAML à la liste des fournisseurs d’identité SAML connus.</span><span class="sxs-lookup"><span data-stu-id="030f7-196">Choose **Save** to save the details of the SAML identity provider and add the new SAML IDP to the list of known SAML IDPs.</span></span>

    ![Bouton Enregistrer](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. <span data-ttu-id="030f7-198">Dans HANA Studio, dans les propriétés système de l’onglet **Configuration**, filtrez uniquement les paramètres sur **saml** et ajustez **assertion_timeout** de **10 s** à **120 s**.</span><span class="sxs-lookup"><span data-stu-id="030f7-198">In HANA Studio within the system properties of the **Configuration** tab, just filter settings by **saml** and adjust the **assertion_timeout** from **10 sec** to **120 sec**.</span></span>

    ![Paramètre assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="030f7-200">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="030f7-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="030f7-201">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="030f7-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="030f7-202">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="030f7-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="030f7-203">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="030f7-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="030f7-204">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="030f7-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="030f7-206">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="030f7-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="030f7-207">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="030f7-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="030f7-209">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="030f7-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="030f7-211">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="030f7-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="030f7-213">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="030f7-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="030f7-215">a.</span><span class="sxs-lookup"><span data-stu-id="030f7-215">a.</span></span> <span data-ttu-id="030f7-216">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="030f7-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="030f7-217">b.</span><span class="sxs-lookup"><span data-stu-id="030f7-217">b.</span></span> <span data-ttu-id="030f7-218">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="030f7-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="030f7-219">c.</span><span class="sxs-lookup"><span data-stu-id="030f7-219">c.</span></span> <span data-ttu-id="030f7-220">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="030f7-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="030f7-221">d.</span><span class="sxs-lookup"><span data-stu-id="030f7-221">d.</span></span> <span data-ttu-id="030f7-222">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="030f7-222">Click **Create**.</span></span>
 
### <a name="creating-a-sap-hana-test-user"></a><span data-ttu-id="030f7-223">Création d’un utilisateur de test SAP HANA</span><span class="sxs-lookup"><span data-stu-id="030f7-223">Creating a SAP HANA test user</span></span>

<span data-ttu-id="030f7-224">Pour permettre aux utilisateurs Azure AD de se connecter à SAP HANA, vous devez les approvisionner dans SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="030f7-224">To enable Azure AD users to log in to SAP HANA, they must be provisioned into SAP HANA.</span></span>
<span data-ttu-id="030f7-225">SAP HANA prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="030f7-225">SAP HANA supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="030f7-226">Si vous avez besoin de créer un utilisateur manuellement, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="030f7-226">If you need to create a user manually, perform the following steps:</span></span>

>[!Note]
><span data-ttu-id="030f7-227">Vous pouvez modifier l’authentification externe utilisée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="030f7-227">You can change the external authentication used by the user.</span></span>
<span data-ttu-id="030f7-228">Les utilisateurs externes sont authentifiés à l’aide d’un système externe, par exemple un système Kerberos.</span><span class="sxs-lookup"><span data-stu-id="030f7-228">External users are authenticated using an external system, for example a Kerberos system.</span></span> <span data-ttu-id="030f7-229">Pour plus d’informations sur les identités externes, contactez votre [administrateur de domaine](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="030f7-229">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="030f7-230">Ouvrez [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) en tant qu’administrateur et activez l’utilisateur de base de données pour l’authentification unique SAML.</span><span class="sxs-lookup"><span data-stu-id="030f7-230">Open the [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator and enable the DB-User for SAML SSO.</span></span>

    ![créer un utilisateur](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. <span data-ttu-id="030f7-232">Cochez la case invisible à gauche de **SAML** et suivez le lien Configurer.</span><span class="sxs-lookup"><span data-stu-id="030f7-232">Tick the invisible checkbox to the left of **SAML** and follow the Configure link.</span></span>

3. <span data-ttu-id="030f7-233">Cliquez sur **Ajouter** pour ajouter le fournisseur d’identité SAML et cliquez sur **OK** en sélectionnant le fournisseur d’identité SAML approprié.</span><span class="sxs-lookup"><span data-stu-id="030f7-233">Click **Add** to add the SAML IDP and click **OK** selecting the appropriate SAML IDP.</span></span>

4. <span data-ttu-id="030f7-234">Ajoutez l’**identité externe** (par ex.</span><span class="sxs-lookup"><span data-stu-id="030f7-234">Add the **External Identity** (ex.</span></span> <span data-ttu-id="030f7-235">BrittaSimon dans le cas présent) ou choisissez **« Quelconque »** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="030f7-235">BrittaSimon here) or choose **"Any"** and click **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="030f7-236">Si la case « Quelconque » n’est pas cochée, le nom d’utilisateur dans HANA doit correspondre exactement au nom de l’utilisateur dans le nom d’utilisateur principal avant le suffixe de domaine (par exemple, BrittaSimon@contoso.com deviendrait BrittaSimon dans HANA).</span><span class="sxs-lookup"><span data-stu-id="030f7-236">If "ANY" check-box is not checked, then the user name in HANA needs to exactly match the name of the user in the UPN before the domain suffix (i.e. BrittaSimon@contoso.com would become BrittaSimon in HANA).</span></span>

5. <span data-ttu-id="030f7-237">À des fins de test, affectez tous les rôles **« XS »** à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="030f7-237">For testing purposes, assign all **"XS"** roles to the user.</span></span>

    ![attribution de rôles](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="030f7-239">Vous devez donner les autorisations appropriées pour vos cas d’usage, uniquement.</span><span class="sxs-lookup"><span data-stu-id="030f7-239">You should give those permissions appropriate for your use cases, only.</span></span>

6. <span data-ttu-id="030f7-240">Enregistrez l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="030f7-240">Save the user.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="030f7-241">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="030f7-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="030f7-242">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="030f7-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP HANA.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="030f7-244">**Pour affecter Britta Simon à SAP HANA, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="030f7-244">**To assign Britta Simon to SAP HANA, perform the following steps:**</span></span>

1. <span data-ttu-id="030f7-245">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="030f7-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="030f7-247">Dans la liste des applications, sélectionnez **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="030f7-247">In the applications list, select **SAP HANA**.</span></span>

    ![Affecter des utilisateurs](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. <span data-ttu-id="030f7-249">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="030f7-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202] 

4. <span data-ttu-id="030f7-251">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="030f7-251">Click **Add** button.</span></span> <span data-ttu-id="030f7-252">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="030f7-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="030f7-254">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="030f7-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="030f7-255">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="030f7-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="030f7-256">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="030f7-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="030f7-257">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="030f7-257">Testing single sign-on</span></span>

<span data-ttu-id="030f7-258">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="030f7-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="030f7-259">Quand vous cliquez sur la vignette SAP HANA dans le volet d’accès, vous devez être connecté automatiquement à votre application SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="030f7-259">When you click the SAP HANA tile in the Access Panel, you should get automatically signed-on to your SAP HANA application.</span></span>
<span data-ttu-id="030f7-260">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="030f7-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="030f7-261">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="030f7-261">Additional resources</span></span>

* [<span data-ttu-id="030f7-262">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="030f7-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="030f7-263">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="030f7-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



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

