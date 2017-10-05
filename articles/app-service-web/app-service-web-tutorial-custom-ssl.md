---
title: "Lier un certificat SSL existant à des applications web Azure | Microsoft Docs"
description: "Découvrez comment lier un certificat SSL personnalisé à votre application web, un backend d’application mobile ou une application API dans Azure App Service."
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
ms.openlocfilehash: 15c31ae5451a31dff2df08047ee43e75edacc127
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-to-azure-web-apps"></a><span data-ttu-id="827a0-103">Lier un certificat SSL existant à des applications web Azure</span><span class="sxs-lookup"><span data-stu-id="827a0-103">Bind an existing custom SSL certificate to Azure Web Apps</span></span>

<span data-ttu-id="827a0-104">Azure Web Apps fournit un service d’hébergement hautement évolutif et appliquant des mises à jour correctives automatiquement.</span><span class="sxs-lookup"><span data-stu-id="827a0-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="827a0-105">Ce didacticiel vous montre comment lier un certificat SSL personnalisé acheté auprès d’une autorité de certification approuvée pour [Azure Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="827a0-105">This tutorial shows you how to bind a custom SSL certificate that you purchased from a trusted certificate authority to [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="827a0-106">Lorsque vous aurez terminé, vous serez en mesure d’accéder à votre application web au niveau du point de terminaison HTTPS de votre domaine DNS personnalisé.</span><span class="sxs-lookup"><span data-stu-id="827a0-106">When you're finished, you'll be able to access your web app at the HTTPS endpoint of your custom DNS domain.</span></span>

