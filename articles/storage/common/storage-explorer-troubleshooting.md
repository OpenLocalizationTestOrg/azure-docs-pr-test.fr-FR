---
title: "Guide de résolution des problèmes de l’Explorateur de stockage Azure | Microsoft Docs"
description: "Vue d’ensemble des deux fonctionnalités de débogage d’Azure"
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
ms.date: 05/18/2017
ms.author: delhan
ms.openlocfilehash: 470b2d87ffdc4769bb2963df7dea646901469e00
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="100f4-103">Guide de résolution des problèmes de l’Explorateur de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="100f4-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="100f4-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="100f4-104">Introduction</span></span>

<span data-ttu-id="100f4-105">L’Explorateur de stockage Microsoft Azure (préversion) est une application autonome qui vous permet d’utiliser facilement les données Stockage Azure sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="100f4-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="100f4-106">L’application peut se connecter aux comptes de stockage hébergés sur Azure, les clouds souverains et Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="100f4-106">The app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="100f4-107">Ce guide résume les solutions aux problèmes couramment rencontrés dans l’Explorateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="100f4-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="100f4-108">Problèmes de connexion</span><span class="sxs-lookup"><span data-stu-id="100f4-108">Sign in issues</span></span>

<span data-ttu-id="100f4-109">Avant de continuer, essayez de redémarrer votre application et de voir si les problèmes peuvent être résolus.</span><span class="sxs-lookup"><span data-stu-id="100f4-109">Before you continue, try restarting your application and see whether the problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="100f4-110">Erreur : certificat auto-signé dans la chaîne d’approbation</span><span class="sxs-lookup"><span data-stu-id="100f4-110">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="100f4-111">Parmi les raisons pouvant expliquer cette erreur, voici les deux plus courantes :</span><span class="sxs-lookup"><span data-stu-id="100f4-111">There are several reasons why you may encounter this error, and the most common two reasons are as follows:</span></span>

1. <span data-ttu-id="100f4-112">L’application est connectée via un « proxy transparent » ; dans cette configuration, un serveur (par exemple, le serveur de votre société) intercepte le trafic HTTPS, le déchiffre, puis le chiffre à l’aide d’un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="100f4-112">The app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="100f4-113">Vous exécutez une application, telle qu’un logiciel antivirus, qui injecte un certificat SSL auto-signé dans les messages HTTPS que vous recevez.</span><span class="sxs-lookup"><span data-stu-id="100f4-113">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into the HTTPS messages that you receive.</span></span>

<span data-ttu-id="100f4-114">Quand l’Explorateur de stockage rencontre l’un de ces problèmes, il ne peut plus savoir si le message HTTPS reçu a été falsifié.</span><span class="sxs-lookup"><span data-stu-id="100f4-114">When Storage Explorer encounters one of the issues, it can no longer know whether the received HTTPS message is tampered.</span></span> <span data-ttu-id="100f4-115">Si vous avez une copie du certificat auto-signé, vous pouvez laisser l’Explorateur de stockage lui faire confiance.</span><span class="sxs-lookup"><span data-stu-id="100f4-115">If you have a copy of the self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="100f4-116">Si vous ne savez pas qui injecte le certificat, suivez ces étapes pour le déterminer :</span><span class="sxs-lookup"><span data-stu-id="100f4-116">If you are unsure of who is injecting the certificate, follow these steps to find it:</span></span>

