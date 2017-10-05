---
title: "Ajouter un certificat SSL à votre application Azure App Service | Microsoft Docs"
description: "Découvrez comment ajouter un certificat SSL à votre application App Service."
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: 191dd7240ad15b4936a72bc27a2d0162350f3afb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="e4af4-103">Acheter et configurer un certificat SSL pour votre service Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e4af4-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="e4af4-104">Dans ce didacticiel, vous allez sécuriser votre application web en achetant un certificat SSL pour votre **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, en le stockant dans [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) de manière sécurisée, et en l’associant à un domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="e4af4-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-to-azure"></a><span data-ttu-id="e4af4-105">Étape 1 : Se connecter à Azure</span><span class="sxs-lookup"><span data-stu-id="e4af4-105">Step 1 - Log in to Azure</span></span>

<span data-ttu-id="e4af4-106">Connectez-vous au portail Azure à l’adresse http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="e4af4-106">Log in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="e4af4-107">Étape 2 : Passer une commande de certificat SSL</span><span class="sxs-lookup"><span data-stu-id="e4af4-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="e4af4-108">Vous pouvez passer une commande de certificat SSL en créant un [Certificat App Service](https://portal.azure.com/#create/Microsoft.SSL) dans le **portail Azure**.</span><span class="sxs-lookup"><span data-stu-id="e4af4-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In the **Azure portal**.</span></span>

