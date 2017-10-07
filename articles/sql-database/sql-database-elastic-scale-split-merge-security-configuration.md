---
title: "configuration de la sécurité fusion aaaSplit | Documents Microsoft"
description: "Définissez les certificats x 409 pour le chiffrement"
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="6e5f1-103">Configuration de la sécurité du fractionnement et de la fusion</span><span class="sxs-lookup"><span data-stu-id="6e5f1-103">Split-merge security configuration</span></span>
<span data-ttu-id="6e5f1-104">service de fractionnement/fusion toouse hello, vous devez correctement configurer la sécurité.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-104">toouse hello Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="6e5f1-105">service de Hello fait partie de la fonctionnalité de mise à l’échelle élastique hello de base de données SQL Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-105">hello service is part of hello Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="6e5f1-106">Pour plus d’informations, consultez le [didacticiel sur le service de fusion et de fractionnement de l’infrastructure élastique](sql-database-elastic-scale-configure-deploy-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="6e5f1-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="6e5f1-107">Configuration des certificats</span><span class="sxs-lookup"><span data-stu-id="6e5f1-107">Configuring certificates</span></span>
<span data-ttu-id="6e5f1-108">Les certificats sont configurés de deux manières.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="6e5f1-109">tooConfigure hello certificat SSL</span><span class="sxs-lookup"><span data-stu-id="6e5f1-109">tooConfigure hello SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="6e5f1-110">tooConfigure les certificats clients</span><span class="sxs-lookup"><span data-stu-id="6e5f1-110">tooConfigure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a><span data-ttu-id="6e5f1-111">certificats tooobtain</span><span class="sxs-lookup"><span data-stu-id="6e5f1-111">tooobtain certificates</span></span>
<span data-ttu-id="6e5f1-112">Les certificats peuvent être obtenues à partir d’autorités de certification publique (CA) ou à partir de hello [Service de certificats Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e5f1-112">Certificates can be obtained from public Certificate Authorities (CAs) or from hello [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="6e5f1-113">Il s’agit des certificats tooobtain hello préféré méthodes.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-113">These are hello preferred methods tooobtain certificates.</span></span>

<span data-ttu-id="6e5f1-114">Si ces options ne sont pas disponibles, vous pouvez générer des **certificats auto-signés**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-toogenerate-certificates"></a><span data-ttu-id="6e5f1-115">Certificats de toogenerate d’outils</span><span class="sxs-lookup"><span data-stu-id="6e5f1-115">Tools toogenerate certificates</span></span>
* [<span data-ttu-id="6e5f1-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="6e5f1-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="6e5f1-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="6e5f1-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a><span data-ttu-id="6e5f1-118">outils de hello toorun</span><span class="sxs-lookup"><span data-stu-id="6e5f1-118">toorun hello tools</span></span>
* <span data-ttu-id="6e5f1-119">Depuis une invite de commandes développeur pour Visual Studio, consultez la rubrique [Invite de commandes Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="6e5f1-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="6e5f1-120">Si installée, accédez à :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="6e5f1-121">Obtenir hello WDK de [Windows 8.1 : télécharger des kits et des outils](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="6e5f1-121">Get hello WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="tooconfigure-hello-ssl-certificate"></a><span data-ttu-id="6e5f1-122">certificat SSL de hello tooconfigure</span><span class="sxs-lookup"><span data-stu-id="6e5f1-122">tooconfigure hello SSL certificate</span></span>
<span data-ttu-id="6e5f1-123">Un certificat SSL est requis tooencrypt hello communication et authentifier hello serveur.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-123">A SSL certificate is required tooencrypt hello communication and authenticate hello server.</span></span> <span data-ttu-id="6e5f1-124">Choisissez hello plus applicable de trois scénarios hello ci-dessous et exécuter toutes ses étapes :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-124">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="6e5f1-125">Création d’un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="6e5f1-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="6e5f1-126">Création d’un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="6e5f1-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="6e5f1-127">Création d’un fichier PFX pour un certificat SSL auto-signé</span><span class="sxs-lookup"><span data-stu-id="6e5f1-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="6e5f1-128">Télécharger le certificat SSL tooCloud Service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-128">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="6e5f1-129">Mise à jour du certificat SSL dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="6e5f1-130">Importation de l’autorité de certification SSL</span><span class="sxs-lookup"><span data-stu-id="6e5f1-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="6e5f1-131">stockage d’un certificat existant à partir du certificat de hello toouse</span><span class="sxs-lookup"><span data-stu-id="6e5f1-131">toouse an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="6e5f1-132">Exportation d’un certificat SSL à partir du magasin de certificats</span><span class="sxs-lookup"><span data-stu-id="6e5f1-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="6e5f1-133">Télécharger le certificat SSL tooCloud Service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-133">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="6e5f1-134">Mise à jour du certificat SSL dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="6e5f1-135">toouse un certificat existant dans un fichier PFX</span><span class="sxs-lookup"><span data-stu-id="6e5f1-135">toouse an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="6e5f1-136">Télécharger le certificat SSL tooCloud Service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-136">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="6e5f1-137">Mise à jour du certificat SSL dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a><span data-ttu-id="6e5f1-138">certificats clients tooconfigure</span><span class="sxs-lookup"><span data-stu-id="6e5f1-138">tooconfigure client certificates</span></span>
<span data-ttu-id="6e5f1-139">Certificats clients sont requis dans l’ordre tooauthenticate demandes toohello service.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-139">Client certificates are required in order tooauthenticate requests toohello service.</span></span> <span data-ttu-id="6e5f1-140">Choisissez hello plus applicable de trois scénarios hello ci-dessous et exécuter toutes ses étapes :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-140">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="6e5f1-141">Désactivation des certificats clients</span><span class="sxs-lookup"><span data-stu-id="6e5f1-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="6e5f1-142">Désactivation de l’authentification par certificat client</span><span class="sxs-lookup"><span data-stu-id="6e5f1-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="6e5f1-143">Émission de nouveaux certificats clients auto-signés</span><span class="sxs-lookup"><span data-stu-id="6e5f1-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="6e5f1-144">Création d’une autorité de certification auto-signée</span><span class="sxs-lookup"><span data-stu-id="6e5f1-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="6e5f1-145">Télécharger le certificat d’autorité de certification tooCloud Service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-145">Upload CA Certificate tooCloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="6e5f1-146">Mise à jour du certificat CA dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="6e5f1-147">Émission de certificats clients</span><span class="sxs-lookup"><span data-stu-id="6e5f1-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="6e5f1-148">Création de fichiers PFX pour les certificats clients</span><span class="sxs-lookup"><span data-stu-id="6e5f1-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="6e5f1-149">Importation d’un certificat client</span><span class="sxs-lookup"><span data-stu-id="6e5f1-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="6e5f1-150">Copie des empreintes numériques des certificats clients</span><span class="sxs-lookup"><span data-stu-id="6e5f1-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="6e5f1-151">Configurer les Clients d’autorisé Bonjour fichier de Configuration de Service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-151">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="6e5f1-152">Utilisation de certificats clients existants</span><span class="sxs-lookup"><span data-stu-id="6e5f1-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="6e5f1-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="6e5f1-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="6e5f1-154">Télécharger le certificat d’autorité de certification tooCloud Service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-154">Upload CA Certificate tooCloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="6e5f1-155">Mise à jour du certificat CA dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="6e5f1-156">Copie des empreintes numériques des certificats clients</span><span class="sxs-lookup"><span data-stu-id="6e5f1-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="6e5f1-157">Configurer les Clients d’autorisé Bonjour fichier de Configuration de Service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-157">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="6e5f1-158">Configuration de la vérification de révocation des certificats clients</span><span class="sxs-lookup"><span data-stu-id="6e5f1-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="6e5f1-159">Adresses IP autorisées</span><span class="sxs-lookup"><span data-stu-id="6e5f1-159">Allowed IP addresses</span></span>
<span data-ttu-id="6e5f1-160">Points de terminaison de service accès toohello peuvent être restreint toospecific les plages d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-160">Access toohello service endpoints can be restricted toospecific ranges of IP addresses.</span></span>

## <a name="tooconfigure-encryption-for-hello-store"></a><span data-ttu-id="6e5f1-161">chiffrement tooconfigure pour le magasin de hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-161">tooconfigure encryption for hello store</span></span>
<span data-ttu-id="6e5f1-162">Un certificat est requis tooencrypt informations d’identification hello qui sont stockées dans le magasin de métadonnées hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-162">A certificate is required tooencrypt hello credentials that are stored in hello metadata store.</span></span> <span data-ttu-id="6e5f1-163">Choisissez hello plus applicable de trois scénarios hello ci-dessous et exécuter toutes ses étapes :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-163">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="6e5f1-164">Utilisation d’un nouveau certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="6e5f1-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="6e5f1-165">Création d’un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="6e5f1-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="6e5f1-166">Création d’un fichier PFX pour un certificat de chiffrement auto-signé</span><span class="sxs-lookup"><span data-stu-id="6e5f1-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="6e5f1-167">Télécharger le certificat de chiffrement tooCloud Service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-167">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="6e5f1-168">Mise à jour du certificat de chiffrement dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="6e5f1-169">Utiliser un certificat existant à partir du magasin de certificats hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-169">Use an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="6e5f1-170">Exportation d’un certificat de chiffrement à partir du magasin de certificats</span><span class="sxs-lookup"><span data-stu-id="6e5f1-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="6e5f1-171">Télécharger le certificat de chiffrement tooCloud Service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-171">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="6e5f1-172">Mise à jour du certificat de chiffrement dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="6e5f1-173">Utilisation d’un certificat existant dans un fichier PFX</span><span class="sxs-lookup"><span data-stu-id="6e5f1-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="6e5f1-174">Télécharger le certificat de chiffrement tooCloud Service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-174">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="6e5f1-175">Mise à jour du certificat de chiffrement dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a><span data-ttu-id="6e5f1-176">configuration par défaut de Hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-176">hello default configuration</span></span>
<span data-ttu-id="6e5f1-177">configuration par défaut de Hello refuse de point de terminaison HTTP tous les accès toohello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-177">hello default configuration denies all access toohello HTTP endpoint.</span></span> <span data-ttu-id="6e5f1-178">Il s’agit de hello recommandée, étant donné que les points de terminaison hello demandes toothese peuvent contenir des informations sensibles telles que des informations d’identification de la base de données.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-178">This is hello recommended setting, since hello requests toothese endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="6e5f1-179">configuration par défaut de Hello permet de point de terminaison HTTPS tous les accès toohello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-179">hello default configuration allows all access toohello HTTPS endpoint.</span></span> <span data-ttu-id="6e5f1-180">Ce paramètre peut être restreint davantage.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-180">This setting may be restricted further.</span></span>

### <a name="changing-hello-configuration"></a><span data-ttu-id="6e5f1-181">La modification de Configuration de hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-181">Changing hello Configuration</span></span>
<span data-ttu-id="6e5f1-182">groupe de règles de contrôle d’accès qui s’appliquent de point de terminaison tooand Hello sont configurés dans hello  **<EndpointAcls>**  section Bonjour **fichier de configuration de service**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-182">hello group of access control rules that apply tooand endpoint are configured in hello **<EndpointAcls>** section in hello **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="6e5f1-183">règles de Hello dans un groupe de contrôle d’accès sont configurés dans un <AccessControl name=""> section du fichier de configuration de service hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-183">hello rules in an access control group are configured in a <AccessControl name=""> section of hello service configuration file.</span></span> 

<span data-ttu-id="6e5f1-184">format de Hello est expliquée dans la documentation de listes de contrôle d’accès réseau.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-184">hello format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="6e5f1-185">Par exemple, tooallow uniquement des adresses IP dans hello plage 100.100.0.0 too100.100.255.255 tooaccess hello point de terminaison HTTPS, les règles de hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-185">For example, tooallow only IPs in hello range 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS endpoint, hello rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="6e5f1-186">Prévention du déni de service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-186">Denial of service prevention</span></span>
<span data-ttu-id="6e5f1-187">Il existe deux mécanismes différents pris en charge toodetect et empêchent les attaques par déni de Service :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-187">There are two different mechanisms supported toodetect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="6e5f1-188">Limiter le nombre de demandes simultanées par hôte distant (désactivé par défaut)</span><span class="sxs-lookup"><span data-stu-id="6e5f1-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="6e5f1-189">Limiter le taux d’accès par hôte distant (activé par défaut)</span><span class="sxs-lookup"><span data-stu-id="6e5f1-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="6e5f1-190">Elles sont basées sur les fonctionnalités de hello en sécurité IP dynamique dans IIS.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-190">These are based on hello features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="6e5f1-191">Lorsque la modification de cette configuration Méfiez-vous de hello suivant facteurs :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-191">When changing this configuration beware of hello following factors:</span></span>

* <span data-ttu-id="6e5f1-192">comportement de Hello de proxies et les périphériques de traduction d’adresses réseau sur les informations d’hôte distant hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-192">hello behavior of proxies and Network Address Translation devices over hello remote host information</span></span>
* <span data-ttu-id="6e5f1-193">Chaque ressource tooany de demande dans un rôle web de hello est pris en compte (par exemple, le chargement des scripts, des images, etc.)</span><span class="sxs-lookup"><span data-stu-id="6e5f1-193">Each request tooany resource in hello web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="6e5f1-194">Limitation du nombre d'accès simultanés</span><span class="sxs-lookup"><span data-stu-id="6e5f1-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="6e5f1-195">Hello que configurer ce comportement sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-195">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="6e5f1-196">Modifier la DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable cette protection.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-196">Change DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="6e5f1-197">Restriction du taux d’accès</span><span class="sxs-lookup"><span data-stu-id="6e5f1-197">Restricting rate of access</span></span>
<span data-ttu-id="6e5f1-198">Hello que configurer ce comportement sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-198">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a><span data-ttu-id="6e5f1-199">Configuration hello réponse tooa a rejeté la demande</span><span class="sxs-lookup"><span data-stu-id="6e5f1-199">Configuring hello response tooa denied request</span></span>
<span data-ttu-id="6e5f1-200">Hello paramètre suivant configure tooa de réponse hello a rejeté la demande :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-200">hello following setting configures hello response tooa denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="6e5f1-201">Consultez la documentation du toohello pour la sécurité IP dynamique dans IIS pour les autres valeurs prises en charge.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-201">Refer toohello documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="6e5f1-202">Opérations de configuration des certificats de service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="6e5f1-203">Cette rubrique sert de référence uniquement.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-203">This topic is for reference only.</span></span> <span data-ttu-id="6e5f1-204">Suivez les étapes de configuration hello décrites dans :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-204">Please follow hello configuration steps outlined in:</span></span>

* <span data-ttu-id="6e5f1-205">Configurer un certificat SSL de hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-205">Configure hello SSL certificate</span></span>
* <span data-ttu-id="6e5f1-206">Configuration des certificats clients</span><span class="sxs-lookup"><span data-stu-id="6e5f1-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="6e5f1-207">Création d’un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="6e5f1-207">Create a self-signed certificate</span></span>
<span data-ttu-id="6e5f1-208">Exécutez :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="6e5f1-209">toocustomize :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-209">toocustomize:</span></span>

* <span data-ttu-id="6e5f1-210">URL du service - n avec hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-210">-n with hello service URL.</span></span> <span data-ttu-id="6e5f1-211">Les caractères génériques (CN=*.cloudapp.net) et d’autres noms (CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net) sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="6e5f1-212">-e avec la date d’expiration de certificat hello créer un mot de passe fort et le spécifier lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-212">-e with hello certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="6e5f1-213">Création d’un fichier PFX pour un certificat SSL auto-signé</span><span class="sxs-lookup"><span data-stu-id="6e5f1-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="6e5f1-214">Exécutez :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="6e5f1-215">Entrez le mot de passe et exportez le certificat avec les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="6e5f1-216">Oui, exporter la clé privée de hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-216">Yes, export hello private key</span></span>
* <span data-ttu-id="6e5f1-217">Exporter toutes les propriétés étendues</span><span class="sxs-lookup"><span data-stu-id="6e5f1-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="6e5f1-218">Exportation d’un certificat SSL à partir du magasin de certificats</span><span class="sxs-lookup"><span data-stu-id="6e5f1-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="6e5f1-219">Recherchez le certificat</span><span class="sxs-lookup"><span data-stu-id="6e5f1-219">Find certificate</span></span>
* <span data-ttu-id="6e5f1-220">Cliquez sur Actions -> Toutes les tâches -> Exporter...</span><span class="sxs-lookup"><span data-stu-id="6e5f1-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="6e5f1-221">Exportez le certificat dans un fichier .PFX avec les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="6e5f1-222">Oui, exporter la clé privée de hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-222">Yes, export hello private key</span></span>
  * <span data-ttu-id="6e5f1-223">Inclure tous les certificats dans le chemin d’accès de certification hello si possible * exporter toutes les propriétés étendues</span><span class="sxs-lookup"><span data-stu-id="6e5f1-223">Include all certificates in hello certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-toocloud-service"></a><span data-ttu-id="6e5f1-224">Télécharger le service toocloud de certificat SSL</span><span class="sxs-lookup"><span data-stu-id="6e5f1-224">Upload SSL certificate toocloud service</span></span>
<span data-ttu-id="6e5f1-225">Téléchargez le certificat avec hello existant ou générés. Fichier PFX portant hello paire de clés SSL :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-225">Upload certificate with hello existing or generated .PFX file with hello SSL key pair:</span></span>

* <span data-ttu-id="6e5f1-226">Entrez hello de mot de passe protège les informations de clé privée hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-226">Enter hello password protecting hello private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="6e5f1-227">Mise à jour du certificat SSL dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="6e5f1-228">Mettre à jour la valeur d’empreinte numérique hello Hello suivant paramètre dans le fichier de configuration de service hello avec l’empreinte numérique hello du service de cloud toohello hello certificat téléchargé :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-228">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="6e5f1-229">Importation de l’autorité de certification SSL</span><span class="sxs-lookup"><span data-stu-id="6e5f1-229">Import SSL certification authority</span></span>
<span data-ttu-id="6e5f1-230">Suivez ces étapes dans tous les comptes/machine qui communiqueront avec le service de hello :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-230">Follow these steps in all account/machine that will communicate with hello service:</span></span>

* <span data-ttu-id="6e5f1-231">Double-cliquez sur hello. Fichier CER dans l’Explorateur Windows</span><span class="sxs-lookup"><span data-stu-id="6e5f1-231">Double-click hello .CER file in Windows Explorer</span></span>
* <span data-ttu-id="6e5f1-232">Dans la boîte de dialogue certificat hello, cliquez sur Installer le certificat...</span><span class="sxs-lookup"><span data-stu-id="6e5f1-232">In hello Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="6e5f1-233">Importer des certificats dans hello que magasin des autorités de Certification racines de confiance</span><span class="sxs-lookup"><span data-stu-id="6e5f1-233">Import certificate into hello Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="6e5f1-234">Désactivation de l’authentification par certificat client</span><span class="sxs-lookup"><span data-stu-id="6e5f1-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="6e5f1-235">Uniquement basée sur certificat l’authentification du client est prise en charge et sa désactivation autorisera des points de terminaison du service de toohello accès public, à moins que les autres mécanismes sont en place (par exemple, Microsoft Azure Virtual Network).</span><span class="sxs-lookup"><span data-stu-id="6e5f1-235">Only client certificate-based authentication is supported and disabling it will allow for public access toohello service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="6e5f1-236">Modifier toofalse de ces paramètres dans la fonctionnalité hello tooturn du fichier configuration hello service :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-236">Change these settings toofalse in hello service configuration file tooturn hello feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="6e5f1-237">Ensuite, copiez hello même empreinte numérique que hello SSL de certificat dans le paramètre hello autorité de certification du certificat :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-237">Then, copy hello same thumbprint as hello SSL certificate in hello CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="6e5f1-238">Création d’une autorité de certification auto-signée</span><span class="sxs-lookup"><span data-stu-id="6e5f1-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="6e5f1-239">Exécutez hello suivant les étapes toocreate un tooact un certificat auto-signé comme une autorité de Certification :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-239">Execute hello following steps toocreate a self-signed certificate tooact as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="6e5f1-240">toocustomize il</span><span class="sxs-lookup"><span data-stu-id="6e5f1-240">toocustomize it</span></span>

* <span data-ttu-id="6e5f1-241">-e avec la date d’expiration de certification hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-241">-e with hello certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="6e5f1-242">Recherche de la clé publique de l’autorité de certification</span><span class="sxs-lookup"><span data-stu-id="6e5f1-242">Find CA public key</span></span>
<span data-ttu-id="6e5f1-243">Tous les certificats de client doivent avoir été émis par une autorité de Certification approuvée par le service de hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-243">All client certificates must have been issued by a Certification Authority trusted by hello service.</span></span> <span data-ttu-id="6e5f1-244">Trouver toohello de clé publique hello autorité de Certification qui a émis les certificats de client hello qui vont toobe utilisé pour l’authentification dans tooupload d’ordre il toohello le service cloud.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-244">Find hello public key toohello Certification Authority that issued hello client certificates that are going toobe used for authentication in order tooupload it toohello cloud service.</span></span>

<span data-ttu-id="6e5f1-245">Si le fichier hello avec une clé publique hello n’est pas disponible, l’exporter à partir du magasin de certificats hello :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-245">If hello file with hello public key is not available, export it from hello certificate store:</span></span>

* <span data-ttu-id="6e5f1-246">Recherchez le certificat</span><span class="sxs-lookup"><span data-stu-id="6e5f1-246">Find certificate</span></span>
  * <span data-ttu-id="6e5f1-247">Recherche d’un certificat client publié par hello même autorité de Certification</span><span class="sxs-lookup"><span data-stu-id="6e5f1-247">Search for a client certificate issued by hello same Certification Authority</span></span>
* <span data-ttu-id="6e5f1-248">Double-cliquez sur le certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-248">Double-click hello certificate.</span></span>
* <span data-ttu-id="6e5f1-249">Sélectionnez l’onglet de chemin d’accès de Certification hello dans la boîte de dialogue certificat hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-249">Select hello Certification Path tab in hello Certificate dialog.</span></span>
* <span data-ttu-id="6e5f1-250">Double-cliquez sur entrée d’autorité de certification hello dans le chemin d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-250">Double-click hello CA entry in hello path.</span></span>
* <span data-ttu-id="6e5f1-251">Prenez des notes de propriétés du certificat hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-251">Take notes of hello certificate properties.</span></span>
* <span data-ttu-id="6e5f1-252">Fermer hello **certificat** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-252">Close hello **Certificate** dialog.</span></span>
* <span data-ttu-id="6e5f1-253">Recherchez le certificat</span><span class="sxs-lookup"><span data-stu-id="6e5f1-253">Find certificate</span></span>
  * <span data-ttu-id="6e5f1-254">Recherchez hello autorité de certification indiquée ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-254">Search for hello CA noted above.</span></span>
* <span data-ttu-id="6e5f1-255">Cliquez sur Actions -> Toutes les tâches -> Exporter...</span><span class="sxs-lookup"><span data-stu-id="6e5f1-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="6e5f1-256">Exportez le certificat dans un fichier .CER avec les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="6e5f1-257">**Non, ne pas exporter la clé privée de hello**</span><span class="sxs-lookup"><span data-stu-id="6e5f1-257">**No, do not export hello private key**</span></span>
  * <span data-ttu-id="6e5f1-258">Inclure tous les certificats dans le chemin d’accès de certification hello si possible.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-258">Include all certificates in hello certification path if possible.</span></span>
  * <span data-ttu-id="6e5f1-259">Exporter toutes les propriétés étendues.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-toocloud-service"></a><span data-ttu-id="6e5f1-260">Télécharger le service toocloud de certificat autorité de certification</span><span class="sxs-lookup"><span data-stu-id="6e5f1-260">Upload CA certificate toocloud service</span></span>
<span data-ttu-id="6e5f1-261">Téléchargez le certificat avec hello existant ou générés. Fichier CER avec une clé publique hello autorité de certification.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-261">Upload certificate with hello existing or generated .CER file with hello CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="6e5f1-262">Mise à jour du certificat CA dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="6e5f1-263">Mettre à jour la valeur d’empreinte numérique hello Hello suivant paramètre dans le fichier de configuration de service hello avec l’empreinte numérique hello du service de cloud toohello hello certificat téléchargé :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-263">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="6e5f1-264">Mettre à jour la valeur hello hello après avoir défini avec hello même empreinte numérique :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-264">Update hello value of hello following setting with hello same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="6e5f1-265">Émission de certificats clients</span><span class="sxs-lookup"><span data-stu-id="6e5f1-265">Issue client certificates</span></span>
<span data-ttu-id="6e5f1-266">Chaque service de hello individuels tooaccess autorisés doit avoir un certificat client publié pour his/hers exclusif à utiliser et doit choisir que HIS/hers propre mot de passe fort tooprotect sa clé privée.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-266">Each individual authorized tooaccess hello service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password tooprotect its private key.</span></span> 

<span data-ttu-id="6e5f1-267">Hello suit doit être exécutée dans hello même machine hello auto-signé où certificat d’autorité de certification a été généré et stocké :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-267">hello following steps must be executed in hello same machine where hello self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="6e5f1-268">Personnalisation :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-268">Customizing:</span></span>

* <span data-ttu-id="6e5f1-269">-n avec un ID de client toohello qui est authentifié avec ce certificat</span><span class="sxs-lookup"><span data-stu-id="6e5f1-269">-n with an ID for toohello client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="6e5f1-270">-e avec la date d’expiration de certificat hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-270">-e with hello certificate expiration date</span></span>
* <span data-ttu-id="6e5f1-271">MyID.pvk et MyID.cer avec des noms de fichier uniques pour ce certificat client</span><span class="sxs-lookup"><span data-stu-id="6e5f1-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="6e5f1-272">Cette commande demande une toobe de mot de passe créé, puis utilisé une seule fois.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-272">This command will prompt for a password toobe created and then used once.</span></span> <span data-ttu-id="6e5f1-273">Utilisez un mot de passe fort.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="6e5f1-274">Création de fichiers PFX pour les certificats clients</span><span class="sxs-lookup"><span data-stu-id="6e5f1-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="6e5f1-275">Pour chaque certificat client généré, exécutez :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="6e5f1-276">Personnalisation :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello client certificate

<span data-ttu-id="6e5f1-277">Entrez le mot de passe et exportez le certificat avec les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="6e5f1-278">Oui, exporter la clé privée de hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-278">Yes, export hello private key</span></span>
* <span data-ttu-id="6e5f1-279">Exporter toutes les propriétés étendues</span><span class="sxs-lookup"><span data-stu-id="6e5f1-279">Export all extended properties</span></span>
* <span data-ttu-id="6e5f1-280">toowhom individuels de Hello qu'est émis ce certificat doit choisir le mot de passe de hello exportation</span><span class="sxs-lookup"><span data-stu-id="6e5f1-280">hello individual toowhom this certificate is being issued should choose hello export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="6e5f1-281">Importation d’un certificat client</span><span class="sxs-lookup"><span data-stu-id="6e5f1-281">Import client certificate</span></span>
<span data-ttu-id="6e5f1-282">Chaque utilisateur pour lequel un certificat client a été émis doit importer la paire de clés hello dans des machines de hello, il utilisera toocommunicate avec le service de hello :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-282">Each individual for whom a client certificate has been issued should import hello key pair in hello machines he/she will use toocommunicate with hello service:</span></span>

* <span data-ttu-id="6e5f1-283">Double-cliquez sur hello. Fichier PFX dans l’Explorateur Windows</span><span class="sxs-lookup"><span data-stu-id="6e5f1-283">Double-click hello .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="6e5f1-284">Importer un certificat dans hello Personal stocker au moins cette option :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-284">Import certificate into hello Personal store with at least this option:</span></span>
  * <span data-ttu-id="6e5f1-285">Inclure toutes les propriétés étendues activées</span><span class="sxs-lookup"><span data-stu-id="6e5f1-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="6e5f1-286">Copie des empreintes numériques des certificats clients</span><span class="sxs-lookup"><span data-stu-id="6e5f1-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="6e5f1-287">Chaque utilisateur pour lequel un certificat client a été émis devez suivre ces étapes dans l’ordre tooobtain hello empreinte numérique du his/hers certificat qui sera ajouté le fichier de configuration de service toohello :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-287">Each individual for whom a client certificate has been issued must follow these steps in order tooobtain hello thumbprint of his/hers certificate which will be added toohello service configuration file:</span></span>

* <span data-ttu-id="6e5f1-288">Exécutez certmgr.exe</span><span class="sxs-lookup"><span data-stu-id="6e5f1-288">Run certmgr.exe</span></span>
* <span data-ttu-id="6e5f1-289">Sélectionnez l’onglet personnel de hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-289">Select hello Personal tab</span></span>
* <span data-ttu-id="6e5f1-290">Double-cliquez sur le certificat de client hello toobe utilisé pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="6e5f1-290">Double-click hello client certificate toobe used for authentication</span></span>
* <span data-ttu-id="6e5f1-291">Hello certificat boîte de dialogue qui s’ouvre, sélectionnez onglet Détails de hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-291">In hello Certificate dialog that opens, select hello Details tab</span></span>
* <span data-ttu-id="6e5f1-292">Veillez à ce que l'option Afficher indique Tous</span><span class="sxs-lookup"><span data-stu-id="6e5f1-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="6e5f1-293">Champ Sélectionnez hello nommé l’empreinte numérique dans la liste de hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-293">Select hello field named Thumbprint in hello list</span></span>
* <span data-ttu-id="6e5f1-294">Copier la valeur hello de l’empreinte numérique hello ** supprimer des caractères Unicode non visible devant le premier chiffre de hello ** supprimer tous les espaces</span><span class="sxs-lookup"><span data-stu-id="6e5f1-294">Copy hello value of hello thumbprint ** Delete non-visible Unicode characters in front of hello first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a><span data-ttu-id="6e5f1-295">Configurer les clients autorisés dans le fichier de configuration de service hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-295">Configure Allowed clients in hello service configuration file</span></span>
<span data-ttu-id="6e5f1-296">Mettre à jour la valeur hello hello suivant paramètre dans le fichier de configuration de service hello avec une liste séparée par des virgules des empreintes numériques de hello de certificats de client hello autorisées du service d’accès toohello :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-296">Update hello value of hello following setting in hello service configuration file with a comma-separated list of hello thumbprints of hello client certificates allowed access toohello service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="6e5f1-297">Configuration de la vérification de révocation des certificats clients</span><span class="sxs-lookup"><span data-stu-id="6e5f1-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="6e5f1-298">paramètre par défaut de Hello ne vérifie pas avec hello autorité de Certification pour l’état de révocation du certificat client.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-298">hello default setting does not check with hello Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="6e5f1-299">tooturn sur hello vérifie si hello autorité de Certification qui a émis les certificats de client hello prend en charge ce type de contrôle, modifiez les hello suivant paramètre avec l’une des valeurs de hello définies dans hello X509RevocationMode énumération :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-299">tooturn on hello checks, if hello Certification Authority which issued hello client certificates supports such checks, change hello following setting with one of hello values defined in hello X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="6e5f1-300">Création d’un fichier PFX pour un certificat de chiffrement auto-signé</span><span class="sxs-lookup"><span data-stu-id="6e5f1-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="6e5f1-301">Pour un certificat de chiffrement, exécutez :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="6e5f1-302">Personnalisation :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

<span data-ttu-id="6e5f1-303">Entrez le mot de passe et exportez le certificat avec les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="6e5f1-304">Oui, exporter la clé privée de hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-304">Yes, export hello private key</span></span>
* <span data-ttu-id="6e5f1-305">Exporter toutes les propriétés étendues</span><span class="sxs-lookup"><span data-stu-id="6e5f1-305">Export all extended properties</span></span>
* <span data-ttu-id="6e5f1-306">Vous devez mot de passe hello lors du chargement du service de cloud hello certificat toohello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-306">You will need hello password when uploading hello certificate toohello cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="6e5f1-307">Exportation d’un certificat de chiffrement à partir du magasin de certificats</span><span class="sxs-lookup"><span data-stu-id="6e5f1-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="6e5f1-308">Recherchez le certificat</span><span class="sxs-lookup"><span data-stu-id="6e5f1-308">Find certificate</span></span>
* <span data-ttu-id="6e5f1-309">Cliquez sur Actions -> Toutes les tâches -> Exporter...</span><span class="sxs-lookup"><span data-stu-id="6e5f1-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="6e5f1-310">Exportez le certificat dans un fichier .PFX avec les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="6e5f1-311">Oui, exporter la clé privée de hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-311">Yes, export hello private key</span></span>
  * <span data-ttu-id="6e5f1-312">Inclure tous les certificats dans le chemin d’accès de certification hello si possible</span><span class="sxs-lookup"><span data-stu-id="6e5f1-312">Include all certificates in hello certification path if possible</span></span> 
* <span data-ttu-id="6e5f1-313">Exporter toutes les propriétés étendues</span><span class="sxs-lookup"><span data-stu-id="6e5f1-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-toocloud-service"></a><span data-ttu-id="6e5f1-314">Télécharger le service de toocloud de certificat de chiffrement</span><span class="sxs-lookup"><span data-stu-id="6e5f1-314">Upload encryption certificate toocloud service</span></span>
<span data-ttu-id="6e5f1-315">Téléchargez le certificat avec hello existant ou générés. Fichier PFX avec une paire de clés de chiffrement hello :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-315">Upload certificate with hello existing or generated .PFX file with hello encryption key pair:</span></span>

* <span data-ttu-id="6e5f1-316">Entrez hello de mot de passe protège les informations de clé privée hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-316">Enter hello password protecting hello private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="6e5f1-317">Mise à jour du certificat de chiffrement dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="6e5f1-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="6e5f1-318">Mettre à jour la valeur d’empreinte numérique hello Hello suivant les paramètres dans le fichier de configuration de service hello avec l’empreinte numérique hello hello téléchargé toohello cloud du service de certificats :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-318">Update hello thumbprint value of hello following settings in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="6e5f1-319">Opérations courantes de certificat</span><span class="sxs-lookup"><span data-stu-id="6e5f1-319">Common certificate operations</span></span>
* <span data-ttu-id="6e5f1-320">Configurer un certificat SSL de hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-320">Configure hello SSL certificate</span></span>
* <span data-ttu-id="6e5f1-321">Configuration des certificats clients</span><span class="sxs-lookup"><span data-stu-id="6e5f1-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="6e5f1-322">Recherchez le certificat</span><span class="sxs-lookup"><span data-stu-id="6e5f1-322">Find certificate</span></span>
<span data-ttu-id="6e5f1-323">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-323">Follow these steps:</span></span>

1. <span data-ttu-id="6e5f1-324">Exécutez mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="6e5f1-325">Fichier -> Ajouter/supprimer un composant logiciel enfichable...</span><span class="sxs-lookup"><span data-stu-id="6e5f1-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="6e5f1-326">Sélectionnez **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="6e5f1-327">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-327">Click **Add**.</span></span>
5. <span data-ttu-id="6e5f1-328">Choisissez l’emplacement de magasin de certificats hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-328">Choose hello certificate store location.</span></span>
6. <span data-ttu-id="6e5f1-329">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-329">Click **Finish**.</span></span>
7. <span data-ttu-id="6e5f1-330">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-330">Click **OK**.</span></span>
8. <span data-ttu-id="6e5f1-331">Développez les **certificats**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="6e5f1-332">Développez le nœud de magasin de certificat hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-332">Expand hello certificate store node.</span></span>
10. <span data-ttu-id="6e5f1-333">Développez le nœud enfant de certificat hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-333">Expand hello Certificate child node.</span></span>
11. <span data-ttu-id="6e5f1-334">Sélectionnez un certificat dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-334">Select a certificate in hello list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="6e5f1-335">Exportation du certificat</span><span class="sxs-lookup"><span data-stu-id="6e5f1-335">Export certificate</span></span>
<span data-ttu-id="6e5f1-336">Bonjour **Assistant Exportation de certificat**:</span><span class="sxs-lookup"><span data-stu-id="6e5f1-336">In hello **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="6e5f1-337">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-337">Click **Next**.</span></span>
2. <span data-ttu-id="6e5f1-338">Sélectionnez **Oui**, puis **clé privée de hello exportation**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-338">Select **Yes**, then **Export hello private key**.</span></span>
3. <span data-ttu-id="6e5f1-339">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-339">Click **Next**.</span></span>
4. <span data-ttu-id="6e5f1-340">Sélectionnez le format de fichier de sortie souhaité hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-340">Select hello desired output file format.</span></span>
5. <span data-ttu-id="6e5f1-341">Vérifiez les options hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-341">Check hello desired options.</span></span>
6. <span data-ttu-id="6e5f1-342">Vérifiez le **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-342">Check **Password**.</span></span>
7. <span data-ttu-id="6e5f1-343">Entrez un mot de passe fort et confirmez-le.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="6e5f1-344">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-344">Click **Next**.</span></span>
9. <span data-ttu-id="6e5f1-345">Tapez ou recherchez un nom de fichier où toostore hello certificat (utilisez un. Extension PFX).</span><span class="sxs-lookup"><span data-stu-id="6e5f1-345">Type or browse a filename where toostore hello certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="6e5f1-346">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-346">Click **Next**.</span></span>
11. <span data-ttu-id="6e5f1-347">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-347">Click **Finish**.</span></span>
12. <span data-ttu-id="6e5f1-348">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="6e5f1-349">Importation d’un certificat</span><span class="sxs-lookup"><span data-stu-id="6e5f1-349">Import certificate</span></span>
<span data-ttu-id="6e5f1-350">Bonjour Assistant Importation de certificat :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-350">In hello Certificate Import Wizard:</span></span>

1. <span data-ttu-id="6e5f1-351">Sélectionnez l’emplacement du magasin hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-351">Select hello store location.</span></span>
   
   * <span data-ttu-id="6e5f1-352">Sélectionnez **utilisateur actuel** si seuls les processus qui s’exécutent sous utilisateur actuel accède au service hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-352">Select **Current User** if only processes running under current user will access hello service</span></span>
   * <span data-ttu-id="6e5f1-353">Sélectionnez **Machine locale** si d’autres processus sur cet ordinateur accède au service hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-353">Select **Local Machine** if other processes in this computer will access hello service</span></span>
2. <span data-ttu-id="6e5f1-354">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-354">Click **Next**.</span></span>
3. <span data-ttu-id="6e5f1-355">Si l’importation à partir d’un fichier, vérifiez le chemin d’accès du fichier hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-355">If importing from a file, confirm hello file path.</span></span>
4. <span data-ttu-id="6e5f1-356">Si vous importez depuis un fichier .PFX :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="6e5f1-357">Entrez hello de mot de passe protège la clé privée de hello</span><span class="sxs-lookup"><span data-stu-id="6e5f1-357">Enter hello password protecting hello private key</span></span>
   2. <span data-ttu-id="6e5f1-358">Sélectionnez les options d’importation</span><span class="sxs-lookup"><span data-stu-id="6e5f1-358">Select import options</span></span>
5. <span data-ttu-id="6e5f1-359">Sélectionnez « Place » certificats hello suivant du magasin</span><span class="sxs-lookup"><span data-stu-id="6e5f1-359">Select "Place" certificates in hello following store</span></span>
6. <span data-ttu-id="6e5f1-360">Cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-360">Click **Browse**.</span></span>
7. <span data-ttu-id="6e5f1-361">Sélectionnez le magasin de votre choix hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-361">Select hello desired store.</span></span>
8. <span data-ttu-id="6e5f1-362">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="6e5f1-363">Si le magasin d’autorité de Certification racine de confiance hello a été choisie, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-363">If hello Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="6e5f1-364">Cliquez sur **OK** dans toutes les fenêtres des boîtes de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="6e5f1-365">Téléchargement d’un certificat</span><span class="sxs-lookup"><span data-stu-id="6e5f1-365">Upload certificate</span></span>
<span data-ttu-id="6e5f1-366">Bonjour [portail Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="6e5f1-366">In hello [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="6e5f1-367">Sélectionnez **Services Cloud**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="6e5f1-368">Sélectionnez le service de cloud computing hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-368">Select hello cloud service.</span></span>
3. <span data-ttu-id="6e5f1-369">Dans le menu supérieur de hello, cliquez sur **certificats**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-369">On hello top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="6e5f1-370">Dans la barre inférieure de hello, cliquez sur **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-370">On hello bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="6e5f1-371">Sélectionnez le fichier de certificat hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-371">Select hello certificate file.</span></span>
6. <span data-ttu-id="6e5f1-372">Si elle est un. PFX fichier, entrez le mot de passe de hello pour la clé privée de hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-372">If it is a .PFX file, enter hello password for hello private key.</span></span>
7. <span data-ttu-id="6e5f1-373">Une fois terminé, copiez l’empreinte numérique du certificat hello hello nouvelle entrée dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-373">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="6e5f1-374">Autres considérations liées à la sécurité</span><span class="sxs-lookup"><span data-stu-id="6e5f1-374">Other security considerations</span></span>
<span data-ttu-id="6e5f1-375">les paramètres de SSL Hello décrites dans ce document chiffrement la communication entre hello service et ses clients lorsque le point de terminaison hello HTTPS est utilisé.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-375">hello SSL settings described in this document encrypt communication between hello service and its clients when hello HTTPS endpoint is used.</span></span> <span data-ttu-id="6e5f1-376">Ceci est important, car les informations d’identification pour l’accès de la base de données et éventuellement d’autres informations sensibles sont contenues dans une communication hello.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-376">This is important since credentials for database access and potentially other sensitive information are contained in hello communication.</span></span> <span data-ttu-id="6e5f1-377">Toutefois, notez que le service de hello persiste état interne, y compris les informations d’identification, dans ses tables internes de la base de données SQL Microsoft Azure hello que vous avez fournies pour le stockage des métadonnées dans votre abonnement Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-377">Note, however, that hello service persists internal status, including credentials, in its internal tables in hello Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="6e5f1-378">Cette base de données a été défini en tant que partie de hello suivant paramètre dans votre fichier de configuration de service (. Fichier CSCFG) :</span><span class="sxs-lookup"><span data-stu-id="6e5f1-378">That database was defined as part of hello following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="6e5f1-379">Les informations d’identification stockées dans cette base de données sont chiffrées.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="6e5f1-380">Toutefois, en tant que meilleure pratique, assurez-vous que les rôles web et de travail de vos déploiements de service sont conservés les toodate et sécurisée en tant qu’ils ont tous deux accès toohello métadonnées de base de données et hello certificat utilisé pour le chiffrement et le déchiffrement des informations d’identification stockées.</span><span class="sxs-lookup"><span data-stu-id="6e5f1-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up toodate and secure as they both have access toohello metadata database and hello certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

