---
title: "Didacticiel : Intégration d’Azure Active Directory à Central Desktop | Microsoft Docs"
description: "Découvrez comment toouse Central Desktop avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="d8f32-103">Didacticiel : Intégration d’Azure Active Directory à Central Desktop</span><span class="sxs-lookup"><span data-stu-id="d8f32-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="d8f32-104">objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure et de Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="d8f32-104">hello objective of this tutorial is tooshow hello integration of Azure and Central Desktop.</span></span> <span data-ttu-id="d8f32-105">scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d8f32-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="d8f32-106">Un abonnement Azure valide</span><span class="sxs-lookup"><span data-stu-id="d8f32-106">A valid Azure subscription</span></span>
* <span data-ttu-id="d8f32-107">Un abonnement Central Desktop pour lequel l’authentification unique est activée / locataire Central Desktop</span><span class="sxs-lookup"><span data-stu-id="d8f32-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="d8f32-108">scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="d8f32-108">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="d8f32-109">Activation de l’intégration d’application hello pour Central Desktop</span><span class="sxs-lookup"><span data-stu-id="d8f32-109">Enabling hello application integration for Central Desktop</span></span>
* <span data-ttu-id="d8f32-110">Configuration de l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="d8f32-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="d8f32-111">Configuration de l'approvisionnement des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="d8f32-111">Configuring user provisioning</span></span>
* <span data-ttu-id="d8f32-112">Affectation d’utilisateurs</span><span class="sxs-lookup"><span data-stu-id="d8f32-112">Assigning users</span></span>

<span data-ttu-id="d8f32-113">![Scénario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scénario")</span><span class="sxs-lookup"><span data-stu-id="d8f32-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-central-desktop"></a><span data-ttu-id="d8f32-114">Activer l’intégration d’application hello pour Central Desktop</span><span class="sxs-lookup"><span data-stu-id="d8f32-114">Enable hello application integration for Central Desktop</span></span>
<span data-ttu-id="d8f32-115">objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="d8f32-115">hello objective of this section is toooutline how tooenable hello application integration for Central Desktop.</span></span>

<span data-ttu-id="d8f32-116">**intégration d’application hello tooenable pour Central Desktop, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d8f32-116">**tooenable hello application integration for Central Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8f32-117">Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8f32-117">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="d8f32-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="d8f32-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="d8f32-119">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="d8f32-119">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="d8f32-120">vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="d8f32-120">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="d8f32-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="d8f32-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="d8f32-122">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="d8f32-122">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="d8f32-123">![Ajouter une application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Ajouter une application")</span><span class="sxs-lookup"><span data-stu-id="d8f32-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="d8f32-124">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.</span><span class="sxs-lookup"><span data-stu-id="d8f32-124">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="d8f32-125">![Ajouter une application à partir de la galerie](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Ajouter une application à partir de la galerie")</span><span class="sxs-lookup"><span data-stu-id="d8f32-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="d8f32-126">Bonjour **zone de recherche**, type **Central Desktop**.</span><span class="sxs-lookup"><span data-stu-id="d8f32-126">In hello **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="d8f32-127">![Galerie d’applications](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Galerie d’applications")</span><span class="sxs-lookup"><span data-stu-id="d8f32-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="d8f32-128">Dans le volet de résultats hello, sélectionnez **Central Desktop**, puis cliquez sur **Complete** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d8f32-128">In hello results pane, select **Central Desktop**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="d8f32-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span><span class="sxs-lookup"><span data-stu-id="d8f32-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="d8f32-130">Configurer l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="d8f32-130">Configure single sign-on</span></span>

