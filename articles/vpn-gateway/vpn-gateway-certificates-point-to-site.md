---
title: "Générer et exporter des certificats pour les connexions de point à site : PowerShell : Azure | Microsoft Docs"
description: "Cet article contient les étapes toocreate un certificat racine auto-signé, exporter la clé publique de hello et générer des certificats de client à l’aide de PowerShell sur Windows 10."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 27b99f7c-50dc-4f88-8a6e-d60080819a43
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 11dda015368cda5ce9799fcc4f01d7c542b84fe8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-and-export-certificates-for-point-to-site-connections-using-powershell-on-windows-10"></a><span data-ttu-id="e33fe-103">Générer et exporter des certificats pour les connexions de point à site à l’aide de PowerShell sur Windows 10</span><span class="sxs-lookup"><span data-stu-id="e33fe-103">Generate and export certificates for Point-to-Site connections using PowerShell on Windows 10</span></span>

<span data-ttu-id="e33fe-104">Connexions de point-to-Site utilisent des certificats tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="e33fe-104">Point-to-Site connections use certificates tooauthenticate.</span></span> <span data-ttu-id="e33fe-105">Cet article vous montre comment toocreate un auto-signé certificat racine et générer des certificats de client à l’aide de PowerShell sur Windows 10.</span><span class="sxs-lookup"><span data-stu-id="e33fe-105">This article shows you how toocreate a self-signed root certificate and generate client certificates using PowerShell on Windows 10.</span></span> <span data-ttu-id="e33fe-106">Si vous recherchez des étapes de configuration de Point-to-Site, telles que comment la liste de certificats racines de tooupload, sélectionnez un des articles hello ' configurer Point-to-Site' à partir de hello suivant :</span><span class="sxs-lookup"><span data-stu-id="e33fe-106">If you are looking for Point-to-Site configuration steps, such as how tooupload root certificates, select one of hello 'Configure Point-to-Site' articles from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e33fe-107">Création de certificat auto-signés - PowerShell</span><span class="sxs-lookup"><span data-stu-id="e33fe-107">Create self-signed certificates - PowerShell</span></span>](vpn-gateway-certificates-point-to-site.md)
> * [<span data-ttu-id="e33fe-108">Création de certificat auto-signés - Makecert</span><span class="sxs-lookup"><span data-stu-id="e33fe-108">Create self-signed certificates - MakeCert</span></span>](vpn-gateway-certificates-point-to-site-makecert.md)
> * [<span data-ttu-id="e33fe-109">Configuration d’une connexion de point à site à un réseau virtuel - Resource Manager - Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e33fe-109">Configure Point-to-Site - Resource Manager - Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="e33fe-110">Configuration d’une connexion point à site à un réseau virtuel - Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="e33fe-110">Configure Point-to-Site - Resource Manager - PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="e33fe-111">Configuration d’une connexion de point à site à un réseau virtuel - Classic - Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e33fe-111">Configure Point-to-Site - Classic - Azure portal</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
> 
> 


<span data-ttu-id="e33fe-112">Vous devez effectuer les étapes de hello dans cet article sur un ordinateur exécutant Windows 10.</span><span class="sxs-lookup"><span data-stu-id="e33fe-112">You must perform hello steps in this article on a computer running Windows 10.</span></span> <span data-ttu-id="e33fe-113">applets de commande PowerShell Hello que vous utilisez des certificats de toogenerate font partie du système d’exploitation de hello Windows 10 et ne fonctionnent pas sur d’autres versions de Windows.</span><span class="sxs-lookup"><span data-stu-id="e33fe-113">hello PowerShell cmdlets that you use toogenerate certificates are part of hello Windows 10 operating system and do not work on other versions of Windows.</span></span> <span data-ttu-id="e33fe-114">l’ordinateur Hello Windows 10 est uniquement les certificats nécessaires toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="e33fe-114">hello Windows 10 computer is only needed toogenerate hello certificates.</span></span> <span data-ttu-id="e33fe-115">Une fois les certificats hello sont générées, vous pouvez les télécharger ou les installer sur n’importe quel système d’exploitation client pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e33fe-115">Once hello certificates are generated, you can upload them, or install them on any supported client operating system.</span></span> 

<span data-ttu-id="e33fe-116">Si vous n’avez pas l’ordinateur d’accès tooa Windows 10, vous pouvez utiliser [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificats.</span><span class="sxs-lookup"><span data-stu-id="e33fe-116">If you do not have access tooa Windows 10 computer, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md) toogenerate certificates.</span></span> <span data-ttu-id="e33fe-117">Hello certificats que vous avez généré à l’aide de ces deux méthodes peuvent être installés sur n’importe quel [pris en charge](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) système d’exploitation client.</span><span class="sxs-lookup"><span data-stu-id="e33fe-117">hello certificates that you generate using either method can be installed on any [supported](vpn-gateway-howto-point-to-site-resource-manager-portal.md#faq) client operating system.</span></span>

## <span data-ttu-id="e33fe-118"><a name="rootcert"></a>Créer un certificat racine auto-signé</span><span class="sxs-lookup"><span data-stu-id="e33fe-118"><a name="rootcert"></a>Create a self-signed root certificate</span></span>

<span data-ttu-id="e33fe-119">Utilisez toocreate d’applet de commande New-SelfSignedCertificate hello un certificat racine auto-signé.</span><span class="sxs-lookup"><span data-stu-id="e33fe-119">Use hello New-SelfSignedCertificate cmdlet toocreate a self-signed root certificate.</span></span> <span data-ttu-id="e33fe-120">Pour obtenir des informations sur des paramètres supplémentaires, consultez [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="e33fe-120">For additional parameter information, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

1. <span data-ttu-id="e33fe-121">Sur un ordinateur sous Windows 10, ouvrez une console Windows PowerShell avec élévation de privilèges.</span><span class="sxs-lookup"><span data-stu-id="e33fe-121">From a computer running Windows 10, open a Windows PowerShell console with elevated privileges.</span></span>
2. <span data-ttu-id="e33fe-122">Utilisez hello suivant le certificat racine auto-signé d’exemple toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="e33fe-122">Use hello following example toocreate hello self-signed root certificate.</span></span> <span data-ttu-id="e33fe-123">Hello exemple suivant crée un certificat racine auto-signé nommé « P2SRootCert » qui est installé automatiquement dans « Volet actuel de certificats ».</span><span class="sxs-lookup"><span data-stu-id="e33fe-123">hello following example creates a self-signed root certificate named 'P2SRootCert' that is automatically installed in 'Certificates-Current User\Personal\Certificates'.</span></span> <span data-ttu-id="e33fe-124">Vous pouvez afficher le certificat de hello en ouvrant *certmgr.msc*, ou *gérer des certificats utilisateur*.</span><span class="sxs-lookup"><span data-stu-id="e33fe-124">You can view hello certificate by opening *certmgr.msc*, or *Manage User Certificates*.</span></span>

  ```powershell
  $cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign
  ```

### <span data-ttu-id="e33fe-125"><a name="cer"></a>Exporter la clé publique de hello (.cer)</span><span class="sxs-lookup"><span data-stu-id="e33fe-125"><a name="cer"></a>Export hello public key (.cer)</span></span>

[!INCLUDE [Export public key](../../includes/vpn-gateway-certificates-export-public-key-include.md)]

<span data-ttu-id="e33fe-126">fichier de exported.cer Hello doit être téléchargé tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e33fe-126">hello exported.cer file must be uploaded tooAzure.</span></span> <span data-ttu-id="e33fe-127">Pour obtenir des instructions, consultez [Configurer une connexion de point à site](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span><span class="sxs-lookup"><span data-stu-id="e33fe-127">For instructions, see [Configure a Point-to-Site connection](vpn-gateway-howto-point-to-site-rm-ps.md#upload).</span></span> <span data-ttu-id="e33fe-128">tooadd un certificat racine de confiance supplémentaires, [cette section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) d’article de hello.</span><span class="sxs-lookup"><span data-stu-id="e33fe-128">tooadd an additional trusted root certificate, [this section](vpn-gateway-howto-point-to-site-rm-ps.md#addremovecert) of hello article.</span></span>

### <a name="export-hello-self-signed-root-certificate-and-public-key-toostore-it-optional"></a><span data-ttu-id="e33fe-129">Exporter le certificat racine auto-signé de hello et toostore de clé publique il (facultatif)</span><span class="sxs-lookup"><span data-stu-id="e33fe-129">Export hello self-signed root certificate and public key toostore it (optional)</span></span>

<span data-ttu-id="e33fe-130">Vous souhaiterez peut-être tooexport hello racine certificat auto-signé et stocker en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="e33fe-130">You may want tooexport hello self-signed root certificate and store it safely.</span></span> <span data-ttu-id="e33fe-131">Si besoin est, vous pouvez l’installer ultérieurement sur un autre ordinateur et générer davantage de certificats clients ou exporter un autre fichier .cer.</span><span class="sxs-lookup"><span data-stu-id="e33fe-131">If need be, you can later install it on another computer and generate more client certificates, or export another .cer file.</span></span> <span data-ttu-id="e33fe-132">tooexport hello auto-signé certificat racine un .pfx, le certificat racine de hello select et l’utilisation hello mêmes étapes comme décrit dans [exporter un certificat client](#clientexport).</span><span class="sxs-lookup"><span data-stu-id="e33fe-132">tooexport hello self-signed root certificate as a .pfx, select hello root certificate and use hello same steps as described in [Export a client certificate](#clientexport).</span></span>

## <span data-ttu-id="e33fe-133"><a name="clientcert"></a>Générer un certificat client</span><span class="sxs-lookup"><span data-stu-id="e33fe-133"><a name="clientcert"></a>Generate a client certificate</span></span>

<span data-ttu-id="e33fe-134">Chaque ordinateur client qui se connecte tooa virtuel à l’aide de Point-to-Site doit avoir un certificat client est installé.</span><span class="sxs-lookup"><span data-stu-id="e33fe-134">Each client computer that connects tooa VNet using Point-to-Site must have a client certificate installed.</span></span> <span data-ttu-id="e33fe-135">Vous générez un certificat client à partir du certificat racine auto-signé hello et puis exportez et installez le certificat de client hello.</span><span class="sxs-lookup"><span data-stu-id="e33fe-135">You generate a client certificate from hello self-signed root certificate, and then export and install hello client certificate.</span></span> <span data-ttu-id="e33fe-136">Si le certificat de client hello n’est pas installé, l’authentification échoue.</span><span class="sxs-lookup"><span data-stu-id="e33fe-136">If hello client certificate is not installed, authentication fails.</span></span> 

<span data-ttu-id="e33fe-137">Hello étapes suivantes vous guident génération d’un certificat client à partir d’un certificat racine auto-signé.</span><span class="sxs-lookup"><span data-stu-id="e33fe-137">hello following steps walk you through generating a client certificate from a self-signed root certificate.</span></span> <span data-ttu-id="e33fe-138">Vous pouvez générer plusieurs certificats de client à partir de hello même certificat racine.</span><span class="sxs-lookup"><span data-stu-id="e33fe-138">You may generate multiple client certificates from hello same root certificate.</span></span> <span data-ttu-id="e33fe-139">Lorsque vous générez les certificats de client à l’aide des étapes hello ci-dessous, hello client certificat est automatiquement installé sur l’ordinateur de hello que vous avez utilisé le certificat de hello toogenerate.</span><span class="sxs-lookup"><span data-stu-id="e33fe-139">When you generate client certificates using hello steps below, hello client certificate is automatically installed on hello computer that you used toogenerate hello certificate.</span></span> <span data-ttu-id="e33fe-140">Si vous voulez tooinstall un certificat client sur un autre ordinateur client, vous pouvez exporter le certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="e33fe-140">If you want tooinstall a client certificate on another client computer, you can export hello certificate.</span></span>

<span data-ttu-id="e33fe-141">les exemples de Hello utilisent toogenerate d’applet de commande New-SelfSignedCertificate hello un certificat client qui expire un an.</span><span class="sxs-lookup"><span data-stu-id="e33fe-141">hello examples use hello New-SelfSignedCertificate cmdlet toogenerate a client certificate that expires in one year.</span></span> <span data-ttu-id="e33fe-142">Pour plus d’informations de paramètre supplémentaires, telles que la définition d’une valeur d’expiration différentes pour le certificat de client hello, consultez [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="e33fe-142">For additional parameter information, such as setting a different expiration value for hello client certificate, see [New-SelfSignedCertificate](https://technet.microsoft.com/itpro/powershell/windows/pkiclient/new-selfsignedcertificate).</span></span>

### <a name="example-1"></a><span data-ttu-id="e33fe-143">Exemple 1</span><span class="sxs-lookup"><span data-stu-id="e33fe-143">Example 1</span></span>

<span data-ttu-id="e33fe-144">Cet exemple utilise hello déclaré variable '$cert' à partir de la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="e33fe-144">This example uses hello declared '$cert' variable from hello previous section.</span></span> <span data-ttu-id="e33fe-145">Si vous avez fermé la console PowerShell de hello après création hello certificat racine auto-signé, ou sont créer des certificats client supplémentaires pour une nouvelle session de console PowerShell, utilisez les étapes de hello dans [exemple 2](#ex2).</span><span class="sxs-lookup"><span data-stu-id="e33fe-145">If you closed hello PowerShell console after creating hello self-signed root certificate, or are creating additional client certificates in a new PowerShell console session, use hello steps in [Example 2](#ex2).</span></span>

<span data-ttu-id="e33fe-146">Modifier et exécuter hello exemple toogenerate un certificat client.</span><span class="sxs-lookup"><span data-stu-id="e33fe-146">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="e33fe-147">Si vous exécutez hello exemple suivant sans le modifier, hello en résulte un certificat client nommé « P2SChildCert ».</span><span class="sxs-lookup"><span data-stu-id="e33fe-147">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span>  <span data-ttu-id="e33fe-148">Si vous souhaitez que le certificat d’enfant tooname hello par autre chose, modifiez la valeur CN de hello.</span><span class="sxs-lookup"><span data-stu-id="e33fe-148">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="e33fe-149">Ne modifiez pas hello TextExtension lors de l’exécution de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="e33fe-149">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="e33fe-150">certificat client Hello que vous générez est automatiquement installé dans « Certificats - actuel\Personnel\Certificats » sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e33fe-150">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

```powershell
New-SelfSignedCertificate -Type Custom -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
```

### <span data-ttu-id="e33fe-151"><a name="ex2"></a>Exemple 2</span><span class="sxs-lookup"><span data-stu-id="e33fe-151"><a name="ex2"></a>Example 2</span></span>

<span data-ttu-id="e33fe-152">Si vous créez des clients supplémentaires des certificats, ou de sont ne pas à l’aide de bienvenue même session PowerShell que vous avez utilisé toocreate votre certificat racine auto-signé, hello utilisation comme suit :</span><span class="sxs-lookup"><span data-stu-id="e33fe-152">If you are creating additional client certificates, or are not using hello same PowerShell session that you used toocreate your self-signed root certificate, use hello following steps:</span></span>

1. <span data-ttu-id="e33fe-153">Identifiez le certificat racine auto-signé hello qui est installé sur l’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="e33fe-153">Identify hello self-signed root certificate that is installed on hello computer.</span></span> <span data-ttu-id="e33fe-154">Cette applet de commande renvoie la liste des certificats installés sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e33fe-154">This cmdlet returns a list of certificates that are installed on your computer.</span></span>

  ```powershell
  Get-ChildItem -Path “Cert:\CurrentUser\My”
  ```
2. <span data-ttu-id="e33fe-155">Recherchez le nom du sujet hello d’hello retourné la liste, puis l’empreinte numérique hello copie trouve du texte tooa tooit suivant fichier.</span><span class="sxs-lookup"><span data-stu-id="e33fe-155">Locate hello subject name from hello returned list, then copy hello thumbprint that is located next tooit tooa text file.</span></span> <span data-ttu-id="e33fe-156">Dans l’exemple suivant de hello, il existe deux certificats.</span><span class="sxs-lookup"><span data-stu-id="e33fe-156">In hello following example, there are two certificates.</span></span> <span data-ttu-id="e33fe-157">nom CN Hello est hello du certificat racine auto-signé de hello à partir de laquelle vous souhaitez toogenerate un certificat enfant.</span><span class="sxs-lookup"><span data-stu-id="e33fe-157">hello CN name is hello name of hello self-signed root certificate from which you want toogenerate a child certificate.</span></span> <span data-ttu-id="e33fe-158">Dans ce cas, « P2SRootCert ».</span><span class="sxs-lookup"><span data-stu-id="e33fe-158">In this case, 'P2SRootCert'.</span></span>

  ```
  Thumbprint                                Subject
  
  AED812AD883826FF76B4D1D5A77B3C08EFA79F3F  CN=P2SChildCert4
  7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655  CN=P2SRootCert
  ```
3. <span data-ttu-id="e33fe-159">Déclarez une variable pour le certificat racine de hello à l’aide de l’empreinte numérique hello à partir de l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="e33fe-159">Declare a variable for hello root certificate using hello thumbprint from hello previous step.</span></span> <span data-ttu-id="e33fe-160">Remplacez l’empreinte numérique avec l’empreinte numérique hello hello du certificat de racine à partir duquel vous souhaitez toogenerate un certificat enfant.</span><span class="sxs-lookup"><span data-stu-id="e33fe-160">Replace THUMBPRINT with hello thumbprint of hello root certificate from which you want toogenerate a child certificate.</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\THUMBPRINT"
  ```

  <span data-ttu-id="e33fe-161">Par exemple, la variable de hello à l’aide de l’empreinte numérique hello pour P2SRootCert à l’étape précédente de hello, ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="e33fe-161">For example, using hello thumbprint for P2SRootCert in hello previous step, hello variable looks like this:</span></span>

  ```powershell
  $cert = Get-ChildItem -Path "Cert:\CurrentUser\My\7181AA8C1B4D34EEDB2F3D3BEC5839F3FE52D655"
  ```
4.  <span data-ttu-id="e33fe-162">Modifier et exécuter hello exemple toogenerate un certificat client.</span><span class="sxs-lookup"><span data-stu-id="e33fe-162">Modify and run hello example toogenerate a client certificate.</span></span> <span data-ttu-id="e33fe-163">Si vous exécutez hello exemple suivant sans le modifier, hello en résulte un certificat client nommé « P2SChildCert ».</span><span class="sxs-lookup"><span data-stu-id="e33fe-163">If you run hello following example without modifying it, hello result is a client certificate named 'P2SChildCert'.</span></span> <span data-ttu-id="e33fe-164">Si vous souhaitez que le certificat d’enfant tooname hello par autre chose, modifiez la valeur CN de hello.</span><span class="sxs-lookup"><span data-stu-id="e33fe-164">If you want tooname hello child certificate something else, modify hello CN value.</span></span> <span data-ttu-id="e33fe-165">Ne modifiez pas hello TextExtension lors de l’exécution de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="e33fe-165">Do not change hello TextExtension when running this example.</span></span> <span data-ttu-id="e33fe-166">certificat client Hello que vous générez est automatiquement installé dans « Certificats - actuel\Personnel\Certificats » sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e33fe-166">hello client certificate that you generate is automatically installed in 'Certificates - Current User\Personal\Certificates' on your computer.</span></span>

  ```powershell
  New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" `
  -Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")
  ```

## <span data-ttu-id="e33fe-167"><a name="clientexport"></a>Exporter un certificat client</span><span class="sxs-lookup"><span data-stu-id="e33fe-167"><a name="clientexport"></a>Export a client certificate</span></span>   

[!INCLUDE [Export client certificate](../../includes/vpn-gateway-certificates-export-client-cert-include.md)]

## <span data-ttu-id="e33fe-168"><a name="install"></a>Installer un certificat client exporté</span><span class="sxs-lookup"><span data-stu-id="e33fe-168"><a name="install"></a>Install an exported client certificate</span></span>

[!INCLUDE [Install client certificate](../../includes/vpn-gateway-certificates-install-client-cert-include.md)]

## <a name="next-steps"></a><span data-ttu-id="e33fe-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e33fe-169">Next steps</span></span>

<span data-ttu-id="e33fe-170">Poursuivez votre configuration point à site.</span><span class="sxs-lookup"><span data-stu-id="e33fe-170">Continue with your Point-to-Site configuration.</span></span> 

* <span data-ttu-id="e33fe-171">Pour **le Gestionnaire de ressources** étapes du modèle de déploiement, consultez [configurer un tooa de connexion de Point-to-Site réseau virtuel](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e33fe-171">For **Resource Manager** deployment model steps, see [Configure a Point-to-Site connection tooa VNet](vpn-gateway-howto-point-to-site-resource-manager-portal.md).</span></span> 
* <span data-ttu-id="e33fe-172">Pour **classique** étapes du modèle de déploiement, consultez [configurer un tooa de connexion VPN Point à Site réseau virtuel (classiques)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e33fe-172">For **classic** deployment model steps, see [Configure a Point-to-Site VPN connection tooa VNet (classic)](vpn-gateway-howto-point-to-site-classic-azure-portal.md).</span></span>