![Création du certificat](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="e4af4-110">Entrez un **nom** convivial pour votre certificat SSL et entrez le **nom de domaine**.</span><span class="sxs-lookup"><span data-stu-id="e4af4-110">Enter a friendly **Name** for your SSL certificate and enter the **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="e4af4-111">Il s’agit de l’une des parties les plus critiques du processus d’achat.</span><span class="sxs-lookup"><span data-stu-id="e4af4-111">This is one of the most critical parts of the purchase process.</span></span> <span data-ttu-id="e4af4-112">Veillez à entrer un nom d’hôte correct (domaine personnalisé) que vous voulez protéger avec ce certificat.</span><span class="sxs-lookup"><span data-stu-id="e4af4-112">Make sure to enter correct host name (custom domain) that you want to protect with this certificate.</span></span> <span data-ttu-id="e4af4-113">**PAS** le nom d’hôte avec WWW.</span><span class="sxs-lookup"><span data-stu-id="e4af4-113">**DO NOT** append the Host name with WWW.</span></span> 
>

<span data-ttu-id="e4af4-114">Sélectionnez votre **abonnement**, **groupe de ressources** et **référence (SKU) de certificat**</span><span class="sxs-lookup"><span data-stu-id="e4af4-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="e4af4-115">Les certificats App Service peuvent uniquement être utilisés par d’autres services App Service au sein du même abonnement.</span><span class="sxs-lookup"><span data-stu-id="e4af4-115">App Service Certificates can only be used by other App Services within the same subscription.</span></span>  
>

## <a name="step-3---store-the-certificate-in-azure-key-vault"></a><span data-ttu-id="e4af4-116">Étape 3 : Stocker le certificat dans Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="e4af4-116">Step 3 - Store the certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="e4af4-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) est un service Azure qui permet de protéger les clés de chiffrement et les secrets utilisés par les services et les applications cloud.</span><span class="sxs-lookup"><span data-stu-id="e4af4-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="e4af4-118">Une fois l’achat du certificat SSL terminé, vous devez ouvrir le panneau des ressources [Certificats App Service](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders).</span><span class="sxs-lookup"><span data-stu-id="e4af4-118">Once the SSL Certificate purchase is complete, you need to open [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![insérer une image de prêt à stocker dans KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="e4af4-120">Vous remarquerez que l’état du certificat est **« Émission en attente »** , car vous devez effectuer quelques étapes supplémentaires avant de commencer à utiliser ce certificat.</span><span class="sxs-lookup"><span data-stu-id="e4af4-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need to complete before you can start using this certificate.</span></span>

<span data-ttu-id="e4af4-121">Cliquez sur **Configuration du certificat** dans le panneau Propriétés du certificat, puis sur **Étape 1 : Stocker** pour stocker ce certificat dans Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="e4af4-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** to store this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="e4af4-122">Dans le panneau **État de Key Vault**, cliquez sur **Référentiel Key Vault** pour choisir un coffre de clés existant destiné à stocker ce certificat **OU Créer un coffre de clés** pour créer un coffre de clés dans les mêmes abonnement et groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e4af4-122">From **Key Vault Status** Blade, click **Key Vault Repository** to choose an existing Key Vault to store this certificate **OR Create New Key Vault** to create new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="e4af4-123">Azure Key Vault engendre peu de frais pour le stockage de ce certificat.</span><span class="sxs-lookup"><span data-stu-id="e4af4-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="e4af4-124">Pour plus d’informations, consultez **[Tarification d’Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="e4af4-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="e4af4-125">Une fois que le référentiel Key Vault où stocker le certificat est sélectionné, l’option **Stocker** doit indiquer que l’opération a réussi.</span><span class="sxs-lookup"><span data-stu-id="e4af4-125">Once you have selected the Key Vault Repository to store this certificate in, the **Store** option should show success.</span></span>

![insérer une image de réussite du stockage dans KV](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-the-domain-ownership"></a><span data-ttu-id="e4af4-127">Étape 4 : Vérifier la propriété du domaine</span><span class="sxs-lookup"><span data-stu-id="e4af4-127">Step 4 - Verify the Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="e4af4-128">Il existe 3 types de vérification du domaine pris en charge par les certificats App Service : domaine, e-mail et manuelle.</span><span class="sxs-lookup"><span data-stu-id="e4af4-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="e4af4-129">Elles sont décrites plus en détail dans la [section Avancé](#advanced).</span><span class="sxs-lookup"><span data-stu-id="e4af4-129">These are explained in more details in the [Advanced section](#advanced).</span></span>

<span data-ttu-id="e4af4-130">Dans le panneau **Configuration du certificat** utilisé à l’étape 3, cliquez sur **Étape 2 : Vérifier**.</span><span class="sxs-lookup"><span data-stu-id="e4af4-130">From the same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="e4af4-131">**Vérification du domaine** Il s’agit du processus le plus pratique **seulement si** vous avez **[acheté votre domaine personnalisé à partir d’Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="e4af4-131">**Domain Verification** This is the most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="e4af4-132">Cliquez sur le bouton **Vérifier** pour terminer cette étape.</span><span class="sxs-lookup"><span data-stu-id="e4af4-132">Click on **Verify** button to complete this step.</span></span>

![insérer une image de vérification du domaine](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="e4af4-134">Après avoir cliqué sur **Vérifier**, utilisez le bouton **Actualiser** jusqu’à ce que l’option **Vérifier** indique que l’opération a réussi.</span><span class="sxs-lookup"><span data-stu-id="e4af4-134">After clicking **Verify**, use the **Refresh** button until the **Verify** option should show success.</span></span>

![insérer une image de réussite de la vérification dans KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-to-app-service-app"></a><span data-ttu-id="e4af4-136">Étape 5 : Attribuer un certificat à une application App Service</span><span class="sxs-lookup"><span data-stu-id="e4af4-136">Step 5 - Assign Certificate to App Service App</span></span>

> [!NOTE]
> <span data-ttu-id="e4af4-137">Avant de suivre les étapes de cette section, vous devez avoir associé un nom de domaine personnalisé à votre application.</span><span class="sxs-lookup"><span data-stu-id="e4af4-137">Before performing the steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="e4af4-138">Pour plus d’informations, consultez la page **[Configuration d’un nom de domaine personnalisé pour une application web.](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="e4af4-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="e4af4-139">Dans le **[portail Azure](https://portal.azure.com/)**, cliquez sur l’option **App Service** sur le côté gauche de la page.</span><span class="sxs-lookup"><span data-stu-id="e4af4-139">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="e4af4-140">Cliquez sur le nom de votre application à laquelle vous voulez attribuer ce certificat.</span><span class="sxs-lookup"><span data-stu-id="e4af4-140">Click the name of your app to which you want to assign this certificate.</span></span>

<span data-ttu-id="e4af4-141">Dans les **Paramètres**, cliquez sur **Certificats SSL**.</span><span class="sxs-lookup"><span data-stu-id="e4af4-141">In the **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="e4af4-142">Cliquez sur **Importer un certificat App Service**, puis sélectionnez le certificat que vous venez d’acheter.</span><span class="sxs-lookup"><span data-stu-id="e4af4-142">Click **Import App Service Certificate** and select the certificate that you just purchased.</span></span>

![insérer une image d’importation de certificat](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="e4af4-144">Dans la section **Liaisons SSL**, cliquez sur **Ajouter des liaisons** et utilisez les listes déroulantes pour sélectionner le nom de domaine à sécuriser à l’aide du protocole SSL, ainsi que le certificat à utiliser.</span><span class="sxs-lookup"><span data-stu-id="e4af4-144">In the **ssl bindings** section Click on **Add bindings**, and use the dropdowns to select the domain name to secure with SSL, and the certificate to use.</span></span> <span data-ttu-id="e4af4-145">Vous pouvez également indiquer si vous voulez utiliser **[l’indication du nom du serveur (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** ou le protocole SSL basé sur IP.</span><span class="sxs-lookup"><span data-stu-id="e4af4-145">You may also select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![insérer une image de liaisons SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="e4af4-147">Cliquez sur **Ajouter une liaison** pour enregistrer les modifications et activer SSL.</span><span class="sxs-lookup"><span data-stu-id="e4af4-147">Click **Add Binding** to save the changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="e4af4-148">Si vous avez sélectionné **SSL basé sur IP** et que votre domaine personnalisé est configuré à l’aide d’un enregistrement A, vous devez effectuer les étapes supplémentaires suivantes.</span><span class="sxs-lookup"><span data-stu-id="e4af4-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps.</span></span> <span data-ttu-id="e4af4-149">Elles sont décrites plus en détail dans la [section Avancé](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="e4af4-149">These are explained in more details in the [Advanced section](#Advanced).</span></span>

<span data-ttu-id="e4af4-150">À ce stade, vous devez être en mesure de visiter votre application en utilisant `HTTPS://` à la place de `HTTP://` pour vérifier que le certificat a été configuré correctement.</span><span class="sxs-lookup"><span data-stu-id="e4af4-150">At this point, you should be able to visit your app using `HTTPS://` instead of `HTTP://` to verify that the certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="e4af4-151">Étape 6 : Tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="e4af4-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="e4af4-152">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="e4af4-152">Azure CLI</span></span>

<span data-ttu-id="e4af4-153">[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Lier un certificat SSL personnalisé à une application web")]</span><span class="sxs-lookup"><span data-stu-id="e4af4-153">[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span> 

### <a name="powershell"></a><span data-ttu-id="e4af4-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4af4-154">PowerShell</span></span>

<span data-ttu-id="e4af4-155">[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Lier un certificat SSL personnalisé à une application web")]</span><span class="sxs-lookup"><span data-stu-id="e4af4-155">[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="advanced"></a><span data-ttu-id="e4af4-156">Avancé</span><span class="sxs-lookup"><span data-stu-id="e4af4-156">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="e4af4-157">Vérifier la propriété du domaine</span><span class="sxs-lookup"><span data-stu-id="e4af4-157">Verifying Domain Ownership</span></span>

<span data-ttu-id="e4af4-158">Il existe 2 autres types de vérification du domaine pris en charge par les certificats App Service : e-mail et manuelle.</span><span class="sxs-lookup"><span data-stu-id="e4af4-158">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="e4af4-159">Vérification par e-mail</span><span class="sxs-lookup"><span data-stu-id="e4af4-159">Mail Verification</span></span>

<span data-ttu-id="e4af4-160">Un e-mail de vérification a déjà été envoyé aux adresses e-mail associées à ce domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="e4af4-160">Verification email has already been sent to the Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="e4af4-161">Pour terminer l’étape de vérification par e-mail, ouvrez l’e-mail, puis cliquez sur le lien de vérification.</span><span class="sxs-lookup"><span data-stu-id="e4af4-161">To complete the Email verification step, open the email and click the verification link.</span></span>

![insérer une image de vérification par e-mail](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="e4af4-163">Si vous avez besoin de renvoyer l’e-mail de vérification, cliquez sur le bouton **Renvoyer le message**.</span><span class="sxs-lookup"><span data-stu-id="e4af4-163">If you need to resend the verification email, click the **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="e4af4-164">Vérification manuelle</span><span class="sxs-lookup"><span data-stu-id="e4af4-164">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4af4-165">Vérification de page web HTML (fonctionne uniquement avec la référence du certificat standard)</span><span class="sxs-lookup"><span data-stu-id="e4af4-165">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="e4af4-166">Créez un fichier HTML nommé **« starfield.html »**</span><span class="sxs-lookup"><span data-stu-id="e4af4-166">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="e4af4-167">Le contenu de ce fichier doit être le nom exact du jeton de vérification du domaine.</span><span class="sxs-lookup"><span data-stu-id="e4af4-167">Content of this file should be the exact name of the Domain Verification Token.</span></span> <span data-ttu-id="e4af4-168">(Vous pouvez copier le jeton à partir du panneau d’état de la vérification du domaine.)</span><span class="sxs-lookup"><span data-stu-id="e4af4-168">(You can copy the token from the Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="e4af4-169">Chargez ce fichier à la racine du serveur web qui héberge votre domaine `/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="e4af4-169">Upload this file at the root of the web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="e4af4-170">Cliquez sur **« Actualiser »** pour mettre à jour l’état du certificat une fois la vérification terminée.</span><span class="sxs-lookup"><span data-stu-id="e4af4-170">Click **Refresh** to update the certificate status after verification is completed.</span></span> <span data-ttu-id="e4af4-171">Cette vérification peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="e4af4-171">It might take few minutes for verification to complete.</span></span>

> [!TIP]
> <span data-ttu-id="e4af4-172">Effectuez la vérification dans un terminal utilisant `curl -G http://<domain>/.well-known/pki-validation/starfield.html`. La réponse doit contenir le `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="e4af4-172">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` the response should contain the `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="e4af4-173">Vérification d’enregistrement TXT DNS</span><span class="sxs-lookup"><span data-stu-id="e4af4-173">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="e4af4-174">À l’aide de votre Gestionnaire DNS, créez un enregistrement TXT sur le sous-domaine `@` avec une valeur égale au jeton de vérification du domaine.</span><span class="sxs-lookup"><span data-stu-id="e4af4-174">Using your DNS manager, Create a TXT record on the `@` subdomain with value equal to the Domain Verification Token.</span></span>
1. <span data-ttu-id="e4af4-175">Cliquez sur **« Actualiser »** pour mettre à jour l’état du certificat une fois la vérification terminée.</span><span class="sxs-lookup"><span data-stu-id="e4af4-175">Click **“Refresh”** to update the Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="e4af4-176">Vous devez créer un enregistrement TXT sur `@.<domain>` avec la valeur `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="e4af4-176">You need to create a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-to-app-service-app"></a><span data-ttu-id="e4af4-177">Attribuer un certificat à une application App Service</span><span class="sxs-lookup"><span data-stu-id="e4af4-177">Assign Certificate to App Service App</span></span>

<span data-ttu-id="e4af4-178">Si vous avez sélectionné **SSL basé sur IP** et que votre domaine personnalisé est configuré à l’aide d’un enregistrement A, vous devez effectuer les étapes supplémentaires suivantes :</span><span class="sxs-lookup"><span data-stu-id="e4af4-178">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps:</span></span>

<span data-ttu-id="e4af4-179">Une fois la liaison SSL basée sur IP configurée, une adresse IP dédiée est attribuée à votre application.</span><span class="sxs-lookup"><span data-stu-id="e4af4-179">After you have configured an IP based SSL binding, a dedicated IP address is assigned to your app.</span></span> <span data-ttu-id="e4af4-180">Vous trouverez cette adresse IP sur la page des **domaines personnalisés** sous les paramètres de votre application, juste au-dessus de la section **Noms d’hôtes**.</span><span class="sxs-lookup"><span data-stu-id="e4af4-180">You can find this IP address on the **Custom domain** page under settings of your app, right above the **Hostnames** section.</span></span> <span data-ttu-id="e4af4-181">Elle est répertoriée en tant qu’**Adresse IP externe**</span><span class="sxs-lookup"><span data-stu-id="e4af4-181">It is listed as **External IP Address**</span></span>

![insérer une image d’IP SSL](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="e4af4-183">Cette adresse IP est différente de celle utilisée précédemment pour configurer l’enregistrement A de votre domaine.</span><span class="sxs-lookup"><span data-stu-id="e4af4-183">Note that this IP address is different than the virtual IP address used previously to configure the A record for your domain.</span></span> <span data-ttu-id="e4af4-184">Si vous utilisez le protocole SSL basé sur SNI ou que vous n’utilisez pas SSL, aucune adresse n’est indiquée pour cette entrée.</span><span class="sxs-lookup"><span data-stu-id="e4af4-184">If you are configured to use SNI based SSL, or are not configured to use SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="e4af4-185">À l’aide des outils fournis par votre bureau d’enregistrement, modifiez l’enregistrement A de votre nom de domaine personnalisé de manière à ce qu’il pointe vers l’adresse IP spécifiée lors de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="e4af4-185">Using the tools provided by your domain name registrar, modify the A record for your custom domain name to point to the IP address from the previous step.</span></span>

## <a name="rekey-and-sync-the-certificate"></a><span data-ttu-id="e4af4-186">Renouveler la clé du certificat et le synchroniser</span><span class="sxs-lookup"><span data-stu-id="e4af4-186">Rekey and Sync the Certificate</span></span>

<span data-ttu-id="e4af4-187">Si vous avez besoin de renouveler la clé de votre certificat, sélectionnez l’option **Recréer la clé et synchroniser** à partir du panneau **Propriétés du certificat**.</span><span class="sxs-lookup"><span data-stu-id="e4af4-187">If you ever need to Rekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="e4af4-188">Cliquez sur le bouton **Renouveler la clé** pour lancer le processus.</span><span class="sxs-lookup"><span data-stu-id="e4af4-188">Click **Rekey** Button to initiate the process.</span></span> <span data-ttu-id="e4af4-189">Ce processus peut prendre de 1 à 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="e4af4-189">This process can take 1-10 minutes to complete.</span></span>

![insérer une image de renouvellement de clé SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="e4af4-191">Le renouvellement de la clé de votre certificat remplace le certificat par un nouveau certificat émis par l’autorité de certification.</span><span class="sxs-lookup"><span data-stu-id="e4af4-191">Rekeying your certificate rolls the certificate with a new certificate issued from the certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4af4-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e4af4-192">Next Steps</span></span>

* [<span data-ttu-id="e4af4-193">Ajouter un réseau de distribution de contenu</span><span class="sxs-lookup"><span data-stu-id="e4af4-193">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)