![Application Web avec certificat SSL personnalisé](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="827a0-108">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="827a0-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="827a0-109">Mettre à jour le niveau de tarification de votre application</span><span class="sxs-lookup"><span data-stu-id="827a0-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="827a0-110">Lier votre certificat SSL personnalisé à App Service</span><span class="sxs-lookup"><span data-stu-id="827a0-110">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="827a0-111">Appliquer le protocole HTTPS à votre application</span><span class="sxs-lookup"><span data-stu-id="827a0-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="827a0-112">Automatiser la liaison de certificat SSL avec des scripts</span><span class="sxs-lookup"><span data-stu-id="827a0-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="827a0-113">Si vous avez besoin d’un certificat SSL personnalisé, vous pouvez en obtenir un directement dans le portail Azure et le lier à votre application web.</span><span class="sxs-lookup"><span data-stu-id="827a0-113">If you need to get a custom SSL certificate, you can get one in the Azure portal directly and bind it to your web app.</span></span> <span data-ttu-id="827a0-114">Suivez le [didacticiel Certificats App Service](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="827a0-114">Follow the [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="827a0-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="827a0-115">Prerequisites</span></span>

<span data-ttu-id="827a0-116">Pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="827a0-116">To complete this tutorial:</span></span>

- [<span data-ttu-id="827a0-117">Création d’une application App Service</span><span class="sxs-lookup"><span data-stu-id="827a0-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="827a0-118">Mappage d’un nom DNS personnalisé à une application web</span><span class="sxs-lookup"><span data-stu-id="827a0-118">Map a custom DNS name to your web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="827a0-119">Acquisition d’un certificat SSL auprès d’une autorité de certification approuvée</span><span class="sxs-lookup"><span data-stu-id="827a0-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="827a0-120">Conditions requises pour le certificat SSL</span><span class="sxs-lookup"><span data-stu-id="827a0-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="827a0-121">Pour l’utiliser dans App Service, un certificat doit remplir toutes les conditions suivantes :</span><span class="sxs-lookup"><span data-stu-id="827a0-121">To use a certificate in App Service, the certificate must meet all the following requirements:</span></span>

* <span data-ttu-id="827a0-122">Être signé par une autorité de certification approuvée</span><span class="sxs-lookup"><span data-stu-id="827a0-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="827a0-123">Être exporté sous la forme d’un fichier PFX protégé par mot de passe</span><span class="sxs-lookup"><span data-stu-id="827a0-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="827a0-124">Contenir une clé privée d’au moins 2048 bits de long</span><span class="sxs-lookup"><span data-stu-id="827a0-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="827a0-125">Contenir tous les certificats intermédiaires dans la chaîne de certificats</span><span class="sxs-lookup"><span data-stu-id="827a0-125">Contains all intermediate certificates in the certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="827a0-126">Les **certificats de chiffrement à courbe elliptique (ECC)** sont compatibles avec App Service, mais ce sujet sort du cadre de cet article.</span><span class="sxs-lookup"><span data-stu-id="827a0-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="827a0-127">Consultez votre autorité de certification sur les étapes à suivre pour créer des certificats ECC.</span><span class="sxs-lookup"><span data-stu-id="827a0-127">Work with your certificate authority on the exact steps to create ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="827a0-128">Préparation de votre application web</span><span class="sxs-lookup"><span data-stu-id="827a0-128">Prepare your web app</span></span>

<span data-ttu-id="827a0-129">Pour lier un certificat SSL personnalisé à votre application web, votre [plan App Service](https://azure.microsoft.com/pricing/details/app-service/) doit se trouver dans le niveau **De base**, **Standard** ou **Premium**.</span><span class="sxs-lookup"><span data-stu-id="827a0-129">To bind a custom SSL certificate to your web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in the **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="827a0-130">Au cours de cette étape, vous allez vous assurer que votre application web se trouve dans le niveau de tarification pris en charge.</span><span class="sxs-lookup"><span data-stu-id="827a0-130">In this step, you make sure that your web app is in the supported pricing tier.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="827a0-131">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="827a0-131">Log in to Azure</span></span>

<span data-ttu-id="827a0-132">Ouvrez le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="827a0-132">Open the [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-to-your-web-app"></a><span data-ttu-id="827a0-133">Accès à votre application web</span><span class="sxs-lookup"><span data-stu-id="827a0-133">Navigate to your web app</span></span>

<span data-ttu-id="827a0-134">Dans le menu de gauche, cliquez sur **App Services** puis sur le nom de votre application web.</span><span class="sxs-lookup"><span data-stu-id="827a0-134">From the left menu, click **App Services**, and then click the name of your web app.</span></span>

![Sélectionner de l’application web](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="827a0-136">Vous accédez à la page de gestion de votre application web.</span><span class="sxs-lookup"><span data-stu-id="827a0-136">You have landed in the management page of your web app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="827a0-137">Vérification du niveau tarifaire</span><span class="sxs-lookup"><span data-stu-id="827a0-137">Check the pricing tier</span></span>

<span data-ttu-id="827a0-138">Dans la navigation de gauche de la page de votre application web, accédez à la section **Paramètres** et sélectionnez **Monter en puissance (plan App Service)**.</span><span class="sxs-lookup"><span data-stu-id="827a0-138">In the left-hand navigation of your web app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu Monter en puissance](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="827a0-140">Vérifiez que votre application ne se trouve pas dans le niveau **Gratuit** ou **Partagé**.</span><span class="sxs-lookup"><span data-stu-id="827a0-140">Check to make sure that your web app is not in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="827a0-141">Le niveau actuel de votre application web est encadré d’un rectangle bleu foncé.</span><span class="sxs-lookup"><span data-stu-id="827a0-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Vérification du niveau de tarification](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="827a0-143">Le SSL personnalisé n’est pas pris en charge aux niveaux **Gratuit** et **Partagé**.</span><span class="sxs-lookup"><span data-stu-id="827a0-143">Custom SSL is not supported in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="827a0-144">Si vous avez besoin de monter en puissance, consultez la section ci-après.</span><span class="sxs-lookup"><span data-stu-id="827a0-144">If you need to scale up, follow the steps in the next section.</span></span> <span data-ttu-id="827a0-145">Sinon, fermez la page **Choisir votre niveau de tarification** et passez à [Charger et lier votre certificat SSL](#upload).</span><span class="sxs-lookup"><span data-stu-id="827a0-145">Otherwise, close the **Choose your pricing tier** page and skip to [Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="827a0-146">Évolution de votre plan App Service</span><span class="sxs-lookup"><span data-stu-id="827a0-146">Scale up your App Service plan</span></span>

<span data-ttu-id="827a0-147">Sélectionnez l’un des niveaux **De base**, **Standard** ou **Premium**.</span><span class="sxs-lookup"><span data-stu-id="827a0-147">Select one of the **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="827a0-148">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="827a0-148">Click **Select**.</span></span>

![Sélection du niveau tarifaire](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="827a0-150">Lorsque la notification suivante s’affiche, cela signifie que la montée en charge est terminée.</span><span class="sxs-lookup"><span data-stu-id="827a0-150">When you see the following notification, the scale operation is complete.</span></span>

![Notification de montée en puissance](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="827a0-152">Liaison de votre certificat SSL</span><span class="sxs-lookup"><span data-stu-id="827a0-152">Bind your SSL certificate</span></span>

<span data-ttu-id="827a0-153">Vous êtes prêt à charger votre certificat SSL dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="827a0-153">You are ready to upload your SSL certificate to your web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="827a0-154">Fusionner les certificats intermédiaires</span><span class="sxs-lookup"><span data-stu-id="827a0-154">Merge intermediate certificates</span></span>

<span data-ttu-id="827a0-155">Si votre autorité de certification vous donne plusieurs certificats dans la chaîne, vous devez les fusionner dans l’ordre.</span><span class="sxs-lookup"><span data-stu-id="827a0-155">If your certificate authority gives you multiple certificates in the certificate chain, you need to merge the certificates in order.</span></span> 

<span data-ttu-id="827a0-156">Pour ce faire, ouvrez chaque certificat reçu dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="827a0-156">To do this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="827a0-157">Créez un fichier pour le certificat fusionné, appelé _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="827a0-157">Create a file for the merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="827a0-158">Dans un éditeur de texte, copiez le contenu de chaque certificat dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="827a0-158">In a text editor, copy the content of each certificate into this file.</span></span> <span data-ttu-id="827a0-159">L’ordre de vos certificats doit être conforme au modèle suivant :</span><span class="sxs-lookup"><span data-stu-id="827a0-159">The order of your certificates should look like the following template:</span></span>

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

### <a name="export-certificate-to-pfx"></a><span data-ttu-id="827a0-160">Exportation du certificat vers PFX</span><span class="sxs-lookup"><span data-stu-id="827a0-160">Export certificate to PFX</span></span>

<span data-ttu-id="827a0-161">Exportez votre certificat SSL fusionné avec la clé privée ayant servi à générer votre demande de certificat.</span><span class="sxs-lookup"><span data-stu-id="827a0-161">Export your merged SSL certificate with the private key that your certificate request was generated with.</span></span>

<span data-ttu-id="827a0-162">Si vous avez généré votre demande de certificat à l’aide d’OpenSSL, vous avez créé un fichier de clé privée.</span><span class="sxs-lookup"><span data-stu-id="827a0-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="827a0-163">Pour exporter votre certificat au format PFX, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="827a0-163">To export your certificate to PFX, run the following command.</span></span> <span data-ttu-id="827a0-164">Remplacez les espaces réservés _&lt;private-key-file>_ et  _&lt;merged-certificate-file>_.</span><span class="sxs-lookup"><span data-stu-id="827a0-164">Replace the placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="827a0-165">Lorsque vous y êtes invité, définissez un mot de passe d’exportation.</span><span class="sxs-lookup"><span data-stu-id="827a0-165">When prompted, define an export password.</span></span> <span data-ttu-id="827a0-166">Vous allez utiliser ce mot de passe lors du chargement de votre certificat SSL dans App Service.</span><span class="sxs-lookup"><span data-stu-id="827a0-166">You'll use this password when uploading your SSL certificate to App Service later.</span></span>

<span data-ttu-id="827a0-167">Si vous avez utilisé IIS ou _Certreq.exe_ pour générer votre demande de certificat, installez le certificat sur votre ordinateur local, puis [exportez le certificat au format PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="827a0-167">If you used IIS or _Certreq.exe_ to generate your certificate request, install the certificate to your local machine, and then [export the certificate to PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="827a0-168">Chargement de votre certificat SSL</span><span class="sxs-lookup"><span data-stu-id="827a0-168">Upload your SSL certificate</span></span>

<span data-ttu-id="827a0-169">Pour charger votre certificat SSL, cliquez sur **Certificats SSL** dans le volet de navigation gauche de votre application web.</span><span class="sxs-lookup"><span data-stu-id="827a0-169">To upload your SSL certificate, click **SSL certificates** in the left navigation of your web app.</span></span>

<span data-ttu-id="827a0-170">Cliquez sur **Charger le certificat**.</span><span class="sxs-lookup"><span data-stu-id="827a0-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="827a0-171">Dans **Fichier de certificat PFX**, sélectionnez votre fichier PFX.</span><span class="sxs-lookup"><span data-stu-id="827a0-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="827a0-172">Dans **Mot de passe du certificat**, tapez le mot de passe que vous avez créé lors de l’exportation du fichier PFX.</span><span class="sxs-lookup"><span data-stu-id="827a0-172">In **Certificate password**, type the password that you created when you exported the PFX file.</span></span>

<span data-ttu-id="827a0-173">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="827a0-173">Click **Upload**.</span></span>

![Téléchargement d’un certificat](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="827a0-175">Lorsque App Service finit de charger votre certificat, celui-ci apparaît dans la page **Certificats SSL**.</span><span class="sxs-lookup"><span data-stu-id="827a0-175">When App Service finishes uploading your certificate, it appears in the **SSL certificates** page.</span></span>

![Certificat chargé](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="827a0-177">Liaison de votre certificat SSL</span><span class="sxs-lookup"><span data-stu-id="827a0-177">Bind your SSL certificate</span></span>

<span data-ttu-id="827a0-178">Dans la section **Liaisons SSL**, cliquez sur **Ajouter une liaison**.</span><span class="sxs-lookup"><span data-stu-id="827a0-178">In the **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="827a0-179">Dans la page **Ajouter une liaison SSL**, utilisez les listes déroulantes pour sélectionner le nom de domaine à sécuriser et le certificat à utiliser.</span><span class="sxs-lookup"><span data-stu-id="827a0-179">In the **Add SSL Binding** page, use the dropdowns to select the domain name to secure, and the certificate to use.</span></span>

> [!NOTE]
> <span data-ttu-id="827a0-180">Si vous avez chargé votre certificat mais que vous ne voyez pas le ou les noms de domaine dans la liste déroulante **Nom d’hôte**, essayez d’actualiser la page du navigateur.</span><span class="sxs-lookup"><span data-stu-id="827a0-180">If you have uploaded your certificate but don't see the domain name(s) in the **Hostname** dropdown, try refreshing the browser page.</span></span>
>
>

<span data-ttu-id="827a0-181">Dans **Type SSL**, choisissez d’utiliser **[l’indication du nom du serveur (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** ou le protocole SSL basé sur IP.</span><span class="sxs-lookup"><span data-stu-id="827a0-181">In **SSL Type**, select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="827a0-182">**SSL basé sur SNI** : plusieurs liaisons SSL basées sur SNI peuvent être ajoutées.</span><span class="sxs-lookup"><span data-stu-id="827a0-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="827a0-183">Cette option permet de sécuriser plusieurs domaines sur la même adresse IP avec plusieurs certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="827a0-183">This option allows multiple SSL certificates to secure multiple domains on the same IP address.</span></span> <span data-ttu-id="827a0-184">La plupart des navigateurs actuels (y compris Internet Explorer, Chrome, Firefox et Opera) prennent en charge SNI (plus d’informations sur la prise en charge des navigateurs dans [Indication du nom du serveur](http://wikipedia.org/wiki/Server_Name_Indication)).</span><span class="sxs-lookup"><span data-stu-id="827a0-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="827a0-185">**SSL basé sur IP** : une seule liaison SSL basée sur IP peut être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="827a0-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="827a0-186">Cette option permet de sécuriser une adresse IP publique dédiée avec un seul certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="827a0-186">This option allows only one SSL certificate to secure a dedicated public IP address.</span></span> <span data-ttu-id="827a0-187">Pour sécuriser plusieurs domaines, vous devez tous les sécuriser en utilisant le même certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="827a0-187">To secure multiple domains, you must secure them all using the same SSL certificate.</span></span> <span data-ttu-id="827a0-188">Cette option est sélectionnée par défaut pour la liaison SSL.</span><span class="sxs-lookup"><span data-stu-id="827a0-188">This is the traditional option for SSL binding.</span></span>

<span data-ttu-id="827a0-189">Cliquez sur **Ajouter une liaison**.</span><span class="sxs-lookup"><span data-stu-id="827a0-189">Click **Add Binding**.</span></span>

![Liaison d’un certificat SSL](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="827a0-191">Lorsque App Service finit de charger votre certificat, celui-ci apparaît dans les sections **Liaisons SSL**.</span><span class="sxs-lookup"><span data-stu-id="827a0-191">When App Service finishes uploading your certificate, it appears in the **SSL bindings** sections.</span></span>

![Certificat lié à une application web](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="827a0-193">Nouveau mappage d’un enregistrement pour SSL IP</span><span class="sxs-lookup"><span data-stu-id="827a0-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="827a0-194">Si vous n’utilisez pas un SSL basé sur IP dans votre application web, passez à [Tester HTTPS pour votre domaine personnalisé](#test).</span><span class="sxs-lookup"><span data-stu-id="827a0-194">If you don't use IP-based SSL in your web app, skip to [Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="827a0-195">Par défaut, votre application web utilise une adresse IP publique partagée.</span><span class="sxs-lookup"><span data-stu-id="827a0-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="827a0-196">Dès que vous liez un certificat avec SSL basé sur IP, App Service crée une adresse IP dédiée pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="827a0-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="827a0-197">Si vous avez mappé un enregistrement A à votre application web, mettez à jour le registre de domaine avec cette nouvelle adresse IP dédiée.</span><span class="sxs-lookup"><span data-stu-id="827a0-197">If you have mapped an A record to your web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="827a0-198">La page **Domaine personnalisé** de votre application web est mise à jour avec la nouvelle adresse IP dédiée.</span><span class="sxs-lookup"><span data-stu-id="827a0-198">Your web app's **Custom domain** page is updated with the new, dedicated IP address.</span></span> <span data-ttu-id="827a0-199">[Copiez cette adresse IP](app-service-web-tutorial-custom-domain.md#info), puis [mappez à nouveau l’enregistrement A](app-service-web-tutorial-custom-domain.md#map-an-a-record) à cette nouvelle adresse IP.</span><span class="sxs-lookup"><span data-stu-id="827a0-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap the A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) to this new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="827a0-200">Test du protocole HTTPS</span><span class="sxs-lookup"><span data-stu-id="827a0-200">Test HTTPS</span></span>

<span data-ttu-id="827a0-201">Il ne reste plus maintenant qu’à vous assurer que HTTPS fonctionne pour votre domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="827a0-201">All that's left to do now is to make sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="827a0-202">Dans différents navigateurs, accédez à `https://<your.custom.domain>` pour vérifier qu’il fournit votre application web.</span><span class="sxs-lookup"><span data-stu-id="827a0-202">In various browsers, browse to `https://<your.custom.domain>` to see that it serves up your web app.</span></span>

![Navigation au sein du portail pour accéder à l’application Azure](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="827a0-204">Si votre application web permet de voir les erreurs de validation de certificat, vous utilisez probablement un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="827a0-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="827a0-205">Si ce n’est pas le cas, vous pouvez avoir oublié des certificats intermédiaires lorsque vous avez exporté votre certificat vers le fichier PFX.</span><span class="sxs-lookup"><span data-stu-id="827a0-205">If that's not the case, you may have left out intermediate certificates when you export your certificate to the PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="827a0-206">Appliquer le protocole HTTPS</span><span class="sxs-lookup"><span data-stu-id="827a0-206">Enforce HTTPS</span></span>

<span data-ttu-id="827a0-207">App Service n’appliquant *pas* le protocole HTTPS, tout le monde peut accéder à votre application à l’aide de HTTP.</span><span class="sxs-lookup"><span data-stu-id="827a0-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="827a0-208">Pour appliquer HTTPS à votre application web, définissez une règle de réécriture dans le fichier _web.config_ de votre application web.</span><span class="sxs-lookup"><span data-stu-id="827a0-208">To enforce HTTPS for your web app, define a rewrite rule in the _web.config_ file for your web app.</span></span> <span data-ttu-id="827a0-209">App Service utilise ce fichier, quelle que soit l’infrastructure de langage de votre application web.</span><span class="sxs-lookup"><span data-stu-id="827a0-209">App Service uses this file, regardless of the language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="827a0-210">Certaines redirections de requête sont propres au langage.</span><span class="sxs-lookup"><span data-stu-id="827a0-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="827a0-211">ASP.NET MVC peut utiliser le filtre [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) au lieu de la règle de réécriture dans le fichier _web.config_.</span><span class="sxs-lookup"><span data-stu-id="827a0-211">ASP.NET MVC can use the [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of the rewrite rule in _web.config_.</span></span>

<span data-ttu-id="827a0-212">Si vous êtes un développeur .NET, vous connaissez probablement ce fichier.</span><span class="sxs-lookup"><span data-stu-id="827a0-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="827a0-213">Il se trouve à la racine de votre solution.</span><span class="sxs-lookup"><span data-stu-id="827a0-213">It is in the root of your solution.</span></span>

<span data-ttu-id="827a0-214">Ou, si vous développez avec PHP, Node.js, Python ou Java, il est possible que ce fichier ait été généré en votre nom dans App Service.</span><span class="sxs-lookup"><span data-stu-id="827a0-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="827a0-215">Connectez-vous au point de terminaison FTP de votre application web en suivant les instructions fournies dans [Déployer votre application dans Azure App Service avec FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="827a0-215">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="827a0-216">Ce fichier doit se trouver dans _/home/site/wwwroot_.</span><span class="sxs-lookup"><span data-stu-id="827a0-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="827a0-217">Dans le cas contraire, créez un fichier _web.config_ dans ce dossier avec le code XML suivant :</span><span class="sxs-lookup"><span data-stu-id="827a0-217">If not, create a _web.config_ file in this folder with the following XML:</span></span>

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

<span data-ttu-id="827a0-218">Pour un fichier _web.config_ existant, copiez l’intégralité de l’élément `<rule>` dans l’élément `configuration/system.webServer/rewrite/rules` de votre fichier _web.config_.</span><span class="sxs-lookup"><span data-stu-id="827a0-218">For an existing _web.config_ file, copy the entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="827a0-219">Si d’autres éléments `<rule>` sont présents dans votre fichier _web.config`<rule>`, placez_  avant les autres éléments `<rule>`.</span><span class="sxs-lookup"><span data-stu-id="827a0-219">If there are other `<rule>` elements in your _web.config_, place the copied `<rule>` element before the other `<rule>` elements.</span></span>

<span data-ttu-id="827a0-220">Cette règle renvoie un HTTP 301 (redirection permanente) vers le protocole HTTPS chaque fois que l’utilisateur envoie une requête HTTP à votre application web.</span><span class="sxs-lookup"><span data-stu-id="827a0-220">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="827a0-221">Par exemple, elle redirige de `http://contoso.com` vers `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="827a0-221">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

<span data-ttu-id="827a0-222">Pour plus d'informations sur le module Réécriture d'URL d'IIS, consultez la documentation sur la [Réécriture d'URL](http://www.iis.net/downloads/microsoft/url-rewrite) .</span><span class="sxs-lookup"><span data-stu-id="827a0-222">For more information on the IIS URL Rewrite module, see the [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="827a0-223">Mettre en œuvre HTTPS pour Web Apps sous Linux</span><span class="sxs-lookup"><span data-stu-id="827a0-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="827a0-224">App Service sous Linux n’appliquant *pas* le protocole HTTPS, tout le monde peut accéder à votre application web à l’aide de HTTP.</span><span class="sxs-lookup"><span data-stu-id="827a0-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="827a0-225">Pour appliquer HTTPS à votre application web, définissez une règle de réécriture dans le fichier _.htaccess_ de votre application web.</span><span class="sxs-lookup"><span data-stu-id="827a0-225">To enforce HTTPS for your web app, define a rewrite rule in the _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="827a0-226">Connectez-vous au point de terminaison FTP de votre application web en suivant les instructions fournies dans [Déployer votre application dans Azure App Service avec FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="827a0-226">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="827a0-227">Dans _/home/site/wwwroot_, créez un fichier _.htaccess_ avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="827a0-227">In _/home/site/wwwroot_, create an _.htaccess_ file with the following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="827a0-228">Cette règle renvoie un HTTP 301 (redirection permanente) vers le protocole HTTPS chaque fois que l’utilisateur envoie une requête HTTP à votre application web.</span><span class="sxs-lookup"><span data-stu-id="827a0-228">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="827a0-229">Par exemple, elle redirige de `http://contoso.com` vers `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="827a0-229">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="827a0-230">Automatisation à l’aide de scripts</span><span class="sxs-lookup"><span data-stu-id="827a0-230">Automate with scripts</span></span>

<span data-ttu-id="827a0-231">Vous pouvez automatiser les liaisons SSL de votre application web à l’aide de scripts, en utilisant [Azure CLI](/cli/azure/install-azure-cli) ou [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="827a0-231">You can automate SSL bindings for your web app with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="827a0-232">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="827a0-232">Azure CLI</span></span>

<span data-ttu-id="827a0-233">La commande suivante charge un fichier PFX exporté et obtient l’empreinte.</span><span class="sxs-lookup"><span data-stu-id="827a0-233">The following command uploads an exported PFX file and gets the thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="827a0-234">La commande suivante ajoute une liaison SSL basée sur SNI à l’aide de l’empreinte de la commande précédente.</span><span class="sxs-lookup"><span data-stu-id="827a0-234">The following command adds an SNI-based SSL binding, using the thumbprint from the previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="827a0-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="827a0-235">Azure PowerShell</span></span>

<span data-ttu-id="827a0-236">La commande suivante charge un fichier PFX exporté et ajoute une liaison SSL basée sur SNI.</span><span class="sxs-lookup"><span data-stu-id="827a0-236">The following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="827a0-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="827a0-237">Next steps</span></span>

<span data-ttu-id="827a0-238">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="827a0-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="827a0-239">Mettre à jour le niveau de tarification de votre application</span><span class="sxs-lookup"><span data-stu-id="827a0-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="827a0-240">Lier votre certificat SSL personnalisé à App Service</span><span class="sxs-lookup"><span data-stu-id="827a0-240">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="827a0-241">Appliquer le protocole HTTPS à votre application</span><span class="sxs-lookup"><span data-stu-id="827a0-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="827a0-242">Automatiser la liaison de certificat SSL avec des scripts</span><span class="sxs-lookup"><span data-stu-id="827a0-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="827a0-243">Passez au didacticiel suivant pour découvrir comment utiliser un réseau de distribution de contenu Azure.</span><span class="sxs-lookup"><span data-stu-id="827a0-243">Advance to the next tutorial to learn how to use Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="827a0-244">Ajouter un réseau de distribution de contenu (CDN) à un Azure App Service</span><span class="sxs-lookup"><span data-stu-id="827a0-244">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
