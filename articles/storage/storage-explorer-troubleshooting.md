---
title: "guide de dépannage de l’Explorateur de stockage aaaAzure | Documents Microsoft"
description: "Vue d’ensemble de la fonctionnalité de débogage hello deux de Azure"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: delhan
ms.openlocfilehash: 21705629500359222bc566c599f0864ad50036ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="8e674-103">Guide de résolution des problèmes de l’Explorateur de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8e674-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="8e674-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="8e674-104">Introduction</span></span>

<span data-ttu-id="8e674-105">Explorateur de stockage Microsoft Azure (aperçu) est une application autonome qui vous permet de travail tooeasily avec des données de stockage Azure sur Windows, Mac OS et Linux.</span><span class="sxs-lookup"><span data-stu-id="8e674-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="8e674-106">application Hello peut se connecter comptes toStorage hébergées sur Azure, les Clouds souverains et pile d’Azure.</span><span class="sxs-lookup"><span data-stu-id="8e674-106">hello app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="8e674-107">Ce guide résume les solutions aux problèmes couramment rencontrés dans l’Explorateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="8e674-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="8e674-108">Problèmes de connexion</span><span class="sxs-lookup"><span data-stu-id="8e674-108">Sign in issues</span></span>

<span data-ttu-id="8e674-109">Seuls les comptes Azure Active Directory (AAD) sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="8e674-109">Only Azure Active Directory (AAD) accounts are supported.</span></span> <span data-ttu-id="8e674-110">Si vous utilisez un compte AD FS, il est attendu que l’ouverture de session tooStorage Qu'explorer ne fonctionnera pas.</span><span class="sxs-lookup"><span data-stu-id="8e674-110">If you use an ADFS account, it’s expected that signing in tooStorage Explorer would not work.</span></span> <span data-ttu-id="8e674-111">Avant de continuer, essayez de redémarrer votre application et voir si des problèmes de hello peuvent être résolus.</span><span class="sxs-lookup"><span data-stu-id="8e674-111">Before you continue, try restarting your application and see whether hello problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="8e674-112">Erreur : certificat auto-signé dans la chaîne d’approbation</span><span class="sxs-lookup"><span data-stu-id="8e674-112">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="8e674-113">Il existe plusieurs raisons pour lesquelles vous pouvez rencontrer cette erreur et hello deux causes principales sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="8e674-113">There are several reasons why you may encounter this error, and hello most common two reasons are as follows:</span></span>

1. <span data-ttu-id="8e674-114">application Hello est connectée via un « proxy transparent », ce qui signifie un serveur (par exemple, le serveur de votre entreprise) est intercepte le trafic HTTPS, déchiffrage et chiffrer à l’aide d’un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="8e674-114">hello app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="8e674-115">Vous exécutez une application, telles que les antivirus qui injecte un certificat SSL auto-signé dans les messages hello HTTPS que vous recevez.</span><span class="sxs-lookup"><span data-stu-id="8e674-115">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into hello HTTPS messages that you receive.</span></span>

<span data-ttu-id="8e674-116">Lorsque l’Explorateur de stockage rencontre un des problèmes de hello, il peut ne plus savoir si le message de salutation reçu HTTPS a été modifié.</span><span class="sxs-lookup"><span data-stu-id="8e674-116">When Storage Explorer encounters one of hello issues, it can no longer know whether hello received HTTPS message is tampered.</span></span> <span data-ttu-id="8e674-117">Si vous avez une copie du certificat auto-signé de hello, vous pouvez laisser l’Explorateur de stockage de confiance.</span><span class="sxs-lookup"><span data-stu-id="8e674-117">If you have a copy of hello self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="8e674-118">Si vous ne savez pas qui injecte les certificats hello, suivez ces étapes toofind il :</span><span class="sxs-lookup"><span data-stu-id="8e674-118">If you are unsure of who is injecting hello certificate, follow these steps toofind it:</span></span>

