---
title: "aaaBind un SSL personnalisé existant de certificats des applications Web tooAzure | Documents Microsoft"
description: "En savoir plus tootoobind une application de web tooyour de certificat SSL personnalisée, principal de l’application mobile ou API app dans Azure App Service."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a><span data-ttu-id="e7617-103">Lier un tooAzure de certificat SSL personnalisé existant Web Apps</span><span class="sxs-lookup"><span data-stu-id="e7617-103">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>

<span data-ttu-id="e7617-104">Azure Web Apps fournit un service d’hébergement hautement évolutif et appliquant des mises à jour correctives automatiquement.</span><span class="sxs-lookup"><span data-stu-id="e7617-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="e7617-105">Ce didacticiel vous montre comment toobind une SSL personnalisée de certificats que vous avez acheté auprès d’une autorité de certification approuvée trop[Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7617-105">This tutorial shows you how toobind a custom SSL certificate that you purchased from a trusted certificate authority too[Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="e7617-106">Lorsque vous avez terminé, vous serez en mesure de tooaccess votre application web au point de terminaison HTTPS hello de votre domaine DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="e7617-106">When you're finished, you'll be able tooaccess your web app at hello HTTPS endpoint of your custom DNS domain.</span></span>

![Application Web avec certificat SSL personnalisé](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="e7617-108">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e7617-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e7617-109">Mettre à jour le niveau de tarification de votre application</span><span class="sxs-lookup"><span data-stu-id="e7617-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="e7617-110">Lier votre tooApp de certificat SSL Service personnalisé</span><span class="sxs-lookup"><span data-stu-id="e7617-110">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="e7617-111">Appliquer le protocole HTTPS à votre application</span><span class="sxs-lookup"><span data-stu-id="e7617-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="e7617-112">Automatiser la liaison de certificat SSL avec des scripts</span><span class="sxs-lookup"><span data-stu-id="e7617-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="e7617-113">Si vous avez besoin de tooget un certificat SSL personnalisé, vous pouvez en obtenir un Bonjour Azure portal directement et liez-le à l’application web tooyour.</span><span class="sxs-lookup"><span data-stu-id="e7617-113">If you need tooget a custom SSL certificate, you can get one in hello Azure portal directly and bind it tooyour web app.</span></span> <span data-ttu-id="e7617-114">Suivez hello [didacticiel de certificats de Service d’application](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="e7617-114">Follow hello [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e7617-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e7617-115">Prerequisites</span></span>

<span data-ttu-id="e7617-116">toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="e7617-116">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="e7617-117">Création d’une application App Service</span><span class="sxs-lookup"><span data-stu-id="e7617-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="e7617-118">Mapper une application personnalisée DNS nom tooyour web</span><span class="sxs-lookup"><span data-stu-id="e7617-118">Map a custom DNS name tooyour web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="e7617-119">Acquisition d’un certificat SSL auprès d’une autorité de certification approuvée</span><span class="sxs-lookup"><span data-stu-id="e7617-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="e7617-120">Conditions requises pour le certificat SSL</span><span class="sxs-lookup"><span data-stu-id="e7617-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="e7617-121">toouse un certificat dans le Service d’applications, les certificats hello doivent respecter toutes les hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="e7617-121">toouse a certificate in App Service, hello certificate must meet all hello following requirements:</span></span>

* <span data-ttu-id="e7617-122">Être signé par une autorité de certification approuvée</span><span class="sxs-lookup"><span data-stu-id="e7617-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="e7617-123">Être exporté sous la forme d’un fichier PFX protégé par mot de passe</span><span class="sxs-lookup"><span data-stu-id="e7617-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="e7617-124">Contenir une clé privée d’au moins 2048 bits de long</span><span class="sxs-lookup"><span data-stu-id="e7617-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="e7617-125">Contient tous les certificats intermédiaires dans la chaîne de certificats hello</span><span class="sxs-lookup"><span data-stu-id="e7617-125">Contains all intermediate certificates in hello certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="e7617-126">Les **certificats de chiffrement à courbe elliptique (ECC)** sont compatibles avec App Service, mais ce sujet sort du cadre de cet article.</span><span class="sxs-lookup"><span data-stu-id="e7617-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="e7617-127">Travailler avec votre autorité de certification sur les certificats ECC de hello étapes exactes toocreate.</span><span class="sxs-lookup"><span data-stu-id="e7617-127">Work with your certificate authority on hello exact steps toocreate ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="e7617-128">Préparation de votre application web</span><span class="sxs-lookup"><span data-stu-id="e7617-128">Prepare your web app</span></span>

<span data-ttu-id="e7617-129">toobind une SSL personnalisée de certificats tooyour web app, votre [plan App Service](https://azure.microsoft.com/pricing/details/app-service/) doit être Bonjour **base**, **Standard**, ou **Premium** couche.</span><span class="sxs-lookup"><span data-stu-id="e7617-129">toobind a custom SSL certificate tooyour web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in hello **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="e7617-130">Dans cette étape, vous vous assurer que votre application web est Bonjour pris en charge niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="e7617-130">In this step, you make sure that your web app is in hello supported pricing tier.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="e7617-131">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="e7617-131">Log in tooAzure</span></span>

<span data-ttu-id="e7617-132">Ouvrez hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e7617-132">Open hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-tooyour-web-app"></a><span data-ttu-id="e7617-133">Accédez tooyour l’application web</span><span class="sxs-lookup"><span data-stu-id="e7617-133">Navigate tooyour web app</span></span>

<span data-ttu-id="e7617-134">Dans le menu de gauche hello, cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application web.</span><span class="sxs-lookup"><span data-stu-id="e7617-134">From hello left menu, click **App Services**, and then click hello name of your web app.</span></span>

![Sélectionner de l’application web](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="e7617-136">Vous n’êtes pas pas dans la page de gestion hello de votre application web.</span><span class="sxs-lookup"><span data-stu-id="e7617-136">You have landed in hello management page of your web app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="e7617-137">Vérifier le niveau tarifaire de hello</span><span class="sxs-lookup"><span data-stu-id="e7617-137">Check hello pricing tier</span></span>

<span data-ttu-id="e7617-138">Navigation de gauche hello de page de votre application web, faites défiler toohello **paramètres** section et sélectionnez **montée en puissance (plan App Service)**.</span><span class="sxs-lookup"><span data-stu-id="e7617-138">In hello left-hand navigation of your web app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu Monter en puissance](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="e7617-140">Vérifiez toomake sûr que votre application web n’est pas hello **libre** ou **Shared** couche.</span><span class="sxs-lookup"><span data-stu-id="e7617-140">Check toomake sure that your web app is not in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="e7617-141">Le niveau actuel de votre application web est encadré d’un rectangle bleu foncé.</span><span class="sxs-lookup"><span data-stu-id="e7617-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Vérification du niveau de tarification](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="e7617-143">SSL personnalisé n’est pas pris en charge dans hello **libre** ou **Shared** couche.</span><span class="sxs-lookup"><span data-stu-id="e7617-143">Custom SSL is not supported in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="e7617-144">Si vous avez besoin tooscale, suivez les étapes de hello dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="e7617-144">If you need tooscale up, follow hello steps in hello next section.</span></span> <span data-ttu-id="e7617-145">Sinon, fermez hello **choisir votre niveau tarifaire** page et ignorer trop[télécharger et de lier votre certificat SSL](#upload).</span><span class="sxs-lookup"><span data-stu-id="e7617-145">Otherwise, close hello **Choose your pricing tier** page and skip too[Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="e7617-146">Évolution de votre plan App Service</span><span class="sxs-lookup"><span data-stu-id="e7617-146">Scale up your App Service plan</span></span>

<span data-ttu-id="e7617-147">Sélectionnez une des hello **base**, **Standard**, ou **Premium** niveaux.</span><span class="sxs-lookup"><span data-stu-id="e7617-147">Select one of hello **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="e7617-148">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="e7617-148">Click **Select**.</span></span>

![Sélection du niveau tarifaire](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="e7617-150">Lorsque vous voyez hello suivant la notification, l’opération de mise à l’échelle de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="e7617-150">When you see hello following notification, hello scale operation is complete.</span></span>

![Notification de montée en puissance](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="e7617-152">Liaison de votre certificat SSL</span><span class="sxs-lookup"><span data-stu-id="e7617-152">Bind your SSL certificate</span></span>

<span data-ttu-id="e7617-153">Vous est prêt tooupload votre certificat SSL tooyour l’application web.</span><span class="sxs-lookup"><span data-stu-id="e7617-153">You are ready tooupload your SSL certificate tooyour web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="e7617-154">Fusionner les certificats intermédiaires</span><span class="sxs-lookup"><span data-stu-id="e7617-154">Merge intermediate certificates</span></span>

<span data-ttu-id="e7617-155">Si votre autorité de certification vous donne plusieurs certificats dans la chaîne de certificats hello, vous devez les certificats hello toomerge dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="e7617-155">If your certificate authority gives you multiple certificates in hello certificate chain, you need toomerge hello certificates in order.</span></span> 

<span data-ttu-id="e7617-156">toodo cela, ouvrez chaque certificat que vous avez reçu dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="e7617-156">toodo this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="e7617-157">Créer un fichier de certificat fusionné hello, appelé _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="e7617-157">Create a file for hello merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="e7617-158">Dans un éditeur de texte, copiez le contenu de chaque certificat hello dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="e7617-158">In a text editor, copy hello content of each certificate into this file.</span></span> <span data-ttu-id="e7617-159">commande Hello vos certificats doit ressembler à hello suivant le modèle :</span><span class="sxs-lookup"><span data-stu-id="e7617-159">hello order of your certificates should look like hello following template:</span></span>

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a><span data-ttu-id="e7617-160">Exporter le certificat tooPFX</span><span class="sxs-lookup"><span data-stu-id="e7617-160">Export certificate tooPFX</span></span>

<span data-ttu-id="e7617-161">Exporter votre certificat SSL fusionnée avec la clé privée hello votre demande de certificat a été généré avec.</span><span class="sxs-lookup"><span data-stu-id="e7617-161">Export your merged SSL certificate with hello private key that your certificate request was generated with.</span></span>

<span data-ttu-id="e7617-162">Si vous avez généré votre demande de certificat à l’aide d’OpenSSL, vous avez créé un fichier de clé privée.</span><span class="sxs-lookup"><span data-stu-id="e7617-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="e7617-163">tooexport tooPFX votre certificat, exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="e7617-163">tooexport your certificate tooPFX, run hello following command.</span></span> <span data-ttu-id="e7617-164">Remplacez les espaces réservés de hello  _&lt;fichier de clé privée >_ et  _&lt;fusionnée de fichier de certificat >_.</span><span class="sxs-lookup"><span data-stu-id="e7617-164">Replace hello placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="e7617-165">Lorsque vous y êtes invité, définissez un mot de passe d’exportation.</span><span class="sxs-lookup"><span data-stu-id="e7617-165">When prompted, define an export password.</span></span> <span data-ttu-id="e7617-166">Vous allez utiliser ce mot de passe lors du téléchargement de votre tooApp de certificat SSL Service ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="e7617-166">You'll use this password when uploading your SSL certificate tooApp Service later.</span></span>

<span data-ttu-id="e7617-167">Si vous avez utilisé IIS ou _Certreq.exe_ toogenerate votre demande de certificat, l’installation hello certificat tooyour ordinateur local, puis [exporter hello certificat tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="e7617-167">If you used IIS or _Certreq.exe_ toogenerate your certificate request, install hello certificate tooyour local machine, and then [export hello certificate tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="e7617-168">Chargement de votre certificat SSL</span><span class="sxs-lookup"><span data-stu-id="e7617-168">Upload your SSL certificate</span></span>

<span data-ttu-id="e7617-169">tooupload votre certificat SSL, cliquez sur **certificats SSL** Bonjour gauche de navigation de votre application web.</span><span class="sxs-lookup"><span data-stu-id="e7617-169">tooupload your SSL certificate, click **SSL certificates** in hello left navigation of your web app.</span></span>

<span data-ttu-id="e7617-170">Cliquez sur **Charger le certificat**.</span><span class="sxs-lookup"><span data-stu-id="e7617-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="e7617-171">Dans **Fichier de certificat PFX**, sélectionnez votre fichier PFX.</span><span class="sxs-lookup"><span data-stu-id="e7617-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="e7617-172">Dans **mot de passe de certificat**, type hello mot de passe que vous avez créé lorsque vous avez exporté le fichier PFX hello.</span><span class="sxs-lookup"><span data-stu-id="e7617-172">In **Certificate password**, type hello password that you created when you exported hello PFX file.</span></span>

<span data-ttu-id="e7617-173">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="e7617-173">Click **Upload**.</span></span>

![Téléchargement d’un certificat](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="e7617-175">Lorsque le Service de l’application a terminé de télécharger votre certificat, il apparaît dans hello **certificats SSL** page.</span><span class="sxs-lookup"><span data-stu-id="e7617-175">When App Service finishes uploading your certificate, it appears in hello **SSL certificates** page.</span></span>

![Certificat chargé](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="e7617-177">Liaison de votre certificat SSL</span><span class="sxs-lookup"><span data-stu-id="e7617-177">Bind your SSL certificate</span></span>

<span data-ttu-id="e7617-178">Bonjour **liaisons SSL** , cliquez sur **ajouter la liaison**.</span><span class="sxs-lookup"><span data-stu-id="e7617-178">In hello **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="e7617-179">Bonjour **ajouter la liaison SSL** page, utilisez hello menus déroulants tooselect hello domaine nom toosecure et toouse de certificat hello.</span><span class="sxs-lookup"><span data-stu-id="e7617-179">In hello **Add SSL Binding** page, use hello dropdowns tooselect hello domain name toosecure, and hello certificate toouse.</span></span>

> [!NOTE]
> <span data-ttu-id="e7617-180">Si vous avez téléchargé votre certificat, mais ne pas afficher ou les noms de domaine hello Bonjour **nom d’hôte** liste déroulante, essayez d’actualiser la page du navigateur hello.</span><span class="sxs-lookup"><span data-stu-id="e7617-180">If you have uploaded your certificate but don't see hello domain name(s) in hello **Hostname** dropdown, try refreshing hello browser page.</span></span>
>
>

<span data-ttu-id="e7617-181">Dans **SSL Type**, sélectionnez si toouse  **[Indication de nom de serveur (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  ou SSL basé sur IP.</span><span class="sxs-lookup"><span data-stu-id="e7617-181">In **SSL Type**, select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="e7617-182">**SSL basé sur SNI** : plusieurs liaisons SSL basées sur SNI peuvent être ajoutées.</span><span class="sxs-lookup"><span data-stu-id="e7617-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="e7617-183">Cette option permet à plusieurs toosecure de certificats SSL plusieurs domaines sur hello même adresse IP.</span><span class="sxs-lookup"><span data-stu-id="e7617-183">This option allows multiple SSL certificates toosecure multiple domains on hello same IP address.</span></span> <span data-ttu-id="e7617-184">La plupart des navigateurs actuels (y compris Internet Explorer, Chrome, Firefox et Opera) prennent en charge SNI (plus d’informations sur la prise en charge des navigateurs dans [Indication du nom du serveur](http://wikipedia.org/wiki/Server_Name_Indication)).</span><span class="sxs-lookup"><span data-stu-id="e7617-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="e7617-185">**SSL basé sur IP** : une seule liaison SSL basée sur IP peut être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="e7617-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="e7617-186">Cette option ne permet qu’un seul toosecure de certificat SSL à une adresse IP publique dédiée.</span><span class="sxs-lookup"><span data-stu-id="e7617-186">This option allows only one SSL certificate toosecure a dedicated public IP address.</span></span> <span data-ttu-id="e7617-187">toosecure plusieurs domaines, vous devez les sécuriser à l’aide de tous les hello même certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="e7617-187">toosecure multiple domains, you must secure them all using hello same SSL certificate.</span></span> <span data-ttu-id="e7617-188">Il s’agit d’option traditionnelles de hello pour la liaison SSL.</span><span class="sxs-lookup"><span data-stu-id="e7617-188">This is hello traditional option for SSL binding.</span></span>

<span data-ttu-id="e7617-189">Cliquez sur **Ajouter une liaison**.</span><span class="sxs-lookup"><span data-stu-id="e7617-189">Click **Add Binding**.</span></span>

![Liaison d’un certificat SSL](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="e7617-191">Lorsque le Service de l’application a terminé de télécharger votre certificat, il apparaît dans hello **liaisons SSL** sections.</span><span class="sxs-lookup"><span data-stu-id="e7617-191">When App Service finishes uploading your certificate, it appears in hello **SSL bindings** sections.</span></span>

![Certificat lié tooweb application](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="e7617-193">Nouveau mappage d’un enregistrement pour SSL IP</span><span class="sxs-lookup"><span data-stu-id="e7617-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="e7617-194">Si vous n’utilisez pas SSL basé sur IP dans votre application web, passez trop[HTTPS de Test pour votre domaine personnalisé](#test).</span><span class="sxs-lookup"><span data-stu-id="e7617-194">If you don't use IP-based SSL in your web app, skip too[Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="e7617-195">Par défaut, votre application web utilise une adresse IP publique partagée.</span><span class="sxs-lookup"><span data-stu-id="e7617-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="e7617-196">Dès que vous liez un certificat avec SSL basé sur IP, App Service crée une adresse IP dédiée pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="e7617-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="e7617-197">Si vous avez mappé une application web de tooyour enregistrement A, mettre à jour le Registre de votre domaine avec cette nouvelle adresse IP dédiée.</span><span class="sxs-lookup"><span data-stu-id="e7617-197">If you have mapped an A record tooyour web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="e7617-198">De votre application web **un domaine personnalisé** page est mise à jour avec hello dédié, nouvelle adresse.</span><span class="sxs-lookup"><span data-stu-id="e7617-198">Your web app's **Custom domain** page is updated with hello new, dedicated IP address.</span></span> <span data-ttu-id="e7617-199">[Copiez cette adresse IP](app-service-web-tutorial-custom-domain.md#info), puis [remappage hello un enregistrement](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis nouvelle adresse.</span><span class="sxs-lookup"><span data-stu-id="e7617-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap hello A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="e7617-200">Test du protocole HTTPS</span><span class="sxs-lookup"><span data-stu-id="e7617-200">Test HTTPS</span></span>

<span data-ttu-id="e7617-201">Tout ce qui a quitté toodo maintenant est toomake sûr que HTTPS fonctionne pour votre domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="e7617-201">All that's left toodo now is toomake sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="e7617-202">Dans différents navigateurs, recherchez trop`https://<your.custom.domain>` toosee qu’il sert de votre application web.</span><span class="sxs-lookup"><span data-stu-id="e7617-202">In various browsers, browse too`https://<your.custom.domain>` toosee that it serves up your web app.</span></span>

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="e7617-204">Si votre application web permet de voir les erreurs de validation de certificat, vous utilisez probablement un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="e7617-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="e7617-205">Si tel n’est pas le cas de hello, vous pouvez avoir laissé des certificats intermédiaires lorsque vous exportez votre fichier PFX du certificat toohello.</span><span class="sxs-lookup"><span data-stu-id="e7617-205">If that's not hello case, you may have left out intermediate certificates when you export your certificate toohello PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="e7617-206">Appliquer le protocole HTTPS</span><span class="sxs-lookup"><span data-stu-id="e7617-206">Enforce HTTPS</span></span>

<span data-ttu-id="e7617-207">App Service n’appliquant *pas* le protocole HTTPS, tout le monde peut accéder à votre application à l’aide de HTTP.</span><span class="sxs-lookup"><span data-stu-id="e7617-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="e7617-208">tooenforce HTTPS pour votre application web, définissez une règle de réécriture Bonjour _web.config_ fichier de votre application web.</span><span class="sxs-lookup"><span data-stu-id="e7617-208">tooenforce HTTPS for your web app, define a rewrite rule in hello _web.config_ file for your web app.</span></span> <span data-ttu-id="e7617-209">Service de l’application utilise ce fichier, quel que soit l’infrastructure de langage hello de votre application web.</span><span class="sxs-lookup"><span data-stu-id="e7617-209">App Service uses this file, regardless of hello language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="e7617-210">Certaines redirections de requête sont propres au langage.</span><span class="sxs-lookup"><span data-stu-id="e7617-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="e7617-211">ASP.NET MVC peuvent utiliser hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtre au lieu de la règle de réécriture hello dans _web.config_.</span><span class="sxs-lookup"><span data-stu-id="e7617-211">ASP.NET MVC can use hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of hello rewrite rule in _web.config_.</span></span>

<span data-ttu-id="e7617-212">Si vous êtes un développeur .NET, vous connaissez probablement ce fichier.</span><span class="sxs-lookup"><span data-stu-id="e7617-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="e7617-213">Il est dans la racine de hello de votre solution.</span><span class="sxs-lookup"><span data-stu-id="e7617-213">It is in hello root of your solution.</span></span>

<span data-ttu-id="e7617-214">Ou, si vous développez avec PHP, Node.js, Python ou Java, il est possible que ce fichier ait été généré en votre nom dans App Service.</span><span class="sxs-lookup"><span data-stu-id="e7617-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="e7617-215">Connecter le point de terminaison de l’application tooyour web FTP en suivant les instructions de hello sur [déployer votre tooAzure d’application du Service d’applications à l’aide de FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="e7617-215">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="e7617-216">Ce fichier doit se trouver dans _/home/site/wwwroot_.</span><span class="sxs-lookup"><span data-stu-id="e7617-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="e7617-217">Dans le cas contraire, créez un _web.config_ fichier dans ce dossier par hello XML suivant :</span><span class="sxs-lookup"><span data-stu-id="e7617-217">If not, create a _web.config_ file in this folder with hello following XML:</span></span>

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

<span data-ttu-id="e7617-218">Pour un existant _web.config_ de fichiers, copiez hello ensemble `<rule>` élément dans votre _web.config_de `configuration/system.webServer/rewrite/rules` élément.</span><span class="sxs-lookup"><span data-stu-id="e7617-218">For an existing _web.config_ file, copy hello entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="e7617-219">S’il existe d’autres `<rule>` éléments dans votre _web.config_, hello place copié `<rule>` élément avant hello autres `<rule>` éléments.</span><span class="sxs-lookup"><span data-stu-id="e7617-219">If there are other `<rule>` elements in your _web.config_, place hello copied `<rule>` element before hello other `<rule>` elements.</span></span>

<span data-ttu-id="e7617-220">Cette règle retourne un HTTP 301 (redirection permanente) le protocole HTTPS toohello chaque fois que l’utilisateur de hello effectue une demande HTTP tooyour l’application web.</span><span class="sxs-lookup"><span data-stu-id="e7617-220">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="e7617-221">Par exemple, il est redirigé à partir de `http://contoso.com` trop`https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e7617-221">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

<span data-ttu-id="e7617-222">Pour plus d’informations sur le module de réécriture d’URL IIS hello, consultez hello [réécriture d’URL](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span><span class="sxs-lookup"><span data-stu-id="e7617-222">For more information on hello IIS URL Rewrite module, see hello [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="e7617-223">Mettre en œuvre HTTPS pour Web Apps sous Linux</span><span class="sxs-lookup"><span data-stu-id="e7617-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="e7617-224">App Service sous Linux n’appliquant *pas* le protocole HTTPS, tout le monde peut accéder à votre application web à l’aide de HTTP.</span><span class="sxs-lookup"><span data-stu-id="e7617-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="e7617-225">tooenforce HTTPS pour votre application web, définissez une règle de réécriture Bonjour _.htaccess_ fichier de votre application web.</span><span class="sxs-lookup"><span data-stu-id="e7617-225">tooenforce HTTPS for your web app, define a rewrite rule in hello _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="e7617-226">Connecter le point de terminaison de l’application tooyour web FTP en suivant les instructions de hello sur [déployer votre tooAzure d’application du Service d’applications à l’aide de FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="e7617-226">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="e7617-227">Dans _/home/site/wwwroot_, créez un _.htaccess_ fichier avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="e7617-227">In _/home/site/wwwroot_, create an _.htaccess_ file with hello following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="e7617-228">Cette règle retourne un HTTP 301 (redirection permanente) le protocole HTTPS toohello chaque fois que l’utilisateur de hello effectue une demande HTTP tooyour l’application web.</span><span class="sxs-lookup"><span data-stu-id="e7617-228">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="e7617-229">Par exemple, il est redirigé à partir de `http://contoso.com` trop`https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="e7617-229">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="e7617-230">Automatiser des tâches à l’aide de scripts</span><span class="sxs-lookup"><span data-stu-id="e7617-230">Automate with scripts</span></span>

<span data-ttu-id="e7617-231">Vous pouvez automatiser des liaisons SSL pour votre application web avec des scripts, à l’aide de hello [CLI d’Azure](/cli/azure/install-azure-cli) ou [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e7617-231">You can automate SSL bindings for your web app with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="e7617-232">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="e7617-232">Azure CLI</span></span>

<span data-ttu-id="e7617-233">Hello commande suivante télécharge un fichier PFX exporté et obtient l’empreinte numérique hello.</span><span class="sxs-lookup"><span data-stu-id="e7617-233">hello following command uploads an exported PFX file and gets hello thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="e7617-234">Hello commande suivante ajoute une liaison SSL SNI, à l’aide de l’empreinte numérique hello à partir de la commande précédente hello.</span><span class="sxs-lookup"><span data-stu-id="e7617-234">hello following command adds an SNI-based SSL binding, using hello thumbprint from hello previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="e7617-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7617-235">Azure PowerShell</span></span>

<span data-ttu-id="e7617-236">Bonjour commande suivante télécharge un fichier PFX exporté et ajoute une liaison SSL SNI.</span><span class="sxs-lookup"><span data-stu-id="e7617-236">hello following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="e7617-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e7617-237">Next steps</span></span>

<span data-ttu-id="e7617-238">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="e7617-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e7617-239">Mettre à jour le niveau de tarification de votre application</span><span class="sxs-lookup"><span data-stu-id="e7617-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="e7617-240">Lier votre tooApp de certificat SSL Service personnalisé</span><span class="sxs-lookup"><span data-stu-id="e7617-240">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="e7617-241">Appliquer le protocole HTTPS à votre application</span><span class="sxs-lookup"><span data-stu-id="e7617-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="e7617-242">Automatiser la liaison de certificat SSL avec des scripts</span><span class="sxs-lookup"><span data-stu-id="e7617-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="e7617-243">Avancer toolearn de didacticiel suivant toohello comment toouse Azure Content Delivery Network.</span><span class="sxs-lookup"><span data-stu-id="e7617-243">Advance toohello next tutorial toolearn how toouse Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e7617-244">Ajouter un tooan de réseau de distribution de contenu (CDN) Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e7617-244">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