<span data-ttu-id="d8f32-131">objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooCentral bureau avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.</span><span class="sxs-lookup"><span data-stu-id="d8f32-131">hello objective of this section is toooutline how tooenable users tooauthenticate tooCentral Desktop with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="d8f32-132">Dans le cadre de cette procédure, vous êtes tooupload requis un client de bureau Central tooyour certificat codé en base 64.</span><span class="sxs-lookup"><span data-stu-id="d8f32-132">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour Central Desktop tenant.</span></span>  
<span data-ttu-id="d8f32-133">Si vous n’êtes pas familiarisé avec cette procédure, consultez [comment tooconvert un fichier binaire du certificat dans un fichier texte](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="d8f32-133">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="d8f32-134">**tooconfigure sur l’authentification unique, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d8f32-134">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8f32-135">Bonjour portail Azure classic sur hello **Central Desktop** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello ** configurer Single Sign On ** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d8f32-135">In hello Azure classic portal, on hello **Central Desktop** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="d8f32-136">![Configurer l’authentification unique](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="d8f32-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="d8f32-137">Sur hello **Comment souhaitez-vous toosign les utilisateurs sur le bureau de tooCentral** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d8f32-137">On hello **How would you like users toosign on tooCentral Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="d8f32-138">![Configurer l’authentification unique](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="d8f32-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="d8f32-139">Sur hello **Configure App URL** page, effectuer hello comme suit, puis cliquez sur **suivant**:</span><span class="sxs-lookup"><span data-stu-id="d8f32-139">On hello **Configure App URL** page, perform hello following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="d8f32-140">Bonjour **Central Desktop URL de connexion** zone de texte, tapez l’URL de votre client Central Desktop hello (par exemple : *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="d8f32-140">In hello **Central Desktop Sign In URL** textbox, type hello URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="d8f32-141">Dans la zone de texte URL de réponse Central Desktop hello, tapez votre URL AssertionConsumerService de Central Desktop (par exemple : https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="d8f32-141">In hello Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="d8f32-142">Vous pouvez obtenir la valeur de hello à partir des métadonnées de hello central desktop (par exemple : *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="d8f32-142">You can get hello value from hello central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="d8f32-143">![Configurer l’URL de l’application](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configurer l’URL de l’application")</span><span class="sxs-lookup"><span data-stu-id="d8f32-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="d8f32-144">Sur hello **configurer l’authentification unique sur Central Desktop** page, toodownload votre certificat, cliquez sur **télécharger le certificat**, puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d8f32-144">On hello **Configure single sign-on at Central Desktop** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
  <span data-ttu-id="d8f32-145">![Configurer l’authentification unique](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="d8f32-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="d8f32-146">Connectez-vous à tooyour **Central Desktop** client.</span><span class="sxs-lookup"><span data-stu-id="d8f32-146">Log in tooyour **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="d8f32-147">Accédez trop**paramètres**, cliquez sur **avancé**, puis cliquez sur **Single Sign On**.</span><span class="sxs-lookup"><span data-stu-id="d8f32-147">Go too**Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="d8f32-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span><span class="sxs-lookup"><span data-stu-id="d8f32-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="d8f32-149">Sur hello **Single Sign On Settings** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d8f32-149">On hello **Single Sign On Settings** page, perform hello following steps:</span></span>
   
  <span data-ttu-id="d8f32-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span><span class="sxs-lookup"><span data-stu-id="d8f32-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="d8f32-151">Sélectionnez **Activer l’authentification unique SAMLv2**.</span><span class="sxs-lookup"><span data-stu-id="d8f32-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="d8f32-152">Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Central Desktop** page, hello de copie **URL de l’émetteur** valeur, puis collez-le dans hello **URL SSO** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="d8f32-152">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Issuer URL** value, and then paste it into hello **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="d8f32-153">Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Central Desktop** page, hello de copie **URL de connexion distante** valeur, puis collez-le dans hello **URL de connexion SSO**zone de texte.</span><span class="sxs-lookup"><span data-stu-id="d8f32-153">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Remote Login URL** value, and then paste it into hello **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="d8f32-154">Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Central Desktop** page, hello de copie **URL de Service de déconnexion unique** valeur, puis collez-le dans hello **URL de déconnexion de SSO** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="d8f32-154">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="d8f32-155">Bonjour **méthode de vérification de Signature de Message** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d8f32-155">In hello **Message Signature Verification Method** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="d8f32-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span><span class="sxs-lookup"><span data-stu-id="d8f32-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="d8f32-157">Sélectionnez **Certificate**.</span><span class="sxs-lookup"><span data-stu-id="d8f32-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="d8f32-158">À partir de hello **certificat SSO** liste, sélectionnez **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="d8f32-158">From hello **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="d8f32-159">Créez un fichier texte à partir du certificat hello téléchargé, hello copie le contenu des fichiers de texte hello et le coller ensuite dans hello **certificat SSO** champ.</span><span class="sxs-lookup"><span data-stu-id="d8f32-159">Create a text file from hello downloaded certificate, copy hello content of hello text file, and then paste it into hello **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="d8f32-160">Pour plus d’informations, consultez [comment tooconvert un fichier binaire du certificat dans un fichier texte](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="d8f32-160">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="d8f32-161">Sélectionnez **afficher une page de connexion de lien tooyour SAMLv2**.</span><span class="sxs-lookup"><span data-stu-id="d8f32-161">Select **Display a link tooyour SAMLv2 login page**.</span></span>
9. <span data-ttu-id="d8f32-162">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="d8f32-162">Click **Update**.</span></span>
10. <span data-ttu-id="d8f32-163">Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d8f32-163">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="d8f32-164">![Configurer l’authentification unique](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configurer l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="d8f32-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="d8f32-165">Configurer l'approvisionnement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="d8f32-165">Configure user provisioning</span></span>

<span data-ttu-id="d8f32-166">Pour AAD utilisateurs toobe en mesure de toosign dans, ils doivent être mis en service toohello application Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="d8f32-166">For AAD users toobe able toosign in, they must be provisioned toohello Central Desktop application.</span></span> <span data-ttu-id="d8f32-167">Cette section décrit comment les comptes utilisateur d’AAD toocreate dans Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="d8f32-167">This section describes how toocreate AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="d8f32-168">**tooprovision tooCentral de comptes utilisateur Desktop :**</span><span class="sxs-lookup"><span data-stu-id="d8f32-168">**tooprovision user accounts tooCentral Desktop:**</span></span>
1. <span data-ttu-id="d8f32-169">Ouvrez une session dans tooyour client Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="d8f32-169">Log in tooyour Central Desktop tenant.</span></span>
2. <span data-ttu-id="d8f32-170">Accédez trop**personnes \> membres internes**.</span><span class="sxs-lookup"><span data-stu-id="d8f32-170">Go too**People \> Internal Members**.</span></span>
3. <span data-ttu-id="d8f32-171">Cliquez sur **Ajouter des membres internes**.</span><span class="sxs-lookup"><span data-stu-id="d8f32-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="d8f32-172">![Personnes](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="d8f32-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="d8f32-173">Bonjour **adresse de messagerie des nouveaux membres** zone de texte, tapez un compte AAD, vous souhaitez tooprovision, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d8f32-173">In hello **Email Address of New Members** textbox, type an AAD account you want tooprovision, and then click **Next**.</span></span>
   
  <span data-ttu-id="d8f32-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span><span class="sxs-lookup"><span data-stu-id="d8f32-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="d8f32-175">Cliquez sur **Add Internal member(s)**.</span><span class="sxs-lookup"><span data-stu-id="d8f32-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="d8f32-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span><span class="sxs-lookup"><span data-stu-id="d8f32-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="d8f32-177">les utilisateurs de Hello que vous avez ajouté recevront un message électronique contenant un lien de confirmation dont ils ont besoin de compte de tooclick tooactivate hello.</span><span class="sxs-lookup"><span data-stu-id="d8f32-177">hello users you have added will receive an email that includes a confirmation link they need tooclick tooactivate hello account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="d8f32-178">Vous pouvez utiliser n’importe quel autre Central Desktop utilisateur compte outil de création ou API fournie par Central Desktop tooprovision des comptes d’utilisateur AAD</span><span class="sxs-lookup"><span data-stu-id="d8f32-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop tooprovision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="d8f32-179">Affecter des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="d8f32-179">Assign users</span></span>
<span data-ttu-id="d8f32-180">tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.</span><span class="sxs-lookup"><span data-stu-id="d8f32-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="d8f32-181">**tooassign utilisateurs tooCentral bureau, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d8f32-181">**tooassign users tooCentral Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8f32-182">Bonjour portail Azure classic, créez un compte de test.</span><span class="sxs-lookup"><span data-stu-id="d8f32-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="d8f32-183">Sur hello **Central Desktop** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="d8f32-183">On hello **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="d8f32-184">![Affecter des utilisateurs](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Affecter des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="d8f32-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="d8f32-185">Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.</span><span class="sxs-lookup"><span data-stu-id="d8f32-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="d8f32-186">![Oui](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Oui")</span><span class="sxs-lookup"><span data-stu-id="d8f32-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="d8f32-187">Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="d8f32-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="d8f32-188">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d8f32-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