1. <span data-ttu-id="8e674-119">Installez Open SSL.</span><span class="sxs-lookup"><span data-stu-id="8e674-119">Install Open SSL</span></span>

    - <span data-ttu-id="8e674-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (une des versions de lumière hello doit être suffisamment)</span><span class="sxs-lookup"><span data-stu-id="8e674-120">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of hello light versions should be sufficient)</span></span>

    - <span data-ttu-id="8e674-121">Mac et Linux : doit être inclus dans votre système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="8e674-121">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="8e674-122">Exécutez Open SSL.</span><span class="sxs-lookup"><span data-stu-id="8e674-122">Run Open SSL</span></span>

    - <span data-ttu-id="8e674-123">Windows : ouvrez le répertoire d’installation Bonjour, cliquez sur **/bin/**, puis double-cliquez sur **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="8e674-123">Windows: open hello installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="8e674-124">Mac et Linux : exécutez **openssl** à partir d’un terminal.</span><span class="sxs-lookup"><span data-stu-id="8e674-124">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="8e674-125">Exécutez s_client -showcerts -connect microsoft.com:443.</span><span class="sxs-lookup"><span data-stu-id="8e674-125">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="8e674-126">Recherchez les certificats auto-signés.</span><span class="sxs-lookup"><span data-stu-id="8e674-126">Look for self-signed certificates.</span></span> <span data-ttu-id="8e674-127">Si vous ne savez pas laquelle sont auto-signés, rechercher n’importe où dans l’objet hello (« %s ») et l’émetteur (« i ») sont hello identiques.</span><span class="sxs-lookup"><span data-stu-id="8e674-127">If you are unsure which are self-signed, look for anywhere hello subject ("s:") and issuer ("i:") are hello same.</span></span>

5. <span data-ttu-id="8e674-128">Lorsque vous avez trouvé les certificats auto-signés, pour chacune d’elles, copier- coller tous les éléments à **---BEGIN CERTIFICATE---** trop**---END CERTIFICATE---** tooa fichier .cer.</span><span class="sxs-lookup"><span data-stu-id="8e674-128">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** tooa new .cer file.</span></span>

6. <span data-ttu-id="8e674-129">Ouvrez l’Explorateur de stockage, cliquez sur **modifier** > **certificats SSL** > **les certificats d’importation**et puis utilisez hello fichier sélecteur toofind, sélectionnez, et ouvrez les fichiers .cer hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="8e674-129">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use hello file picker toofind, select, and open hello .cer files that you created.</span></span>

<span data-ttu-id="8e674-130">Si vous ne trouvez pas les certificats auto-signés à l’aide de hello étapes ci-dessus, nous contacter via l’outil commentaires hello pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="8e674-130">If you cannot find any self-signed certificates using hello above steps, contact us through hello feedback tool for more help.</span></span>

### <a name="unable-tooretrieve-subscriptions"></a><span data-ttu-id="8e674-131">Impossible de tooretrieve abonnements</span><span class="sxs-lookup"><span data-stu-id="8e674-131">Unable tooretrieve subscriptions</span></span>

<span data-ttu-id="8e674-132">Si vous êtes tooretrieve Impossible de vos abonnements après avoir se connecter avec succès, suivez ces étapes tootroubleshoot ce problème :</span><span class="sxs-lookup"><span data-stu-id="8e674-132">If you are unable tooretrieve your subscriptions after you successfully sign in, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="8e674-133">Vérifiez que votre compte a accès toohello abonnements en vous connectant à hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8e674-133">Verify that your account has access toohello subscriptions by signing into hello Azure portal.</span></span>

- <span data-ttu-id="8e674-134">Assurez-vous que vous êtes connecté à l’aide d’environnement approprié de hello (Azure, Azure Chine, Azure en Allemagne, Azure du gouvernement ou pile d’environnement/Azure personnalisée).</span><span class="sxs-lookup"><span data-stu-id="8e674-134">Make sure that you have signed in using hello correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="8e674-135">Si vous êtes derrière un proxy, assurez-vous que vous avez configuré un proxy de l’Explorateur de stockage hello correctement.</span><span class="sxs-lookup"><span data-stu-id="8e674-135">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="8e674-136">Essayez de supprimer et readding compte de hello.</span><span class="sxs-lookup"><span data-stu-id="8e674-136">Try removing and readding hello account.</span></span>

- <span data-ttu-id="8e674-137">Essayez de supprimer les hello fichiers suivants à partir de votre répertoire racine (autrement dit, C:\Users\ContosoUser), puis rajoutez les compte hello :</span><span class="sxs-lookup"><span data-stu-id="8e674-137">Try deleting hello following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding hello account:</span></span>

    - <span data-ttu-id="8e674-138">.adalcache</span><span class="sxs-lookup"><span data-stu-id="8e674-138">.adalcache</span></span>

    - <span data-ttu-id="8e674-139">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="8e674-139">.devaccounts</span></span>

    - <span data-ttu-id="8e674-140">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="8e674-140">.extaccounts</span></span>

- <span data-ttu-id="8e674-141">Console des outils de développement espion hello (en appuyant sur F12) lorsque vous vous connectez des messages d’erreur :</span><span class="sxs-lookup"><span data-stu-id="8e674-141">Watch hello developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![Outils de développement](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a><span data-ttu-id="8e674-143">Page d’authentification hello toosee Impossible</span><span class="sxs-lookup"><span data-stu-id="8e674-143">Unable toosee hello authentication page</span></span>

<span data-ttu-id="8e674-144">Si vous êtes page d’authentification impossible toosee hello, procédez comme tootroubleshoot de ces étapes de ce problème :</span><span class="sxs-lookup"><span data-stu-id="8e674-144">If you are unable toosee hello authentication page, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="8e674-145">Selon la vitesse de votre connexion de hello, elle peut prendre un certain temps pour tooload de page de connexion hello, attendez au moins une minute avant de fermer la boîte de dialogue d’authentification hello.</span><span class="sxs-lookup"><span data-stu-id="8e674-145">Depending on hello speed of your connection, it may take a while for hello sign-in page tooload, wait at least one minute before closing hello authentication dialog box.</span></span>

- <span data-ttu-id="8e674-146">Si vous êtes derrière un proxy, assurez-vous que vous avez configuré un proxy de l’Explorateur de stockage hello correctement.</span><span class="sxs-lookup"><span data-stu-id="8e674-146">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="8e674-147">Afficher la console du développeur hello en appuyant sur la touche F12 de hello.</span><span class="sxs-lookup"><span data-stu-id="8e674-147">View hello developer console by pressing hello F12 key.</span></span> <span data-ttu-id="8e674-148">Regardez des réponses hello à partir de la console de développement hello et observez si vous pouvez rechercher un indice pour la raison pour laquelle l’authentification ne fonctionne ne pas.</span><span class="sxs-lookup"><span data-stu-id="8e674-148">Watch hello responses from hello developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="8e674-149">Impossible de supprimer un compte</span><span class="sxs-lookup"><span data-stu-id="8e674-149">Cannot remove account</span></span>

<span data-ttu-id="8e674-150">Si vous n’êtes pas tooremove un compte ou si hello authentifier de nouveau lien ne fait rien, suivez ces étapes tootroubleshoot ce problème :</span><span class="sxs-lookup"><span data-stu-id="8e674-150">If you are unable tooremove an account, or if hello reauthenticate link does not do anything, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="8e674-151">Essayez de supprimer les hello fichiers suivants à partir de votre répertoire racine et puis readding compte de hello :</span><span class="sxs-lookup"><span data-stu-id="8e674-151">Try deleting hello following files from your root directory, and then readding hello account:</span></span>

    - <span data-ttu-id="8e674-152">.adalcache</span><span class="sxs-lookup"><span data-stu-id="8e674-152">.adalcache</span></span>

    - <span data-ttu-id="8e674-153">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="8e674-153">.devaccounts</span></span>

    - <span data-ttu-id="8e674-154">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="8e674-154">.extaccounts</span></span>

- <span data-ttu-id="8e674-155">Si vous souhaitez tooremove SAS attaché à des ressources de stockage, supprimez hello fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="8e674-155">If you want tooremove SAS attached Storage resources, delete hello following files:</span></span>

    - <span data-ttu-id="8e674-156">Dossier %AppData%/StorageExplorer pour Windows</span><span class="sxs-lookup"><span data-stu-id="8e674-156">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="8e674-157">/Users/<votre_nom>/Library/Application Support/StorageExplorer pour Mac</span><span class="sxs-lookup"><span data-stu-id="8e674-157">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="8e674-158">~/.config/StorageExplorer pour Linux</span><span class="sxs-lookup"><span data-stu-id="8e674-158">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="8e674-159">Vous devez tooreenter vos informations d’identification si vous supprimez ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="8e674-159">You will have tooreenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="8e674-160">Problèmes de proxy</span><span class="sxs-lookup"><span data-stu-id="8e674-160">Proxy issues</span></span>

<span data-ttu-id="8e674-161">Tout d’abord, assurez-vous que vous avez entré des informations suivantes de hello sont tous corrects :</span><span class="sxs-lookup"><span data-stu-id="8e674-161">First, make sure that hello following information you entered are all correct:</span></span>

- <span data-ttu-id="8e674-162">Hello URL de proxy et le port numéro</span><span class="sxs-lookup"><span data-stu-id="8e674-162">hello proxy URL and port number</span></span>

- <span data-ttu-id="8e674-163">Nom d’utilisateur et mot de passe si nécessaire par proxy de hello</span><span class="sxs-lookup"><span data-stu-id="8e674-163">Username and password if required by hello proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="8e674-164">Solutions courantes</span><span class="sxs-lookup"><span data-stu-id="8e674-164">Common solutions</span></span>

<span data-ttu-id="8e674-165">Si vous rencontrez encore des problèmes, suivez ces étapes tootroubleshoot les :</span><span class="sxs-lookup"><span data-stu-id="8e674-165">If you are still experiencing issues, follow these steps tootroubleshoot them:</span></span>

- <span data-ttu-id="8e674-166">Si vous pouvez vous connecter à toohello Internet sans utiliser de votre proxy, vérifiez que l’Explorateur de stockage fonctionne sans paramètres de proxy activées.</span><span class="sxs-lookup"><span data-stu-id="8e674-166">If you can connect toohello Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="8e674-167">Si c’est le cas de hello, il peut être un problème avec vos paramètres de proxy.</span><span class="sxs-lookup"><span data-stu-id="8e674-167">If this is hello case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="8e674-168">Travailler avec vos problèmes de proxy administrateur tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="8e674-168">Work with your proxy administrator tooidentify hello problems.</span></span>

- <span data-ttu-id="8e674-169">Vérifiez que les autres applications à l’aide du serveur de proxy hello fonctionnent comme prévu.</span><span class="sxs-lookup"><span data-stu-id="8e674-169">Verify that other applications using hello proxy server work as expected.</span></span>

- <span data-ttu-id="8e674-170">Vérifiez que vous pouvez vous connecter à l’aide de votre navigateur web du portail Microsoft Azure toohello</span><span class="sxs-lookup"><span data-stu-id="8e674-170">Verify that you can connect toohello Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="8e674-171">Vérifiez que vous pouvez recevoir des réponses de vos points de terminaison de service.</span><span class="sxs-lookup"><span data-stu-id="8e674-171">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="8e674-172">Entrez une des URL de point de terminaison dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="8e674-172">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="8e674-173">Si vous pouvez vous connecter, vous devez recevoir une réponse XML InvalidQueryParameterValue ou similaire.</span><span class="sxs-lookup"><span data-stu-id="8e674-173">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="8e674-174">Si quelqu’un d’autre utilise également l’Explorateur de stockage avec votre serveur proxy, vérifiez que cette personne peut se connecter.</span><span class="sxs-lookup"><span data-stu-id="8e674-174">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="8e674-175">Si elles peuvent se connecter, vous avez peut-être toocontact votre administrateur du serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="8e674-175">If they can connect, you may have toocontact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="8e674-176">Outils pour diagnostiquer les problèmes</span><span class="sxs-lookup"><span data-stu-id="8e674-176">Tools for diagnosing issues</span></span>

<span data-ttu-id="8e674-177">Si vous disposez des outils de mise en réseau, tel que Fiddler pour Windows, vous pouvez être en mesure de toodiagnose des problèmes hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="8e674-177">If you have networking tools, such as Fiddler for Windows, you may be able toodiagnose hello problems as follows:</span></span>

- <span data-ttu-id="8e674-178">Si vous avez toowork via votre proxy, vous avez peut-être tooconfigure votre tooconnect outil réseau via le proxy hello.</span><span class="sxs-lookup"><span data-stu-id="8e674-178">If you have toowork through your proxy, you may have tooconfigure your networking tool tooconnect through hello proxy.</span></span>

- <span data-ttu-id="8e674-179">Vérifiez le numéro de port de hello utilisé par votre outil de mise en réseau.</span><span class="sxs-lookup"><span data-stu-id="8e674-179">Check hello port number used by your networking tool.</span></span>

- <span data-ttu-id="8e674-180">Entrez l’URL de l’hôte local hello et hello numéro de port de l’outil de mise en réseau en tant que paramètres de proxy dans l’Explorateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="8e674-180">Enter hello local host URL and hello networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="8e674-181">Si cette opération est effectuée correctement, l’outil de mise en réseau démarre la journalisation de demandes réseau apportées par les points de terminaison toomanagement et le service de l’Explorateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="8e674-181">If this is done correctly, your networking tool starts logging network requests made by Storage Explorer toomanagement and service endpoints.</span></span> <span data-ttu-id="8e674-182">Par exemple, entrez https://cawablobgrs.blob.core.windows.net/ pour votre point de terminaison d’objet blob dans un navigateur, et vous recevez une réponse similaire hello suivant, ce qui suggère hello ressource existe, bien que vous ne pouvez pas y accéder.</span><span class="sxs-lookup"><span data-stu-id="8e674-182">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles hello following, which suggests hello resource exists, although you cannot access it.</span></span>

![Exemple de code](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="8e674-184">Contacter l’administrateur du serveur proxy</span><span class="sxs-lookup"><span data-stu-id="8e674-184">Contact proxy server admin</span></span>

<span data-ttu-id="8e674-185">Si vos paramètres de proxy sont correctes, vous avez peut-être toocontact votre administrateur de serveur proxy, et</span><span class="sxs-lookup"><span data-stu-id="8e674-185">If your proxy settings are correct, you may have toocontact your proxy server admin, and</span></span>

- <span data-ttu-id="8e674-186">Assurez-vous que votre proxy ne bloque pas le trafic tooAzure gestion ou ressource de points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="8e674-186">Make sure that your proxy does not block traffic tooAzure management or resource endpoints.</span></span>

- <span data-ttu-id="8e674-187">Vérifiez que le protocole d’authentification hello utilisé par votre serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="8e674-187">Verify hello authentication protocol used by your proxy server.</span></span> <span data-ttu-id="8e674-188">L’Explorateur de stockage ne prend pas en charge les proxys NTLM.</span><span class="sxs-lookup"><span data-stu-id="8e674-188">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-tooretrieve-children-error-message"></a><span data-ttu-id="8e674-189">Message d’erreur « Impossible de tooRetrieve enfants »</span><span class="sxs-lookup"><span data-stu-id="8e674-189">"Unable tooRetrieve Children" error message</span></span>

<span data-ttu-id="8e674-190">Si vous êtes connecté tooAzure via un proxy, vérifiez que vos paramètres de proxy sont corrects.</span><span class="sxs-lookup"><span data-stu-id="8e674-190">If you are connected tooAzure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="8e674-191">Si vous ont été accordé l’accès tooa ressource propriétaire hello de hello abonnement ou le compte, vérifiez que vous avez lu ou répertorier les autorisations pour cette ressource.</span><span class="sxs-lookup"><span data-stu-id="8e674-191">If you were granted access tooa resource from hello owner of hello subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="8e674-192">Problèmes liés à l’URL SAP</span><span class="sxs-lookup"><span data-stu-id="8e674-192">Issues with SAS URL</span></span>
<span data-ttu-id="8e674-193">Si vous vous connectez tooa service à l’aide d’une URL SAS et rencontre cette erreur :</span><span class="sxs-lookup"><span data-stu-id="8e674-193">If you are connecting tooa service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="8e674-194">Vérifiez que les URL hello fournit les autorisations nécessaires hello tooread ou une liste de ressources.</span><span class="sxs-lookup"><span data-stu-id="8e674-194">Verify that hello URL provides hello necessary permissions tooread or list resources.</span></span>

- <span data-ttu-id="8e674-195">Vérifiez que hello QU'URL n’a pas expiré.</span><span class="sxs-lookup"><span data-stu-id="8e674-195">Verify that hello URL has not expired.</span></span>

- <span data-ttu-id="8e674-196">Si hello URL SAS est basé sur une stratégie d’accès, vérifiez que la stratégie d’accès hello n’a pas été révoquée.</span><span class="sxs-lookup"><span data-stu-id="8e674-196">If hello SAS URL is based on an access policy, verify that hello access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e674-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8e674-197">Next steps</span></span>

<span data-ttu-id="8e674-198">Si aucune des solutions de hello vous convient, de soumettre votre problème via l’outil commentaires hello avec votre adresse de messagerie et autant de détails sur le problème hello inclus en tant que vous pouvez, afin que nous pouvons vous contacter pour résoudre le problème de hello.</span><span class="sxs-lookup"><span data-stu-id="8e674-198">If none of hello solutions work for you, submit your issue through hello feedback tool with your email and as many details about hello issue included as you can, so that we can contact you for fixing hello issue.</span></span>

<span data-ttu-id="8e674-199">toodo, cliquez sur **aide** menu, puis sur **envoyer des commentaires**.</span><span class="sxs-lookup"><span data-stu-id="8e674-199">toodo this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Commentaires](./media/storage-explorer-troubleshooting/4022503_en_1.png)