1. <span data-ttu-id="100f4-117">Installez Open SSL.</span><span class="sxs-lookup"><span data-stu-id="100f4-117">Install Open SSL</span></span>

    - <span data-ttu-id="100f4-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (n’importe quelle version légère devrait suffire)</span><span class="sxs-lookup"><span data-stu-id="100f4-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of the light versions should be sufficient)</span></span>

    - <span data-ttu-id="100f4-119">Mac et Linux : doit être inclus dans votre système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="100f4-119">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="100f4-120">Exécutez Open SSL.</span><span class="sxs-lookup"><span data-stu-id="100f4-120">Run Open SSL</span></span>

    - <span data-ttu-id="100f4-121">Windows : ouvrez le répertoire d’installation, cliquez sur **/bin/**, puis double-cliquez sur **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="100f4-121">Windows: open the installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="100f4-122">Mac et Linux : exécutez **openssl** à partir d’un terminal.</span><span class="sxs-lookup"><span data-stu-id="100f4-122">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="100f4-123">Exécutez s_client -showcerts -connect microsoft.com:443.</span><span class="sxs-lookup"><span data-stu-id="100f4-123">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="100f4-124">Recherchez les certificats auto-signés.</span><span class="sxs-lookup"><span data-stu-id="100f4-124">Look for self-signed certificates.</span></span> <span data-ttu-id="100f4-125">Ce sont ceux dont le sujet (« s: ») et l’émetteur (« i: ») sont identiques.</span><span class="sxs-lookup"><span data-stu-id="100f4-125">If you are unsure which are self-signed, look for anywhere the subject ("s:") and issuer ("i:") are the same.</span></span>

5. <span data-ttu-id="100f4-126">Après avoir trouvé les certificats auto-signés pour chacun d’eux, copiez et collez tout depuis **---BEGIN CERTIFICATE---** jusqu’à **---END CERTIFICATE---** (les deux inclus) dans un nouveau fichier .cer.</span><span class="sxs-lookup"><span data-stu-id="100f4-126">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** to a new .cer file.</span></span>

6. <span data-ttu-id="100f4-127">Ouvrez l’Explorateur de stockage, cliquez sur **Modifier** > **Certificats SSL** > **Importer les certificats**, puis utilisez le sélecteur de fichiers pour rechercher, sélectionner et ouvrir les fichiers .cer que vous avez créés.</span><span class="sxs-lookup"><span data-stu-id="100f4-127">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use the file picker to find, select, and open the .cer files that you created.</span></span>

<span data-ttu-id="100f4-128">Si vous ne trouvez aucun certificat auto-signé à l’aide de la procédure ci-dessus, contactez-nous au moyen de l’outil de commentaires pour obtenir de l’aide.</span><span class="sxs-lookup"><span data-stu-id="100f4-128">If you cannot find any self-signed certificates using the above steps, contact us through the feedback tool for more help.</span></span>

### <a name="unable-to-retrieve-subscriptions"></a><span data-ttu-id="100f4-129">Impossible de récupérer les abonnements</span><span class="sxs-lookup"><span data-stu-id="100f4-129">Unable to retrieve subscriptions</span></span>

<span data-ttu-id="100f4-130">Si vous ne parvenez pas à récupérer vos abonnements après vous être connecté avec succès, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="100f4-130">If you are unable to retrieve your subscriptions after you successfully sign in, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="100f4-131">Vérifiez que votre compte a accès aux abonnements en vous connectant au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="100f4-131">Verify that your account has access to the subscriptions by signing into the Azure Portal.</span></span>

- <span data-ttu-id="100f4-132">Assurez-vous que vous vous êtes connecté à l’aide de l’environnement approprié (Azure, Azure - Chine, Azure - Allemagne, Azure - Gouvernement des États-Unis ou Environnement personnalisé/Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="100f4-132">Make sure that you have signed in using the correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="100f4-133">Si vous vous trouvez derrière un proxy, vérifiez que vous avez correctement configuré le proxy de l’Explorateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="100f4-133">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="100f4-134">Essayez de supprimer et de rajouter le compte.</span><span class="sxs-lookup"><span data-stu-id="100f4-134">Try removing and readding the account.</span></span>

- <span data-ttu-id="100f4-135">Essayez de supprimer les fichiers suivants de votre répertoire racine (autrement dit, C:\Users\ContosoUser), puis de rajouter le compte :</span><span class="sxs-lookup"><span data-stu-id="100f4-135">Try deleting the following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding the account:</span></span>

    - <span data-ttu-id="100f4-136">.adalcache</span><span class="sxs-lookup"><span data-stu-id="100f4-136">.adalcache</span></span>

    - <span data-ttu-id="100f4-137">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="100f4-137">.devaccounts</span></span>

    - <span data-ttu-id="100f4-138">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="100f4-138">.extaccounts</span></span>

- <span data-ttu-id="100f4-139">Quand vous vous connectez, vérifiez si la console des outils de développement indique des messages d’erreur (en appuyant sur F12) :</span><span class="sxs-lookup"><span data-stu-id="100f4-139">Watch the developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![Outils de développement](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-to-see-the-authentication-page"></a><span data-ttu-id="100f4-141">Impossible de voir la page d’authentification</span><span class="sxs-lookup"><span data-stu-id="100f4-141">Unable to see the authentication page</span></span>

<span data-ttu-id="100f4-142">Si vous ne pouvez pas voir la page d’authentification, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="100f4-142">If you are unable to see the authentication page, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="100f4-143">Selon la vitesse de votre connexion, le chargement de la page de connexion peut prendre un certain temps ; attendez au moins une minute avant de fermer la boîte de dialogue d’authentification.</span><span class="sxs-lookup"><span data-stu-id="100f4-143">Depending on the speed of your connection, it may take a while for the sign-in page to load, wait at least one minute before closing the authentication dialog box.</span></span>

- <span data-ttu-id="100f4-144">Si vous vous trouvez derrière un proxy, vérifiez que vous avez correctement configuré le proxy de l’Explorateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="100f4-144">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="100f4-145">Affichez la console de développement en appuyant sur la touche F12.</span><span class="sxs-lookup"><span data-stu-id="100f4-145">View the developer console by pressing the F12 key.</span></span> <span data-ttu-id="100f4-146">Dans les réponses indiquées par la console de développement, recherchez des indices éventuels sur le dysfonctionnement de l’authentification.</span><span class="sxs-lookup"><span data-stu-id="100f4-146">Watch the responses from the developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="100f4-147">Impossible de supprimer un compte</span><span class="sxs-lookup"><span data-stu-id="100f4-147">Cannot remove account</span></span>

<span data-ttu-id="100f4-148">Si vous ne pouvez pas supprimer un compte, ou que le lien de réauthentification est inopérant, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="100f4-148">If you are unable to remove an account, or if the reauthenticate link does not do anything, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="100f4-149">Essayez de supprimer les fichiers suivants de votre répertoire racine, puis de rajouter le compte :</span><span class="sxs-lookup"><span data-stu-id="100f4-149">Try deleting the following files from your root directory, and then readding the account:</span></span>

    - <span data-ttu-id="100f4-150">.adalcache</span><span class="sxs-lookup"><span data-stu-id="100f4-150">.adalcache</span></span>

    - <span data-ttu-id="100f4-151">.devaccounts</span><span class="sxs-lookup"><span data-stu-id="100f4-151">.devaccounts</span></span>

    - <span data-ttu-id="100f4-152">.extaccounts</span><span class="sxs-lookup"><span data-stu-id="100f4-152">.extaccounts</span></span>

- <span data-ttu-id="100f4-153">Si vous souhaitez supprimer des ressources de stockage jointes SAP, supprimez les fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="100f4-153">If you want to remove SAS attached Storage resources, delete the following files:</span></span>

    - <span data-ttu-id="100f4-154">Dossier %AppData%/StorageExplorer pour Windows</span><span class="sxs-lookup"><span data-stu-id="100f4-154">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="100f4-155">/Users/<votre_nom>/Library/Application Support/StorageExplorer pour Mac</span><span class="sxs-lookup"><span data-stu-id="100f4-155">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="100f4-156">~/.config/StorageExplorer pour Linux</span><span class="sxs-lookup"><span data-stu-id="100f4-156">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="100f4-157">Vous devez entrer à nouveau toutes vos informations d’identification si vous supprimez ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="100f4-157">You will have to reenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="100f4-158">Problèmes de proxy</span><span class="sxs-lookup"><span data-stu-id="100f4-158">Proxy issues</span></span>

<span data-ttu-id="100f4-159">Tout d’abord, vérifiez que les informations suivantes que vous avez entrées sont toutes correctes :</span><span class="sxs-lookup"><span data-stu-id="100f4-159">First, make sure that the following information you entered are all correct:</span></span>

- <span data-ttu-id="100f4-160">URL de proxy et numéro de port</span><span class="sxs-lookup"><span data-stu-id="100f4-160">The proxy URL and port number</span></span>

- <span data-ttu-id="100f4-161">Nom d’utilisateur et mot de passe si requis par le proxy</span><span class="sxs-lookup"><span data-stu-id="100f4-161">Username and password if required by the proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="100f4-162">Solutions courantes</span><span class="sxs-lookup"><span data-stu-id="100f4-162">Common solutions</span></span>

<span data-ttu-id="100f4-163">Si vous rencontrez toujours des problèmes, suivez ces étapes :</span><span class="sxs-lookup"><span data-stu-id="100f4-163">If you are still experiencing issues, follow these steps to troubleshoot them:</span></span>

- <span data-ttu-id="100f4-164">Si vous pouvez vous connecter à Internet sans utiliser votre proxy, vérifiez que l’Explorateur de stockage fonctionne sans les paramètres de proxy activés.</span><span class="sxs-lookup"><span data-stu-id="100f4-164">If you can connect to the Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="100f4-165">Si c’est le cas, le dysfonctionnement est peut-être lié à vos paramètres de proxy.</span><span class="sxs-lookup"><span data-stu-id="100f4-165">If this is the case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="100f4-166">Contactez l’administrateur de votre proxy pour identifier les problèmes.</span><span class="sxs-lookup"><span data-stu-id="100f4-166">Work with your proxy administrator to identify the problems.</span></span>

- <span data-ttu-id="100f4-167">Vérifiez que les autres applications utilisant le serveur proxy fonctionnent normalement.</span><span class="sxs-lookup"><span data-stu-id="100f4-167">Verify that other applications using the proxy server work as expected.</span></span>

- <span data-ttu-id="100f4-168">Vérifiez que vous pouvez vous connecter au portail Microsoft Azure à l’aide de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="100f4-168">Verify that you can connect to the Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="100f4-169">Vérifiez que vous pouvez recevoir des réponses de vos points de terminaison de service.</span><span class="sxs-lookup"><span data-stu-id="100f4-169">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="100f4-170">Entrez une des URL de point de terminaison dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="100f4-170">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="100f4-171">Si vous pouvez vous connecter, vous devez recevoir une réponse XML InvalidQueryParameterValue ou similaire.</span><span class="sxs-lookup"><span data-stu-id="100f4-171">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="100f4-172">Si quelqu’un d’autre utilise également l’Explorateur de stockage avec votre serveur proxy, vérifiez que cette personne peut se connecter.</span><span class="sxs-lookup"><span data-stu-id="100f4-172">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="100f4-173">Si elle le peut, vous devrez peut-être contacter l’administrateur de votre serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="100f4-173">If they can connect, you may have to contact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="100f4-174">Outils pour diagnostiquer les problèmes</span><span class="sxs-lookup"><span data-stu-id="100f4-174">Tools for diagnosing issues</span></span>

<span data-ttu-id="100f4-175">Si vous disposez d’outils de mise en réseau, tels que Fiddler pour Windows, vous pouvez peut-être diagnostiquer les problèmes comme suit :</span><span class="sxs-lookup"><span data-stu-id="100f4-175">If you have networking tools, such as Fiddler for Windows, you may be able to diagnose the problems as follows:</span></span>

- <span data-ttu-id="100f4-176">Si vous devez passer par votre serveur proxy, vous devez peut-être configurer votre outil de mise en réseau pour vous connecter via le proxy.</span><span class="sxs-lookup"><span data-stu-id="100f4-176">If you have to work through your proxy, you may have to configure your networking tool to connect through the proxy.</span></span>

- <span data-ttu-id="100f4-177">Vérifiez le numéro de port utilisé par votre outil de mise en réseau.</span><span class="sxs-lookup"><span data-stu-id="100f4-177">Check the port number used by your networking tool.</span></span>

- <span data-ttu-id="100f4-178">Entrez l’URL de l’hôte local et le numéro de port de l’outil de mise en réseau en tant que paramètres de proxy dans l’Explorateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="100f4-178">Enter the local host URL and the networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="100f4-179">Si cette opération est effectuée correctement, l’outil de mise en réseau démarre la journalisation des demandes réseau effectuées par l’Explorateur de stockage sur les points de terminaison de service et de gestion.</span><span class="sxs-lookup"><span data-stu-id="100f4-179">If this isdone correctly, your networking tool starts logging network requests made by Storage Explorer to management and service endpoints.</span></span> <span data-ttu-id="100f4-180">Par exemple, si vous entrez https://cawablobgrs.blob.core.windows.net/ pour votre point de terminaison d’objets blob dans un navigateur, vous recevez une réponse semblable à la suivante, qui suggère que la ressource existe, bien que vous ne puissiez pas y accéder.</span><span class="sxs-lookup"><span data-stu-id="100f4-180">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles the following, which suggests the resource exists, although you cannot access it.</span></span>

![Exemple de code](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="100f4-182">Contacter l’administrateur du serveur proxy</span><span class="sxs-lookup"><span data-stu-id="100f4-182">Contact proxy server admin</span></span>

<span data-ttu-id="100f4-183">Si vos paramètres de proxy sont corrects, vous devrez peut-être contacter l’administrateur de votre serveur proxy, puis :</span><span class="sxs-lookup"><span data-stu-id="100f4-183">If your proxy settings are correct, you may have to contact your proxy server admin, and</span></span>

- <span data-ttu-id="100f4-184">Vérifier que votre proxy ne bloque pas le trafic vers les points de terminaison de gestion ou de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="100f4-184">Make sure that your proxy does not block traffic to Azure management or resource endpoints.</span></span>

- <span data-ttu-id="100f4-185">Vérifier le protocole d’authentification utilisé par votre serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="100f4-185">Verify the authentication protocol used by your proxy server.</span></span> <span data-ttu-id="100f4-186">L’Explorateur de stockage ne prend pas en charge les proxys NTLM.</span><span class="sxs-lookup"><span data-stu-id="100f4-186">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-to-retrieve-children-error-message"></a><span data-ttu-id="100f4-187">Message d’erreur indiquant qu’il est impossible de récupérer les enfants</span><span class="sxs-lookup"><span data-stu-id="100f4-187">"Unable to Retrieve Children" error message</span></span>

<span data-ttu-id="100f4-188">Si vous êtes connecté à Azure par le biais d’un proxy, vérifiez que vos paramètres de proxy sont corrects.</span><span class="sxs-lookup"><span data-stu-id="100f4-188">If you are connected to Azure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="100f4-189">Si le propriétaire de l’abonnement ou du compte vous a accordé l’accès à une ressource, vérifiez que vous êtes habilité à lire ou à répertorier cette ressource.</span><span class="sxs-lookup"><span data-stu-id="100f4-189">If you were granted access to a resource from the owner of the subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="100f4-190">Problèmes liés à l’URL SAP</span><span class="sxs-lookup"><span data-stu-id="100f4-190">Issues with SAS URL</span></span>
<span data-ttu-id="100f4-191">Si vous vous connectez à un service à l’aide d’une URL SAP et que vous rencontrez cette erreur :</span><span class="sxs-lookup"><span data-stu-id="100f4-191">If you are connecting to a service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="100f4-192">Vérifiez que l’URL fournit les autorisations nécessaires pour lire ou répertorier les ressources.</span><span class="sxs-lookup"><span data-stu-id="100f4-192">Verify that the URL provides the necessary permissions to read or list resources.</span></span>

- <span data-ttu-id="100f4-193">Vérifiez que l’URL n’a pas expiré.</span><span class="sxs-lookup"><span data-stu-id="100f4-193">Verify that the URL has not expired.</span></span>

- <span data-ttu-id="100f4-194">Si l’URL SAP est basée sur une stratégie d’accès, vérifiez que cette dernière n’a pas été révoquée.</span><span class="sxs-lookup"><span data-stu-id="100f4-194">If the SAS URL is based on an access policy, verify that the access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="100f4-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="100f4-195">Next steps</span></span>

<span data-ttu-id="100f4-196">Si aucune des solutions ne convient, soumettez votre problème au moyen de l’outil de commentaires avec votre e-mail, en indiquant le maximum de détails sur le problème afin que nous puissions vous contacter pour le résoudre.</span><span class="sxs-lookup"><span data-stu-id="100f4-196">If none of the solutions work for you, submit your issue through the feedback tool with your email and as many details about the issue included as you can, so that we can contact you for fixing the issue.</span></span>

<span data-ttu-id="100f4-197">Pour ce faire, cliquez sur le menu **Aide**, puis sur **Envoyer des commentaires**.</span><span class="sxs-lookup"><span data-stu-id="100f4-197">To do this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Commentaires](./media/storage-explorer-troubleshooting/4022503_en_1.png)
