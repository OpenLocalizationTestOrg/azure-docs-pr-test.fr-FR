---
title: "application de Service d’applications Azure tooyour de certificats aaaAdd une connexion SSL | Documents Microsoft"
description: "Découvrez comment tooadd une connexion SSL certificat tooyour application de Service d’applications."
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
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="38b45-103">Acheter et configurer un certificat SSL pour votre service Azure App Service</span><span class="sxs-lookup"><span data-stu-id="38b45-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="38b45-104">Dans ce didacticiel, vous allez sécuriser votre application web en achetant un certificat SSL pour votre **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, en le stockant dans [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) de manière sécurisée, et en l’associant à un domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="38b45-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-tooazure"></a><span data-ttu-id="38b45-105">Étape 1 : ouvrez une session dans tooAzure</span><span class="sxs-lookup"><span data-stu-id="38b45-105">Step 1 - Log in tooAzure</span></span>

<span data-ttu-id="38b45-106">Ouvrez une session dans toohello portail Azure à http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="38b45-106">Log in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="38b45-107">Étape 2 : Passer une commande de certificat SSL</span><span class="sxs-lookup"><span data-stu-id="38b45-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="38b45-108">Vous pouvez placer une commande de certificat SSL en créant un [certificat de Service de l’application](https://portal.azure.com/#create/Microsoft.SSL) Bonjour **portail Azure**.</span><span class="sxs-lookup"><span data-stu-id="38b45-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In hello **Azure portal**.</span></span>

![Création du certificat](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="38b45-110">Entrez un nom convivial de **nom** de certificat pour SSL et entrez hello **nom de domaine**</span><span class="sxs-lookup"><span data-stu-id="38b45-110">Enter a friendly **Name** for your SSL certificate and enter hello **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="38b45-111">Il s’agit d’une des parties essentielles de hello du processus d’achat hello.</span><span class="sxs-lookup"><span data-stu-id="38b45-111">This is one of hello most critical parts of hello purchase process.</span></span> <span data-ttu-id="38b45-112">Assurez-vous que tooenter corriger le nom d’hôte (domaine personnalisé) que vous souhaitez tooprotect avec ce certificat.</span><span class="sxs-lookup"><span data-stu-id="38b45-112">Make sure tooenter correct host name (custom domain) that you want tooprotect with this certificate.</span></span> <span data-ttu-id="38b45-113">**Ne le faites pas** ajouter le nom d’hôte hello avec WWW.</span><span class="sxs-lookup"><span data-stu-id="38b45-113">**DO NOT** append hello Host name with WWW.</span></span> 
>

<span data-ttu-id="38b45-114">Sélectionnez votre **abonnement**, **groupe de ressources** et **référence (SKU) de certificat**</span><span class="sxs-lookup"><span data-stu-id="38b45-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="38b45-115">Certificats de Service d’application exclusivement par d’autres Services d’application au sein de hello même abonnement.</span><span class="sxs-lookup"><span data-stu-id="38b45-115">App Service Certificates can only be used by other App Services within hello same subscription.</span></span>  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a><span data-ttu-id="38b45-116">Étape 3 : stocker le certificat hello dans Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="38b45-116">Step 3 - Store hello certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="38b45-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) est un service Azure qui permet de protéger les clés de chiffrement et les secrets utilisés par les services et les applications cloud.</span><span class="sxs-lookup"><span data-stu-id="38b45-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="38b45-118">Une fois hello achat du certificat SSL est terminée, vous devez tooopen [App Service Certificate](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) panneau des ressources.</span><span class="sxs-lookup"><span data-stu-id="38b45-118">Once hello SSL Certificate purchase is complete, you need tooopen [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![Insérer une image de toostore prêt dans KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="38b45-120">Vous remarquerez que l’état du certificat est **« Émission en attente »** qu’il sont a quelques étapes supplémentaires vous devez toocomplete avant de commencer à l’aide de ce certificat.</span><span class="sxs-lookup"><span data-stu-id="38b45-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need toocomplete before you can start using this certificate.</span></span>

