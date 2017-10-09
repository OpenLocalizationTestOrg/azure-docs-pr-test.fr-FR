---
title: "API reporting aaaPrerequisites tooaccess hello Azure AD. | Microsoft Docs"
description: "En savoir plus sur les API reporting de hello conditions préalables tooaccess hello Azure AD"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="c272e-104">API de création de rapports conditions préalables tooaccess hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="c272e-104">Prerequisites tooaccess hello Azure AD reporting API</span></span>
<span data-ttu-id="c272e-105">Hello [AD Azure reporting API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) vous fournir des données de toohello de l’accès par programme via un ensemble d’API REST.</span><span class="sxs-lookup"><span data-stu-id="c272e-105">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="c272e-106">Vous pouvez appeler ces API à partir de divers outils et langages de programmation.</span><span class="sxs-lookup"><span data-stu-id="c272e-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="c272e-107">Hello reporting utilise des API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) API tooauthorize toohello web à l’accès.</span><span class="sxs-lookup"><span data-stu-id="c272e-107">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="c272e-108">tooprepare toohello de votre accès aux API de création de rapports, vous devez :</span><span class="sxs-lookup"><span data-stu-id="c272e-108">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="c272e-109">Créer une application dans votre client Azure AD</span><span class="sxs-lookup"><span data-stu-id="c272e-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="c272e-110">Grant hello application les autorisations appropriées tooaccess hello données Azure AD</span><span class="sxs-lookup"><span data-stu-id="c272e-110">Grant hello application appropriate permissions tooaccess hello Azure AD data</span></span>
3. <span data-ttu-id="c272e-111">Collecter les paramètres de configuration de votre annuaire</span><span class="sxs-lookup"><span data-stu-id="c272e-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="c272e-112">Si vous avez des questions, des problèmes ou des commentaires, veuillez contacter [Aide à la création de rapports AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c272e-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="c272e-113">Créer une application Azure AD</span><span class="sxs-lookup"><span data-stu-id="c272e-113">Create an Azure AD application</span></span>
<span data-ttu-id="c272e-114">tooconfigure votre API directory tooaccess hello AD Azure reporting, vous devez vous connecter toohello portail classique Azure avec un compte d’administrateur d’abonnement Azure est également un membre du rôle d’annuaire hello administrateur général dans votre locataire Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c272e-114">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure classic portal with an Azure subscription administrator account that is also a member of hello Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c272e-115">Applications qui s’exécutent sous les informations d’identification avec des privilèges « admin », comme cela peuvent être très puissantes, donc Veuillez être des informations d’identification de l’application que tookeep hello ID/secret sécurisé.</span><span class="sxs-lookup"><span data-stu-id="c272e-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="c272e-116">Bonjour [portail Azure classic](https://manage.windowsazure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c272e-116">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="c272e-118">À partir de hello **active directory** , sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="c272e-118">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="c272e-119">Dans le menu hello haut de hello, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="c272e-119">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="c272e-121">Dans la barre inférieure de hello, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c272e-121">On hello bottom bar, click **Add**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="c272e-123">Sur hello **comment vous souhaitez toodo ?** boîte de dialogue, cliquez sur **ajouter une application développée par mon organisation**.</span><span class="sxs-lookup"><span data-stu-id="c272e-123">On hello **What do you want toodo?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="c272e-125">Sur hello **Parlez-nous de votre application** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c272e-125">On hello **Tell us about your application** dialog, perform hello following steps:</span></span> 
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="c272e-127">a.</span><span class="sxs-lookup"><span data-stu-id="c272e-127">a.</span></span> <span data-ttu-id="c272e-128">Bonjour **nom** zone de texte, tapez un nom (par exemple : Application de l’API Reporting).</span><span class="sxs-lookup"><span data-stu-id="c272e-128">In hello **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="c272e-129">b.</span><span class="sxs-lookup"><span data-stu-id="c272e-129">b.</span></span> <span data-ttu-id="c272e-130">Sélectionnez **Application Web et/ou API Web**.</span><span class="sxs-lookup"><span data-stu-id="c272e-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="c272e-131">c.</span><span class="sxs-lookup"><span data-stu-id="c272e-131">c.</span></span> <span data-ttu-id="c272e-132">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c272e-132">Click **Next**.</span></span>
7. <span data-ttu-id="c272e-133">Sur hello **propriétés de l’application** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c272e-133">On hello **App properties** dialog, perform hello following steps:</span></span> 
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="c272e-135">a.</span><span class="sxs-lookup"><span data-stu-id="c272e-135">a.</span></span> <span data-ttu-id="c272e-136">Bonjour **URL de connexion** zone de texte, type `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="c272e-136">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="c272e-137">b.</span><span class="sxs-lookup"><span data-stu-id="c272e-137">b.</span></span> <span data-ttu-id="c272e-138">Bonjour **URI ID d’application** zone de texte, type ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="c272e-138">In hello **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="c272e-139">c.</span><span class="sxs-lookup"><span data-stu-id="c272e-139">c.</span></span> <span data-ttu-id="c272e-140">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="c272e-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="c272e-141">Accorder votre hello de toouse autorisation application API</span><span class="sxs-lookup"><span data-stu-id="c272e-141">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="c272e-142">Bonjour [portail Azure classic](https://manage.windowsazure.com/), on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c272e-142">In hello [Azure classic portal](https://manage.windowsazure.com/), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="c272e-144">À partir de hello **active directory** , sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="c272e-144">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="c272e-145">Dans le menu hello haut de hello, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="c272e-145">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="c272e-147">Dans la liste des applications hello, sélectionnez votre application nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="c272e-147">In hello applications list, select your newly created application.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="c272e-149">Dans le menu hello haut de hello, cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="c272e-149">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="c272e-151">Bonjour **autorisations tooother applications** section, pourquoi **Azure Active Directory** ressource, cliquez sur hello **autorisations d’Application** la liste déroulante, puis Sélectionnez **lire les données d’annuaire**.</span><span class="sxs-lookup"><span data-stu-id="c272e-151">In hello **Permissions tooother applications** section, for hello **Azure Active Directory** resource, click hello **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="c272e-153">Dans la barre inférieure de hello, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c272e-153">On hello bottom bar, click **Save**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="c272e-155">Collecter les paramètres de configuration de votre annuaire</span><span class="sxs-lookup"><span data-stu-id="c272e-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="c272e-156">Cette section vous montre comment hello tooget suivant les paramètres de votre annuaire :</span><span class="sxs-lookup"><span data-stu-id="c272e-156">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="c272e-157">Nom de domaine</span><span class="sxs-lookup"><span data-stu-id="c272e-157">Domain name</span></span>
* <span data-ttu-id="c272e-158">ID client</span><span class="sxs-lookup"><span data-stu-id="c272e-158">Client ID</span></span>
* <span data-ttu-id="c272e-159">Clé secrète client</span><span class="sxs-lookup"><span data-stu-id="c272e-159">Client secret</span></span>

<span data-ttu-id="c272e-160">Vous avez besoin de ces valeurs lors de la configuration d’API de création de rapports appelle toohello.</span><span class="sxs-lookup"><span data-stu-id="c272e-160">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="c272e-161">Obtenir votre nom de domaine</span><span class="sxs-lookup"><span data-stu-id="c272e-161">Get your domain name</span></span>
1. <span data-ttu-id="c272e-162">Bonjour [portail Azure classic](https://manage.windowsazure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c272e-162">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="c272e-164">À partir de hello **active directory** , sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="c272e-164">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="c272e-165">Dans le menu hello haut de hello, cliquez sur **domaines**.</span><span class="sxs-lookup"><span data-stu-id="c272e-165">In hello menu on hello top, click **Domains**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="c272e-167">Bonjour **nom de domaine** colonne, copiez votre nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="c272e-167">In hello **Domain Name** column, copy your domain name.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a><span data-ttu-id="c272e-169">Obtenir l’ID de client de l’application hello</span><span class="sxs-lookup"><span data-stu-id="c272e-169">Get hello application's client ID</span></span>
1. <span data-ttu-id="c272e-170">Bonjour [portail Azure classic](https://manage.windowsazure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c272e-170">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="c272e-172">À partir de hello **active directory** , sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="c272e-172">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="c272e-173">Dans le menu hello haut de hello, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="c272e-173">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="c272e-175">Dans la liste des applications hello, sélectionnez votre application nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="c272e-175">In hello applications list, select your newly created application.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="c272e-177">Dans le menu hello haut de hello, cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="c272e-177">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="c272e-179">Copiez votre **ID Client**.</span><span class="sxs-lookup"><span data-stu-id="c272e-179">Copy your **Client ID**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a><span data-ttu-id="c272e-181">Obtenir la clé secrète du client de l’application hello</span><span class="sxs-lookup"><span data-stu-id="c272e-181">Get hello application's client secret</span></span>
<span data-ttu-id="c272e-182">tooget cliente de votre application secrète, vous devez toocreate une nouvelle clé et enregistrer, sa valeur lors de l’enregistrement de clé hello, car il n’est pas possible de tooretrieve cette valeur ultérieurement plus.</span><span class="sxs-lookup"><span data-stu-id="c272e-182">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

1. <span data-ttu-id="c272e-183">Bonjour [portail Azure classic](https://manage.windowsazure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c272e-183">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="c272e-185">À partir de hello **active directory** , sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="c272e-185">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="c272e-186">Dans le menu hello haut de hello, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="c272e-186">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="c272e-188">Dans la liste des applications hello, sélectionnez votre application nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="c272e-188">In hello applications list, select your newly created application.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="c272e-190">Dans le menu hello haut de hello, cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="c272e-190">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="c272e-192">Bonjour **clés** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c272e-192">In hello **Keys** section, perform hello following steps:</span></span> 
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="c272e-194">a.</span><span class="sxs-lookup"><span data-stu-id="c272e-194">a.</span></span> <span data-ttu-id="c272e-195">À partir de la liste de durée hello, sélectionnez une durée</span><span class="sxs-lookup"><span data-stu-id="c272e-195">From hello duration list, select a duration</span></span>
   
    <span data-ttu-id="c272e-196">b.</span><span class="sxs-lookup"><span data-stu-id="c272e-196">b.</span></span> <span data-ttu-id="c272e-197">Dans la barre inférieure de hello, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c272e-197">On hello bottom bar, click **Save**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="c272e-199">c.</span><span class="sxs-lookup"><span data-stu-id="c272e-199">c.</span></span> <span data-ttu-id="c272e-200">Copiez la valeur de clé hello.</span><span class="sxs-lookup"><span data-stu-id="c272e-200">Copy hello key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c272e-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c272e-201">Next Steps</span></span>
* <span data-ttu-id="c272e-202">Serait vous comme tooaccess hello des données à partir d’Azure AD de hello reporting API de manière programmée ?</span><span class="sxs-lookup"><span data-stu-id="c272e-202">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="c272e-203">Extraire [prise en main de hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c272e-203">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="c272e-204">Si vous souhaitez que toofind plus d’informations sur la création de rapports Azure Active Directory, consultez hello [Guide Azure Active Directory Reporting](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c272e-204">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