<span data-ttu-id="38b45-121">Cliquez sur **Configuration de certificat** à l’intérieur du panneau des propriétés du certificat, puis cliquez sur **étape 1 : magasin** toostore ce certificat dans Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="38b45-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** toostore this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="38b45-122">À partir de **clé de coffre état** panneau, cliquez sur **référentiel de coffre de clé** toochoose un toostore de coffre de clés existant ce certificat **ou créer nouveau coffre de clés** toocreate nouvelle clé de coffre à l’intérieur du même groupe d’abonnement et de ressources.</span><span class="sxs-lookup"><span data-stu-id="38b45-122">From **Key Vault Status** Blade, click **Key Vault Repository** toochoose an existing Key Vault toostore this certificate **OR Create New Key Vault** toocreate new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="38b45-123">Azure Key Vault engendre peu de frais pour le stockage de ce certificat.</span><span class="sxs-lookup"><span data-stu-id="38b45-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="38b45-124">Pour plus d’informations, consultez **[Tarification d’Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="38b45-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="38b45-125">Après avoir sélectionné hello référentiel de coffre de clé toostore ce certificat dans, hello **magasin** option doit afficher succès.</span><span class="sxs-lookup"><span data-stu-id="38b45-125">Once you have selected hello Key Vault Repository toostore this certificate in, hello **Store** option should show success.</span></span>

![insérer une image de réussite du stockage dans KV](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a><span data-ttu-id="38b45-127">Étape 4 - vérifier hello la propriété du domaine</span><span class="sxs-lookup"><span data-stu-id="38b45-127">Step 4 - Verify hello Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="38b45-128">Il existe 3 types de vérification du domaine pris en charge par les certificats App Service : domaine, e-mail et manuelle.</span><span class="sxs-lookup"><span data-stu-id="38b45-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="38b45-129">Ceux-ci sont expliquées plus en détails dans hello [avancé section](#advanced).</span><span class="sxs-lookup"><span data-stu-id="38b45-129">These are explained in more details in hello [Advanced section](#advanced).</span></span>

<span data-ttu-id="38b45-130">À partir de hello même **Configuration de certificat** panneau que vous avez utilisé à l’étape 3, cliquez sur **étape 2 : vérifier**.</span><span class="sxs-lookup"><span data-stu-id="38b45-130">From hello same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="38b45-131">**Vérification du domaine** ce processus plus pratique de hello est **uniquement si** avoir  **[acheté votre domaine personnalisé à partir du Service d’applications Azure.](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="38b45-131">**Domain Verification** This is hello most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="38b45-132">Cliquez sur **Vérifiez** bouton toocomplete cette étape.</span><span class="sxs-lookup"><span data-stu-id="38b45-132">Click on **Verify** button toocomplete this step.</span></span>

![insérer une image de vérification du domaine](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="38b45-134">Après avoir cliqué sur **Vérifiez**, utilisez hello **Actualiser** bouton jusqu'à ce que hello **Vérifiez** option doit afficher succès.</span><span class="sxs-lookup"><span data-stu-id="38b45-134">After clicking **Verify**, use hello **Refresh** button until hello **Verify** option should show success.</span></span>

![insérer une image de réussite de la vérification dans KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a><span data-ttu-id="38b45-136">Étape 5 : affecter tooApp du certificat de Service d’applications</span><span class="sxs-lookup"><span data-stu-id="38b45-136">Step 5 - Assign Certificate tooApp Service App</span></span>

> [!NOTE]
> <span data-ttu-id="38b45-137">Avant d’effectuer les étapes hello dans cette section, vous devez associé un nom de domaine personnalisé avec votre application.</span><span class="sxs-lookup"><span data-stu-id="38b45-137">Before performing hello steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="38b45-138">Pour plus d’informations, consultez la page **[Configuration d’un nom de domaine personnalisé pour une application web.](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="38b45-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="38b45-139">Bonjour  **[portail Azure](https://portal.azure.com/)**, cliquez sur hello **du Service d’applications** option à gauche de hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="38b45-139">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="38b45-140">Cliquez sur le nom de hello de votre application toowhich souhaité tooassign ce certificat.</span><span class="sxs-lookup"><span data-stu-id="38b45-140">Click hello name of your app toowhich you want tooassign this certificate.</span></span>

<span data-ttu-id="38b45-141">Bonjour **paramètres**, cliquez sur **certificats SSL**.</span><span class="sxs-lookup"><span data-stu-id="38b45-141">In hello **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="38b45-142">Cliquez sur **importer un certificat Service application** et sélectionnez hello certificat que vous venez d’acheter.</span><span class="sxs-lookup"><span data-stu-id="38b45-142">Click **Import App Service Certificate** and select hello certificate that you just purchased.</span></span>

![insérer une image d’importation de certificat](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="38b45-144">Bonjour **liaisons ssl** section cliquez sur **ajouter des liaisons**et utilisez hello menus déroulants tooselect hello domaine nom toosecure avec SSL, hello toouse de certificat.</span><span class="sxs-lookup"><span data-stu-id="38b45-144">In hello **ssl bindings** section Click on **Add bindings**, and use hello dropdowns tooselect hello domain name toosecure with SSL, and hello certificate toouse.</span></span> <span data-ttu-id="38b45-145">Vous pouvez également sélectionner si toouse  **[Indication de nom de serveur (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  ou SSL basé sur IP.</span><span class="sxs-lookup"><span data-stu-id="38b45-145">You may also select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![insérer une image de liaisons SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="38b45-147">Cliquez sur **ajouter la liaison de** toosave hello les modifications et activer le protocole SSL.</span><span class="sxs-lookup"><span data-stu-id="38b45-147">Click **Add Binding** toosave hello changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="38b45-148">Si vous avez sélectionné **SSL basé sur IP** et votre domaine personnalisé est configuré à l’aide d’un enregistrement A, vous devez effectuer des hello supplémentaires comme suit.</span><span class="sxs-lookup"><span data-stu-id="38b45-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps.</span></span> <span data-ttu-id="38b45-149">Ceux-ci sont expliquées plus en détails dans hello [avancé section](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="38b45-149">These are explained in more details in hello [Advanced section](#Advanced).</span></span>

<span data-ttu-id="38b45-150">À ce stade, vous doit être en mesure de toovisit à votre application à l’aide de `HTTPS://` au lieu de `HTTP://` tooverify qui hello certificat a été configuré correctement.</span><span class="sxs-lookup"><span data-stu-id="38b45-150">At this point, you should be able toovisit your app using `HTTPS://` instead of `HTTP://` tooverify that hello certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="38b45-151">Étape 6 : Tâches de gestion</span><span class="sxs-lookup"><span data-stu-id="38b45-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="38b45-152">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="38b45-152">Azure CLI</span></span>

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a><span data-ttu-id="38b45-153">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38b45-153">PowerShell</span></span>

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a><span data-ttu-id="38b45-154">Avancé</span><span class="sxs-lookup"><span data-stu-id="38b45-154">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="38b45-155">Vérifier la propriété du domaine</span><span class="sxs-lookup"><span data-stu-id="38b45-155">Verifying Domain Ownership</span></span>

<span data-ttu-id="38b45-156">Il existe 2 autres types de vérification du domaine pris en charge par les certificats App Service : e-mail et manuelle.</span><span class="sxs-lookup"><span data-stu-id="38b45-156">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="38b45-157">Vérification par e-mail</span><span class="sxs-lookup"><span data-stu-id="38b45-157">Mail Verification</span></span>

<span data-ttu-id="38b45-158">Message de vérification a déjà été envoyée à toohello que les adresses de messagerie associé à ce domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="38b45-158">Verification email has already been sent toohello Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="38b45-159">étape de vérification toocomplete hello par courrier électronique, par courrier électronique hello, cliquez sur le lien de vérification hello.</span><span class="sxs-lookup"><span data-stu-id="38b45-159">toocomplete hello Email verification step, open hello email and click hello verification link.</span></span>

![insérer une image de vérification par e-mail](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="38b45-161">Si vous avez besoin de message de vérification tooresend hello, cliquez sur hello **renvoyer un E-mail** bouton.</span><span class="sxs-lookup"><span data-stu-id="38b45-161">If you need tooresend hello verification email, click hello **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="38b45-162">Vérification manuelle</span><span class="sxs-lookup"><span data-stu-id="38b45-162">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38b45-163">Vérification de page web HTML (fonctionne uniquement avec la référence du certificat standard)</span><span class="sxs-lookup"><span data-stu-id="38b45-163">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="38b45-164">Créez un fichier HTML nommé **« starfield.html »**</span><span class="sxs-lookup"><span data-stu-id="38b45-164">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="38b45-165">Contenu de ce fichier doit être nom exact de hello Hello jeton de vérification de domaine.</span><span class="sxs-lookup"><span data-stu-id="38b45-165">Content of this file should be hello exact name of hello Domain Verification Token.</span></span> <span data-ttu-id="38b45-166">(Vous pouvez copier le jeton de hello de hello Panneau de statut de vérification de domaine)</span><span class="sxs-lookup"><span data-stu-id="38b45-166">(You can copy hello token from hello Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="38b45-167">Télécharger ce fichier à la racine de hello du serveur web de hello hébergeant votre domaine`/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="38b45-167">Upload this file at hello root of hello web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="38b45-168">Cliquez sur **Actualiser** tooupdate état du certificat hello après la vérification est terminée.</span><span class="sxs-lookup"><span data-stu-id="38b45-168">Click **Refresh** tooupdate hello certificate status after verification is completed.</span></span> <span data-ttu-id="38b45-169">Il peut prendre quelques minutes pour toocomplete de vérification.</span><span class="sxs-lookup"><span data-stu-id="38b45-169">It might take few minutes for verification toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="38b45-170">Vérifiez dans un à l’aide de Terminal Server `curl -G http://<domain>/.well-known/pki-validation/starfield.html` réponse de hello doit contenir hello `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="38b45-170">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello response should contain hello `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="38b45-171">Vérification d’enregistrement TXT DNS</span><span class="sxs-lookup"><span data-stu-id="38b45-171">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="38b45-172">Le Gestionnaire DNS, de créer un enregistrement TXT sur hello `@` sous-domaine avec la valeur de toohello égale jeton de vérification de domaine.</span><span class="sxs-lookup"><span data-stu-id="38b45-172">Using your DNS manager, Create a TXT record on hello `@` subdomain with value equal toohello Domain Verification Token.</span></span>
1. <span data-ttu-id="38b45-173">Cliquez sur **« Actualiser »** tooupdate hello état du certificat une fois la vérification est terminée.</span><span class="sxs-lookup"><span data-stu-id="38b45-173">Click **“Refresh”** tooupdate hello Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="38b45-174">Vous avez besoin d’un enregistrement TXT de toocreate sur `@.<domain>` avec la valeur `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="38b45-174">You need toocreate a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-tooapp-service-app"></a><span data-ttu-id="38b45-175">Affecter le certificat tooApp application de Service</span><span class="sxs-lookup"><span data-stu-id="38b45-175">Assign Certificate tooApp Service App</span></span>

<span data-ttu-id="38b45-176">Si vous avez sélectionné **SSL basé sur IP** et votre domaine personnalisé est configuré à l’aide d’un enregistrement A, vous devez effectuer des hello supplémentaires comme suit :</span><span class="sxs-lookup"><span data-stu-id="38b45-176">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps:</span></span>

<span data-ttu-id="38b45-177">Après avoir configuré une adresse IP en fonction de liaison SSL, une adresse IP dédiée est affectée tooyour application.</span><span class="sxs-lookup"><span data-stu-id="38b45-177">After you have configured an IP based SSL binding, a dedicated IP address is assigned tooyour app.</span></span> <span data-ttu-id="38b45-178">Vous pouvez trouver cette adresse IP sur hello **un domaine personnalisé** page sous les paramètres de votre application, juste au-dessus de hello **noms d’hôtes** section.</span><span class="sxs-lookup"><span data-stu-id="38b45-178">You can find this IP address on hello **Custom domain** page under settings of your app, right above hello **Hostnames** section.</span></span> <span data-ttu-id="38b45-179">Elle est répertoriée en tant qu’**Adresse IP externe**</span><span class="sxs-lookup"><span data-stu-id="38b45-179">It is listed as **External IP Address**</span></span>

![insérer une image d’IP SSL](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="38b45-181">Notez que cette adresse IP est différente de celle de l’adresse IP virtuelle hello utilisé précédemment enregistrement tooconfigure hello pour votre domaine.</span><span class="sxs-lookup"><span data-stu-id="38b45-181">Note that this IP address is different than hello virtual IP address used previously tooconfigure hello A record for your domain.</span></span> <span data-ttu-id="38b45-182">Si vous avez configuré toouse SSL basé sur SNI, ou ne sont pas configurés toouse SSL, aucune adresse n’est répertoriée pour cette entrée.</span><span class="sxs-lookup"><span data-stu-id="38b45-182">If you are configured toouse SNI based SSL, or are not configured toouse SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="38b45-183">À l’aide des outils de hello fournis par votre bureau d’enregistrement du nom de domaine, modifiez hello un enregistrement pour votre domaine personnalisé nom toopoint toohello adresse IP à partir de l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="38b45-183">Using hello tools provided by your domain name registrar, modify hello A record for your custom domain name toopoint toohello IP address from hello previous step.</span></span>

## <a name="rekey-and-sync-hello-certificate"></a><span data-ttu-id="38b45-184">Changement de clé et hello de synchronisation des certificats</span><span class="sxs-lookup"><span data-stu-id="38b45-184">Rekey and Sync hello Certificate</span></span>

<span data-ttu-id="38b45-185">Si vous avez besoin tooRekey votre certificat, sélectionnez **recomposition la synchronisation et** option à partir de **propriétés du certificat** panneau.</span><span class="sxs-lookup"><span data-stu-id="38b45-185">If you ever need tooRekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="38b45-186">Cliquez sur **recomposition** bouton processus de hello tooinitiate.</span><span class="sxs-lookup"><span data-stu-id="38b45-186">Click **Rekey** Button tooinitiate hello process.</span></span> <span data-ttu-id="38b45-187">Ce processus peut prendre toocomplete de 1 à 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="38b45-187">This process can take 1-10 minutes toocomplete.</span></span>

![insérer une image de renouvellement de clé SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="38b45-189">Régénération de votre certificat restaure certificat hello avec un nouveau certificat émis à partir de l’autorité de certification hello.</span><span class="sxs-lookup"><span data-stu-id="38b45-189">Rekeying your certificate rolls hello certificate with a new certificate issued from hello certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38b45-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="38b45-190">Next Steps</span></span>

* [<span data-ttu-id="38b45-191">Ajouter un réseau de distribution de contenu</span><span class="sxs-lookup"><span data-stu-id="38b45-191">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)