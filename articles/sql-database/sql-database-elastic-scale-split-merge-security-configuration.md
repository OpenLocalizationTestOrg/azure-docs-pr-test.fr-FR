---
title: "Configuration de la sécurité du fractionnement et de la fusion | Microsoft Docs"
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
ms.openlocfilehash: 7e6ccf51a4b75eef16a7df5c1a1018954af8e5dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="7eddc-103">Configuration de la sécurité du fractionnement et de la fusion</span><span class="sxs-lookup"><span data-stu-id="7eddc-103">Split-merge security configuration</span></span>
<span data-ttu-id="7eddc-104">Pour utiliser le service de fusion et de fractionnement, vous devez configurer correctement la sécurité.</span><span class="sxs-lookup"><span data-stu-id="7eddc-104">To use the Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="7eddc-105">Ce service fait partie de la fonctionnalité d’infrastructure élastique de la base de données SQL Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7eddc-105">The service is part of the Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="7eddc-106">Pour plus d’informations, consultez le [didacticiel sur le service de fusion et de fractionnement de l’infrastructure élastique](sql-database-elastic-scale-configure-deploy-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="7eddc-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="7eddc-107">Configuration des certificats</span><span class="sxs-lookup"><span data-stu-id="7eddc-107">Configuring certificates</span></span>
<span data-ttu-id="7eddc-108">Les certificats sont configurés de deux manières.</span><span class="sxs-lookup"><span data-stu-id="7eddc-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="7eddc-109">Pour configurer le certificat SSL</span><span class="sxs-lookup"><span data-stu-id="7eddc-109">To Configure the SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="7eddc-110">Pour configurer des certificats clients</span><span class="sxs-lookup"><span data-stu-id="7eddc-110">To Configure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="to-obtain-certificates"></a><span data-ttu-id="7eddc-111">Pour obtenir des certificats</span><span class="sxs-lookup"><span data-stu-id="7eddc-111">To obtain certificates</span></span>
<span data-ttu-id="7eddc-112">Les certificats peuvent être obtenus à partir d’autorités de certification publiques ou du [Service de certificats Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="7eddc-112">Certificates can be obtained from public Certificate Authorities (CAs) or from the [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="7eddc-113">Il s’agit des méthodes préférées pour obtenir des certificats.</span><span class="sxs-lookup"><span data-stu-id="7eddc-113">These are the preferred methods to obtain certificates.</span></span>

<span data-ttu-id="7eddc-114">Si ces options ne sont pas disponibles, vous pouvez générer des **certificats auto-signés**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-to-generate-certificates"></a><span data-ttu-id="7eddc-115">Outils de génération de certificats</span><span class="sxs-lookup"><span data-stu-id="7eddc-115">Tools to generate certificates</span></span>
* [<span data-ttu-id="7eddc-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="7eddc-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="7eddc-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="7eddc-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="to-run-the-tools"></a><span data-ttu-id="7eddc-118">Pour exécuter les outils</span><span class="sxs-lookup"><span data-stu-id="7eddc-118">To run the tools</span></span>
* <span data-ttu-id="7eddc-119">Depuis une invite de commandes développeur pour Visual Studio, consultez la rubrique [Invite de commandes Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx)</span><span class="sxs-lookup"><span data-stu-id="7eddc-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="7eddc-120">Si installée, accédez à :</span><span class="sxs-lookup"><span data-stu-id="7eddc-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="7eddc-121">Obtenez le kit WDK de [Windows 8.1 : téléchargement des kits et outils](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="7eddc-121">Get the WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="to-configure-the-ssl-certificate"></a><span data-ttu-id="7eddc-122">Pour configurer le certificat SSL</span><span class="sxs-lookup"><span data-stu-id="7eddc-122">To configure the SSL certificate</span></span>
<span data-ttu-id="7eddc-123">Un certificat SSL est nécessaire pour chiffrer les communications et authentifier le serveur.</span><span class="sxs-lookup"><span data-stu-id="7eddc-123">A SSL certificate is required to encrypt the communication and authenticate the server.</span></span> <span data-ttu-id="7eddc-124">Choisissez le plus approprié des trois scénarios ci-dessous et exécutez toutes les étapes associées :</span><span class="sxs-lookup"><span data-stu-id="7eddc-124">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="7eddc-125">Création d’un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="7eddc-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="7eddc-126">Création d’un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="7eddc-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="7eddc-127">Création d’un fichier PFX pour un certificat SSL auto-signé</span><span class="sxs-lookup"><span data-stu-id="7eddc-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="7eddc-128">Téléchargement du certificat SSL vers le service cloud</span><span class="sxs-lookup"><span data-stu-id="7eddc-128">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="7eddc-129">Mise à jour du certificat SSL dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="7eddc-130">Importation de l’autorité de certification SSL</span><span class="sxs-lookup"><span data-stu-id="7eddc-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="to-use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="7eddc-131">Pour utiliser un certificat existant du magasin de certificats</span><span class="sxs-lookup"><span data-stu-id="7eddc-131">To use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="7eddc-132">Exportation d’un certificat SSL à partir du magasin de certificats</span><span class="sxs-lookup"><span data-stu-id="7eddc-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="7eddc-133">Téléchargement du certificat SSL vers le service cloud</span><span class="sxs-lookup"><span data-stu-id="7eddc-133">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="7eddc-134">Mise à jour du certificat SSL dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="to-use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="7eddc-135">Pour utiliser un certificat existant dans un fichier PFX</span><span class="sxs-lookup"><span data-stu-id="7eddc-135">To use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="7eddc-136">Téléchargement du certificat SSL vers le service cloud</span><span class="sxs-lookup"><span data-stu-id="7eddc-136">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="7eddc-137">Mise à jour du certificat SSL dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="to-configure-client-certificates"></a><span data-ttu-id="7eddc-138">Pour configurer des certificats clients</span><span class="sxs-lookup"><span data-stu-id="7eddc-138">To configure client certificates</span></span>
<span data-ttu-id="7eddc-139">Les certificats clients sont requis pour authentifier les demandes au service.</span><span class="sxs-lookup"><span data-stu-id="7eddc-139">Client certificates are required in order to authenticate requests to the service.</span></span> <span data-ttu-id="7eddc-140">Choisissez le plus approprié des trois scénarios ci-dessous et exécutez toutes les étapes associées :</span><span class="sxs-lookup"><span data-stu-id="7eddc-140">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="7eddc-141">Désactivation des certificats clients</span><span class="sxs-lookup"><span data-stu-id="7eddc-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="7eddc-142">Désactivation de l’authentification par certificat client</span><span class="sxs-lookup"><span data-stu-id="7eddc-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="7eddc-143">Émission de nouveaux certificats clients auto-signés</span><span class="sxs-lookup"><span data-stu-id="7eddc-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="7eddc-144">Création d’une autorité de certification auto-signée</span><span class="sxs-lookup"><span data-stu-id="7eddc-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="7eddc-145">Téléchargement du certificat CA vers le service cloud</span><span class="sxs-lookup"><span data-stu-id="7eddc-145">Upload CA Certificate to Cloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="7eddc-146">Mise à jour du certificat CA dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="7eddc-147">Émission de certificats clients</span><span class="sxs-lookup"><span data-stu-id="7eddc-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="7eddc-148">Création de fichiers PFX pour les certificats clients</span><span class="sxs-lookup"><span data-stu-id="7eddc-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="7eddc-149">Importation d’un certificat client</span><span class="sxs-lookup"><span data-stu-id="7eddc-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="7eddc-150">Copie des empreintes numériques des certificats clients</span><span class="sxs-lookup"><span data-stu-id="7eddc-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="7eddc-151">Configuration des clients autorisés dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-151">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="7eddc-152">Utilisation de certificats clients existants</span><span class="sxs-lookup"><span data-stu-id="7eddc-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="7eddc-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="7eddc-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="7eddc-154">Téléchargement du certificat CA vers le service cloud</span><span class="sxs-lookup"><span data-stu-id="7eddc-154">Upload CA Certificate to Cloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="7eddc-155">Mise à jour du certificat CA dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="7eddc-156">Copie des empreintes numériques des certificats clients</span><span class="sxs-lookup"><span data-stu-id="7eddc-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="7eddc-157">Configuration des clients autorisés dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-157">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="7eddc-158">Configuration de la vérification de révocation des certificats clients</span><span class="sxs-lookup"><span data-stu-id="7eddc-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="7eddc-159">Adresses IP autorisées</span><span class="sxs-lookup"><span data-stu-id="7eddc-159">Allowed IP addresses</span></span>
<span data-ttu-id="7eddc-160">L’accès aux points de terminaison de service peut être limité à des plages d’adresses IP spécifiques.</span><span class="sxs-lookup"><span data-stu-id="7eddc-160">Access to the service endpoints can be restricted to specific ranges of IP addresses.</span></span>

## <a name="to-configure-encryption-for-the-store"></a><span data-ttu-id="7eddc-161">Pour configurer le cryptage pour le magasin</span><span class="sxs-lookup"><span data-stu-id="7eddc-161">To configure encryption for the store</span></span>
<span data-ttu-id="7eddc-162">Un certificat est nécessaire pour chiffrer les informations d’identification stockées dans le magasin de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="7eddc-162">A certificate is required to encrypt the credentials that are stored in the metadata store.</span></span> <span data-ttu-id="7eddc-163">Choisissez le plus approprié des trois scénarios ci-dessous et exécutez toutes les étapes associées :</span><span class="sxs-lookup"><span data-stu-id="7eddc-163">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="7eddc-164">Utilisation d’un nouveau certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="7eddc-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="7eddc-165">Création d’un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="7eddc-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="7eddc-166">Création d’un fichier PFX pour un certificat de chiffrement auto-signé</span><span class="sxs-lookup"><span data-stu-id="7eddc-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="7eddc-167">Téléchargement du certificat de chiffrement vers le service cloud</span><span class="sxs-lookup"><span data-stu-id="7eddc-167">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="7eddc-168">Mise à jour du certificat de chiffrement dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="7eddc-169">Utilisation d’un certificat existant du magasin de certificats</span><span class="sxs-lookup"><span data-stu-id="7eddc-169">Use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="7eddc-170">Exportation d’un certificat de chiffrement à partir du magasin de certificats</span><span class="sxs-lookup"><span data-stu-id="7eddc-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="7eddc-171">Téléchargement du certificat de chiffrement vers le service cloud</span><span class="sxs-lookup"><span data-stu-id="7eddc-171">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="7eddc-172">Mise à jour du certificat de chiffrement dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="7eddc-173">Utilisation d’un certificat existant dans un fichier PFX</span><span class="sxs-lookup"><span data-stu-id="7eddc-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="7eddc-174">Téléchargement du certificat de chiffrement vers le service cloud</span><span class="sxs-lookup"><span data-stu-id="7eddc-174">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="7eddc-175">Mise à jour du certificat de chiffrement dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="the-default-configuration"></a><span data-ttu-id="7eddc-176">Configuration par défaut</span><span class="sxs-lookup"><span data-stu-id="7eddc-176">The default configuration</span></span>
<span data-ttu-id="7eddc-177">La configuration par défaut refuse tout accès au point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="7eddc-177">The default configuration denies all access to the HTTP endpoint.</span></span> <span data-ttu-id="7eddc-178">Il s’agit du paramètre recommandé, puisque les demandes pour ces points de terminaison peuvent comporter des informations sensibles comme les informations d’identification de la base de données.</span><span class="sxs-lookup"><span data-stu-id="7eddc-178">This is the recommended setting, since the requests to these endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="7eddc-179">La configuration par défaut accepte tout accès au point de terminaison HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7eddc-179">The default configuration allows all access to the HTTPS endpoint.</span></span> <span data-ttu-id="7eddc-180">Ce paramètre peut être restreint davantage.</span><span class="sxs-lookup"><span data-stu-id="7eddc-180">This setting may be restricted further.</span></span>

### <a name="changing-the-configuration"></a><span data-ttu-id="7eddc-181">Modification de la configuration</span><span class="sxs-lookup"><span data-stu-id="7eddc-181">Changing the Configuration</span></span>
<span data-ttu-id="7eddc-182">Le groupe de règles de contrôle d’accès qui s’appliquent à un point de terminaison est configuré dans la section **<EndpointAcls>** du **fichier de configuration de service**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-182">The group of access control rules that apply to and endpoint are configured in the **<EndpointAcls>** section in the **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="7eddc-183">Les règles dans un groupe de contrôle d’accès sont configurées dans une section <AccessControl name=""> du fichier de configuration du service.</span><span class="sxs-lookup"><span data-stu-id="7eddc-183">The rules in an access control group are configured in a <AccessControl name=""> section of the service configuration file.</span></span> 

<span data-ttu-id="7eddc-184">Le format est expliqué dans la documentation de listes de contrôle d’accès réseau.</span><span class="sxs-lookup"><span data-stu-id="7eddc-184">The format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="7eddc-185">Par exemple, pour autoriser uniquement les adresses IP de la plage 100.100.0.0 à 100.100.255.255 à accéder au point de terminaison HTTPS, les règles ressembleraient à ceci :</span><span class="sxs-lookup"><span data-stu-id="7eddc-185">For example, to allow only IPs in the range 100.100.0.0 to 100.100.255.255 to access the HTTPS endpoint, the rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="7eddc-186">Prévention du déni de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-186">Denial of service prevention</span></span>
<span data-ttu-id="7eddc-187">Il existe deux mécanismes différents pris en charge pour détecter et prévenir les attaques par déni de service :</span><span class="sxs-lookup"><span data-stu-id="7eddc-187">There are two different mechanisms supported to detect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="7eddc-188">Limiter le nombre de demandes simultanées par hôte distant (désactivé par défaut)</span><span class="sxs-lookup"><span data-stu-id="7eddc-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="7eddc-189">Limiter le taux d’accès par hôte distant (activé par défaut)</span><span class="sxs-lookup"><span data-stu-id="7eddc-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="7eddc-190">Ces mécanismes sont basés sur les fonctionnalités plus longuement documentées dans la rubrique Sécurité IP dynamique dans IIS.</span><span class="sxs-lookup"><span data-stu-id="7eddc-190">These are based on the features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="7eddc-191">Lors de la modification de cette configuration, soyez attentif aux facteurs suivants :</span><span class="sxs-lookup"><span data-stu-id="7eddc-191">When changing this configuration beware of the following factors:</span></span>

* <span data-ttu-id="7eddc-192">Le comportement des proxys et des appareils de traduction d’adresses réseau sur les informations de l’hôte distant</span><span class="sxs-lookup"><span data-stu-id="7eddc-192">The behavior of proxies and Network Address Translation devices over the remote host information</span></span>
* <span data-ttu-id="7eddc-193">Chaque demande à une ressource du rôle web est prise en compte (par exemple, le chargement de scripts, les images, etc.)</span><span class="sxs-lookup"><span data-stu-id="7eddc-193">Each request to any resource in the web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="7eddc-194">Limitation du nombre d'accès simultanés</span><span class="sxs-lookup"><span data-stu-id="7eddc-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="7eddc-195">Les paramètres qui configurent ce comportement sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="7eddc-195">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="7eddc-196">Modifiez DynamicIpRestrictionDenyByConcurrentRequests sur true pour activer cette protection.</span><span class="sxs-lookup"><span data-stu-id="7eddc-196">Change DynamicIpRestrictionDenyByConcurrentRequests to true to enable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="7eddc-197">Restriction du taux d’accès</span><span class="sxs-lookup"><span data-stu-id="7eddc-197">Restricting rate of access</span></span>
<span data-ttu-id="7eddc-198">Les paramètres qui configurent ce comportement sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="7eddc-198">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-the-response-to-a-denied-request"></a><span data-ttu-id="7eddc-199">Configuration de la réponse à une demande refusée</span><span class="sxs-lookup"><span data-stu-id="7eddc-199">Configuring the response to a denied request</span></span>
<span data-ttu-id="7eddc-200">Le paramètre suivant configure la réponse à une demande refusée :</span><span class="sxs-lookup"><span data-stu-id="7eddc-200">The following setting configures the response to a denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="7eddc-201">Reportez-vous à la documentation relative à la sécurité IP dynamique dans IIS pour les autres valeurs prises en charge.</span><span class="sxs-lookup"><span data-stu-id="7eddc-201">Refer to the documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="7eddc-202">Opérations de configuration des certificats de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="7eddc-203">Cette rubrique sert de référence uniquement.</span><span class="sxs-lookup"><span data-stu-id="7eddc-203">This topic is for reference only.</span></span> <span data-ttu-id="7eddc-204">Suivez les étapes de configuration décrites dans :</span><span class="sxs-lookup"><span data-stu-id="7eddc-204">Please follow the configuration steps outlined in:</span></span>

* <span data-ttu-id="7eddc-205">Configuration du certificat SSL</span><span class="sxs-lookup"><span data-stu-id="7eddc-205">Configure the SSL certificate</span></span>
* <span data-ttu-id="7eddc-206">Configuration des certificats clients</span><span class="sxs-lookup"><span data-stu-id="7eddc-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="7eddc-207">Création d’un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="7eddc-207">Create a self-signed certificate</span></span>
<span data-ttu-id="7eddc-208">Exécutez :</span><span class="sxs-lookup"><span data-stu-id="7eddc-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="7eddc-209">Pour personnaliser :</span><span class="sxs-lookup"><span data-stu-id="7eddc-209">To customize:</span></span>

* <span data-ttu-id="7eddc-210">-n avec l’URL du service.</span><span class="sxs-lookup"><span data-stu-id="7eddc-210">-n with the service URL.</span></span> <span data-ttu-id="7eddc-211">Les caractères génériques (CN=*.cloudapp.net) et d’autres noms (CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net) sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7eddc-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="7eddc-212">-e avec la date d'expiration du certificat Créez un mot de passe fort et spécifiez-le lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="7eddc-212">-e with the certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="7eddc-213">Création d’un fichier PFX pour un certificat SSL auto-signé</span><span class="sxs-lookup"><span data-stu-id="7eddc-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="7eddc-214">Exécutez :</span><span class="sxs-lookup"><span data-stu-id="7eddc-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="7eddc-215">Entrez le mot de passe et exportez le certificat avec les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="7eddc-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="7eddc-216">Oui, exporter la clé privée</span><span class="sxs-lookup"><span data-stu-id="7eddc-216">Yes, export the private key</span></span>
* <span data-ttu-id="7eddc-217">Exporter toutes les propriétés étendues</span><span class="sxs-lookup"><span data-stu-id="7eddc-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="7eddc-218">Exportation d’un certificat SSL à partir du magasin de certificats</span><span class="sxs-lookup"><span data-stu-id="7eddc-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="7eddc-219">Recherchez le certificat</span><span class="sxs-lookup"><span data-stu-id="7eddc-219">Find certificate</span></span>
* <span data-ttu-id="7eddc-220">Cliquez sur Actions -> Toutes les tâches -> Exporter...</span><span class="sxs-lookup"><span data-stu-id="7eddc-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="7eddc-221">Exportez le certificat dans un fichier .PFX avec les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="7eddc-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="7eddc-222">Oui, exporter la clé privée</span><span class="sxs-lookup"><span data-stu-id="7eddc-222">Yes, export the private key</span></span>
  * <span data-ttu-id="7eddc-223">Inclure tous les certificats dans le chemin d’accès de certification si possible *Exporter toutes les propriétés étendues</span><span class="sxs-lookup"><span data-stu-id="7eddc-223">Include all certificates in the certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-to-cloud-service"></a><span data-ttu-id="7eddc-224">Téléchargement du certificat SSL vers le service cloud</span><span class="sxs-lookup"><span data-stu-id="7eddc-224">Upload SSL certificate to cloud service</span></span>
<span data-ttu-id="7eddc-225">Téléchargez le certificat avec le fichier .PFX existant ou généré avec la paire de clés SSL :</span><span class="sxs-lookup"><span data-stu-id="7eddc-225">Upload certificate with the existing or generated .PFX file with the SSL key pair:</span></span>

* <span data-ttu-id="7eddc-226">Entrez le mot de passe protégeant les informations de clés privées</span><span class="sxs-lookup"><span data-stu-id="7eddc-226">Enter the password protecting the private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="7eddc-227">Mise à jour du certificat SSL dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="7eddc-228">Mettez à jour la valeur de l’empreinte numérique du paramètre suivant du fichier de configuration de service avec l’empreinte numérique du certificat téléchargé vers le service cloud :</span><span class="sxs-lookup"><span data-stu-id="7eddc-228">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="7eddc-229">Importation de l’autorité de certification SSL</span><span class="sxs-lookup"><span data-stu-id="7eddc-229">Import SSL certification authority</span></span>
<span data-ttu-id="7eddc-230">Suivez les étapes suivantes pour tous les comptes/ordinateurs qui communiquent avec le service :</span><span class="sxs-lookup"><span data-stu-id="7eddc-230">Follow these steps in all account/machine that will communicate with the service:</span></span>

* <span data-ttu-id="7eddc-231">Double-cliquez sur le fichier .CER dans l'Explorateur Windows</span><span class="sxs-lookup"><span data-stu-id="7eddc-231">Double-click the .CER file in Windows Explorer</span></span>
* <span data-ttu-id="7eddc-232">Dans la boîte de dialogue Certificat, cliquez sur Installer le certificat...</span><span class="sxs-lookup"><span data-stu-id="7eddc-232">In the Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="7eddc-233">Importez le certificat dans le magasin racine des autorités de certification approuvées</span><span class="sxs-lookup"><span data-stu-id="7eddc-233">Import certificate into the Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="7eddc-234">Désactivation de l’authentification par certificat client</span><span class="sxs-lookup"><span data-stu-id="7eddc-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="7eddc-235">Seule l’authentification par certificat client est prise en charge et sa désactivation permet l’accès public aux points de terminaison de service, à moins que d’autres mécanismes soient en place (par exemple, Microsoft Azure Virtual Network).</span><span class="sxs-lookup"><span data-stu-id="7eddc-235">Only client certificate-based authentication is supported and disabling it will allow for public access to the service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="7eddc-236">Définissez les paramètres suivants sur false dans le fichier de configuration de service pour désactiver la fonctionnalité :</span><span class="sxs-lookup"><span data-stu-id="7eddc-236">Change these settings to false in the service configuration file to turn the feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="7eddc-237">Ensuite, copiez la même empreinte numérique que celle du certificat SSL dans le paramètre du certificat de l’autorité de certification :</span><span class="sxs-lookup"><span data-stu-id="7eddc-237">Then, copy the same thumbprint as the SSL certificate in the CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="7eddc-238">Création d’une autorité de certification auto-signée</span><span class="sxs-lookup"><span data-stu-id="7eddc-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="7eddc-239">Exécutez les étapes suivantes pour créer un certificat auto-signé qui agit comme une autorité de certification :</span><span class="sxs-lookup"><span data-stu-id="7eddc-239">Execute the following steps to create a self-signed certificate to act as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="7eddc-240">Pour le personnaliser</span><span class="sxs-lookup"><span data-stu-id="7eddc-240">To customize it</span></span>

* <span data-ttu-id="7eddc-241">-e avec la date d’expiration du certificat</span><span class="sxs-lookup"><span data-stu-id="7eddc-241">-e with the certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="7eddc-242">Recherche de la clé publique de l’autorité de certification</span><span class="sxs-lookup"><span data-stu-id="7eddc-242">Find CA public key</span></span>
<span data-ttu-id="7eddc-243">Tous les certificats clients doivent avoir été émis par une autorité de certification approuvée par le service.</span><span class="sxs-lookup"><span data-stu-id="7eddc-243">All client certificates must have been issued by a Certification Authority trusted by the service.</span></span> <span data-ttu-id="7eddc-244">Recherchez la clé publique d’accès à l’autorité de certification qui a émis les certificats clients qui seront utilisés pour l’authentification afin de la télécharger vers le service cloud.</span><span class="sxs-lookup"><span data-stu-id="7eddc-244">Find the public key to the Certification Authority that issued the client certificates that are going to be used for authentication in order to upload it to the cloud service.</span></span>

<span data-ttu-id="7eddc-245">Si le fichier comportant la clé publique n’est pas disponible, exportez-le à partir du magasin de certificats :</span><span class="sxs-lookup"><span data-stu-id="7eddc-245">If the file with the public key is not available, export it from the certificate store:</span></span>

* <span data-ttu-id="7eddc-246">Recherchez le certificat</span><span class="sxs-lookup"><span data-stu-id="7eddc-246">Find certificate</span></span>
  * <span data-ttu-id="7eddc-247">Recherchez un certificat client émis par la même autorité de certification</span><span class="sxs-lookup"><span data-stu-id="7eddc-247">Search for a client certificate issued by the same Certification Authority</span></span>
* <span data-ttu-id="7eddc-248">Double-cliquez sur le certificat.</span><span class="sxs-lookup"><span data-stu-id="7eddc-248">Double-click the certificate.</span></span>
* <span data-ttu-id="7eddc-249">Sélectionnez l’onglet Chemin d’accès de certification dans la boîte de dialogue Certificat.</span><span class="sxs-lookup"><span data-stu-id="7eddc-249">Select the Certification Path tab in the Certificate dialog.</span></span>
* <span data-ttu-id="7eddc-250">Double-cliquez sur l’entrée de l’autorité de certification dans le chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="7eddc-250">Double-click the CA entry in the path.</span></span>
* <span data-ttu-id="7eddc-251">Prenez note des propriétés du certificat.</span><span class="sxs-lookup"><span data-stu-id="7eddc-251">Take notes of the certificate properties.</span></span>
* <span data-ttu-id="7eddc-252">Fermez la boîte de dialogue **Certificat** .</span><span class="sxs-lookup"><span data-stu-id="7eddc-252">Close the **Certificate** dialog.</span></span>
* <span data-ttu-id="7eddc-253">Recherchez le certificat</span><span class="sxs-lookup"><span data-stu-id="7eddc-253">Find certificate</span></span>
  * <span data-ttu-id="7eddc-254">Recherchez l’autorité de certification indiquée ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7eddc-254">Search for the CA noted above.</span></span>
* <span data-ttu-id="7eddc-255">Cliquez sur Actions -> Toutes les tâches -> Exporter...</span><span class="sxs-lookup"><span data-stu-id="7eddc-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="7eddc-256">Exportez le certificat dans un fichier .CER avec les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="7eddc-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="7eddc-257">**Non, ne pas exporter la clé privée**</span><span class="sxs-lookup"><span data-stu-id="7eddc-257">**No, do not export the private key**</span></span>
  * <span data-ttu-id="7eddc-258">Inclure tous les certificats dans le chemin d’accès de certification si possible.</span><span class="sxs-lookup"><span data-stu-id="7eddc-258">Include all certificates in the certification path if possible.</span></span>
  * <span data-ttu-id="7eddc-259">Exporter toutes les propriétés étendues.</span><span class="sxs-lookup"><span data-stu-id="7eddc-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-to-cloud-service"></a><span data-ttu-id="7eddc-260">Téléchargement du certificat CA vers le service cloud</span><span class="sxs-lookup"><span data-stu-id="7eddc-260">Upload CA certificate to cloud service</span></span>
<span data-ttu-id="7eddc-261">Téléchargez le certificat avec le fichier .CER existant ou généré avec la clé publique de l’autorité de certification.</span><span class="sxs-lookup"><span data-stu-id="7eddc-261">Upload certificate with the existing or generated .CER file with the CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="7eddc-262">Mise à jour du certificat CA dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="7eddc-263">Mettez à jour la valeur de l’empreinte numérique du paramètre suivant du fichier de configuration de service avec l’empreinte numérique du certificat téléchargé vers le service cloud :</span><span class="sxs-lookup"><span data-stu-id="7eddc-263">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="7eddc-264">Mettez à jour la valeur du paramètre suivant avec la même empreinte numérique :</span><span class="sxs-lookup"><span data-stu-id="7eddc-264">Update the value of the following setting with the same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="7eddc-265">Émission de certificats clients</span><span class="sxs-lookup"><span data-stu-id="7eddc-265">Issue client certificates</span></span>
<span data-ttu-id="7eddc-266">Chaque personne autorisée à accéder au service doit être dotée d’un certificat client émis pour son utilisation exclusive et doit choisir un mot de passe fort pour protéger sa clé privée.</span><span class="sxs-lookup"><span data-stu-id="7eddc-266">Each individual authorized to access the service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password to protect its private key.</span></span> 

<span data-ttu-id="7eddc-267">Les étapes suivantes doivent être exécutées sur l’ordinateur sur lequel le certificat auto-signé de l’autorité de certification a été généré et stocké :</span><span class="sxs-lookup"><span data-stu-id="7eddc-267">The following steps must be executed in the same machine where the self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="7eddc-268">Personnalisation :</span><span class="sxs-lookup"><span data-stu-id="7eddc-268">Customizing:</span></span>

* <span data-ttu-id="7eddc-269">-n avec un identifiant client qui sera authentifié avec ce certificat</span><span class="sxs-lookup"><span data-stu-id="7eddc-269">-n with an ID for to the client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="7eddc-270">-e avec la date d'expiration du certificat</span><span class="sxs-lookup"><span data-stu-id="7eddc-270">-e with the certificate expiration date</span></span>
* <span data-ttu-id="7eddc-271">MyID.pvk et MyID.cer avec des noms de fichier uniques pour ce certificat client</span><span class="sxs-lookup"><span data-stu-id="7eddc-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="7eddc-272">Cette commande vous demande de créer un mot de passe et de l’utiliser une seule fois.</span><span class="sxs-lookup"><span data-stu-id="7eddc-272">This command will prompt for a password to be created and then used once.</span></span> <span data-ttu-id="7eddc-273">Utilisez un mot de passe fort.</span><span class="sxs-lookup"><span data-stu-id="7eddc-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="7eddc-274">Création de fichiers PFX pour les certificats clients</span><span class="sxs-lookup"><span data-stu-id="7eddc-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="7eddc-275">Pour chaque certificat client généré, exécutez :</span><span class="sxs-lookup"><span data-stu-id="7eddc-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="7eddc-276">Personnalisation :</span><span class="sxs-lookup"><span data-stu-id="7eddc-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the client certificate

<span data-ttu-id="7eddc-277">Entrez le mot de passe et exportez le certificat avec les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="7eddc-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="7eddc-278">Oui, exporter la clé privée</span><span class="sxs-lookup"><span data-stu-id="7eddc-278">Yes, export the private key</span></span>
* <span data-ttu-id="7eddc-279">Exporter toutes les propriétés étendues</span><span class="sxs-lookup"><span data-stu-id="7eddc-279">Export all extended properties</span></span>
* <span data-ttu-id="7eddc-280">La personne pour laquelle ce certificat a été émis doit choisir le mot de passe d’exportation</span><span class="sxs-lookup"><span data-stu-id="7eddc-280">The individual to whom this certificate is being issued should choose the export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="7eddc-281">Importation d’un certificat client</span><span class="sxs-lookup"><span data-stu-id="7eddc-281">Import client certificate</span></span>
<span data-ttu-id="7eddc-282">Chaque personne pour laquelle un certificat client a été émis doit importer la paire de clés dans les ordinateurs qu’elle utilise pour communiquer avec le service :</span><span class="sxs-lookup"><span data-stu-id="7eddc-282">Each individual for whom a client certificate has been issued should import the key pair in the machines he/she will use to communicate with the service:</span></span>

* <span data-ttu-id="7eddc-283">Double-cliquez sur le fichier .PFX dans l'Explorateur Windows</span><span class="sxs-lookup"><span data-stu-id="7eddc-283">Double-click the .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="7eddc-284">Importez un certificat dans le magasin Personnel avec au moins l'option suivante :</span><span class="sxs-lookup"><span data-stu-id="7eddc-284">Import certificate into the Personal store with at least this option:</span></span>
  * <span data-ttu-id="7eddc-285">Inclure toutes les propriétés étendues activées</span><span class="sxs-lookup"><span data-stu-id="7eddc-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="7eddc-286">Copie des empreintes numériques des certificats clients</span><span class="sxs-lookup"><span data-stu-id="7eddc-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="7eddc-287">Chaque personne pour laquelle un certificat client a été émis doit suivre les étapes ci-dessous afin d'obtenir l'empreinte numérique de son certificat qui sera ajoutée au fichier de configuration de service :</span><span class="sxs-lookup"><span data-stu-id="7eddc-287">Each individual for whom a client certificate has been issued must follow these steps in order to obtain the thumbprint of his/hers certificate which will be added to the service configuration file:</span></span>

* <span data-ttu-id="7eddc-288">Exécutez certmgr.exe</span><span class="sxs-lookup"><span data-stu-id="7eddc-288">Run certmgr.exe</span></span>
* <span data-ttu-id="7eddc-289">Sélectionnez l'onglet Personnel</span><span class="sxs-lookup"><span data-stu-id="7eddc-289">Select the Personal tab</span></span>
* <span data-ttu-id="7eddc-290">Double-cliquez sur le certificat client à utiliser pour l'authentification</span><span class="sxs-lookup"><span data-stu-id="7eddc-290">Double-click the client certificate to be used for authentication</span></span>
* <span data-ttu-id="7eddc-291">Dans la boîte de dialogue Certificat qui s'ouvre, sélectionnez l'onglet Détails</span><span class="sxs-lookup"><span data-stu-id="7eddc-291">In the Certificate dialog that opens, select the Details tab</span></span>
* <span data-ttu-id="7eddc-292">Veillez à ce que l'option Afficher indique Tous</span><span class="sxs-lookup"><span data-stu-id="7eddc-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="7eddc-293">Sélectionnez le champ nommé Empreinte numérique dans la liste</span><span class="sxs-lookup"><span data-stu-id="7eddc-293">Select the field named Thumbprint in the list</span></span>
* <span data-ttu-id="7eddc-294">Copiez la valeur de l’empreinte numérique ** Supprimez les caractères Unicode non visibles devant le premier chiffre ** Supprimez tous les espaces</span><span class="sxs-lookup"><span data-stu-id="7eddc-294">Copy the value of the thumbprint ** Delete non-visible Unicode characters in front of the first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-the-service-configuration-file"></a><span data-ttu-id="7eddc-295">Configuration des clients autorisés dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-295">Configure Allowed clients in the service configuration file</span></span>
<span data-ttu-id="7eddc-296">Mettez à jour la valeur du paramètre suivant dans le fichier de configuration de service avec une liste séparée par des virgules des empreintes numériques des certificats clients autorisés à accéder au service :</span><span class="sxs-lookup"><span data-stu-id="7eddc-296">Update the value of the following setting in the service configuration file with a comma-separated list of the thumbprints of the client certificates allowed access to the service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="7eddc-297">Configuration de la vérification de révocation des certificats clients</span><span class="sxs-lookup"><span data-stu-id="7eddc-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="7eddc-298">Le paramètre par défaut ne vérifie pas l’état de révocation du certificat client auprès de l’autorité de certification.</span><span class="sxs-lookup"><span data-stu-id="7eddc-298">The default setting does not check with the Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="7eddc-299">Pour activer les vérifications, si l’autorité de certification qui a émis les certificats clients prend en charge ces vérifications, définissez le paramètre suivant avec l’une des valeurs définies dans l’énumération X509RevocationMode :</span><span class="sxs-lookup"><span data-stu-id="7eddc-299">To turn on the checks, if the Certification Authority which issued the client certificates supports such checks, change the following setting with one of the values defined in the X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="7eddc-300">Création d’un fichier PFX pour un certificat de chiffrement auto-signé</span><span class="sxs-lookup"><span data-stu-id="7eddc-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="7eddc-301">Pour un certificat de chiffrement, exécutez :</span><span class="sxs-lookup"><span data-stu-id="7eddc-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="7eddc-302">Personnalisation :</span><span class="sxs-lookup"><span data-stu-id="7eddc-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the encryption certificate

<span data-ttu-id="7eddc-303">Entrez le mot de passe et exportez le certificat avec les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="7eddc-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="7eddc-304">Oui, exporter la clé privée</span><span class="sxs-lookup"><span data-stu-id="7eddc-304">Yes, export the private key</span></span>
* <span data-ttu-id="7eddc-305">Exporter toutes les propriétés étendues</span><span class="sxs-lookup"><span data-stu-id="7eddc-305">Export all extended properties</span></span>
* <span data-ttu-id="7eddc-306">Vous aurez besoin du mot de passe lors du téléchargement du certificat vers le service cloud.</span><span class="sxs-lookup"><span data-stu-id="7eddc-306">You will need the password when uploading the certificate to the cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="7eddc-307">Exportation d’un certificat de chiffrement à partir du magasin de certificats</span><span class="sxs-lookup"><span data-stu-id="7eddc-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="7eddc-308">Recherchez le certificat</span><span class="sxs-lookup"><span data-stu-id="7eddc-308">Find certificate</span></span>
* <span data-ttu-id="7eddc-309">Cliquez sur Actions -> Toutes les tâches -> Exporter...</span><span class="sxs-lookup"><span data-stu-id="7eddc-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="7eddc-310">Exportez le certificat dans un fichier .PFX avec les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="7eddc-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="7eddc-311">Oui, exporter la clé privée</span><span class="sxs-lookup"><span data-stu-id="7eddc-311">Yes, export the private key</span></span>
  * <span data-ttu-id="7eddc-312">Inclure tous les certificats dans le chemin d’accès de certification si possible</span><span class="sxs-lookup"><span data-stu-id="7eddc-312">Include all certificates in the certification path if possible</span></span> 
* <span data-ttu-id="7eddc-313">Exporter toutes les propriétés étendues</span><span class="sxs-lookup"><span data-stu-id="7eddc-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-to-cloud-service"></a><span data-ttu-id="7eddc-314">Téléchargement du certificat de chiffrement vers le service cloud</span><span class="sxs-lookup"><span data-stu-id="7eddc-314">Upload encryption certificate to cloud service</span></span>
<span data-ttu-id="7eddc-315">Téléchargez le certificat avec le fichier .PFX existant ou généré avec la paire de clés de chiffrement :</span><span class="sxs-lookup"><span data-stu-id="7eddc-315">Upload certificate with the existing or generated .PFX file with the encryption key pair:</span></span>

* <span data-ttu-id="7eddc-316">Entrez le mot de passe protégeant les informations de clés privées</span><span class="sxs-lookup"><span data-stu-id="7eddc-316">Enter the password protecting the private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="7eddc-317">Mise à jour du certificat de chiffrement dans le fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="7eddc-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="7eddc-318">Mettez à jour la valeur de l’empreinte numérique des paramètres suivants du fichier de configuration de service avec l’empreinte numérique du certificat téléchargé vers le service cloud :</span><span class="sxs-lookup"><span data-stu-id="7eddc-318">Update the thumbprint value of the following settings in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="7eddc-319">Opérations courantes de certificat</span><span class="sxs-lookup"><span data-stu-id="7eddc-319">Common certificate operations</span></span>
* <span data-ttu-id="7eddc-320">Configuration du certificat SSL</span><span class="sxs-lookup"><span data-stu-id="7eddc-320">Configure the SSL certificate</span></span>
* <span data-ttu-id="7eddc-321">Configuration des certificats clients</span><span class="sxs-lookup"><span data-stu-id="7eddc-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="7eddc-322">Recherchez le certificat</span><span class="sxs-lookup"><span data-stu-id="7eddc-322">Find certificate</span></span>
<span data-ttu-id="7eddc-323">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="7eddc-323">Follow these steps:</span></span>

1. <span data-ttu-id="7eddc-324">Exécutez mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="7eddc-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="7eddc-325">Fichier -> Ajouter/supprimer un composant logiciel enfichable...</span><span class="sxs-lookup"><span data-stu-id="7eddc-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="7eddc-326">Sélectionnez **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="7eddc-327">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-327">Click **Add**.</span></span>
5. <span data-ttu-id="7eddc-328">Choisissez l’emplacement du magasin de certificats.</span><span class="sxs-lookup"><span data-stu-id="7eddc-328">Choose the certificate store location.</span></span>
6. <span data-ttu-id="7eddc-329">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-329">Click **Finish**.</span></span>
7. <span data-ttu-id="7eddc-330">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-330">Click **OK**.</span></span>
8. <span data-ttu-id="7eddc-331">Développez les **certificats**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="7eddc-332">Développez le nœud du magasin du certificat.</span><span class="sxs-lookup"><span data-stu-id="7eddc-332">Expand the certificate store node.</span></span>
10. <span data-ttu-id="7eddc-333">Développez le nœud enfant du certificat.</span><span class="sxs-lookup"><span data-stu-id="7eddc-333">Expand the Certificate child node.</span></span>
11. <span data-ttu-id="7eddc-334">Sélectionnez un certificat dans la liste.</span><span class="sxs-lookup"><span data-stu-id="7eddc-334">Select a certificate in the list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="7eddc-335">Exportation du certificat</span><span class="sxs-lookup"><span data-stu-id="7eddc-335">Export certificate</span></span>
<span data-ttu-id="7eddc-336">Dans l’ **Assistant Exportation de certificat**:</span><span class="sxs-lookup"><span data-stu-id="7eddc-336">In the **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="7eddc-337">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-337">Click **Next**.</span></span>
2. <span data-ttu-id="7eddc-338">Sélectionnez l’option **Oui**, puis **Exporter la clé privée**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-338">Select **Yes**, then **Export the private key**.</span></span>
3. <span data-ttu-id="7eddc-339">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-339">Click **Next**.</span></span>
4. <span data-ttu-id="7eddc-340">Sélectionnez le format de fichier de sortie souhaité.</span><span class="sxs-lookup"><span data-stu-id="7eddc-340">Select the desired output file format.</span></span>
5. <span data-ttu-id="7eddc-341">Vérifiez les options de votre choix.</span><span class="sxs-lookup"><span data-stu-id="7eddc-341">Check the desired options.</span></span>
6. <span data-ttu-id="7eddc-342">Vérifiez le **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-342">Check **Password**.</span></span>
7. <span data-ttu-id="7eddc-343">Entrez un mot de passe fort et confirmez-le.</span><span class="sxs-lookup"><span data-stu-id="7eddc-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="7eddc-344">Cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-344">Click **Next**.</span></span>
9. <span data-ttu-id="7eddc-345">Tapez ou sélectionnez un nom de fichier dans lequel stocker le certificat (utilisez une extension .PFX).</span><span class="sxs-lookup"><span data-stu-id="7eddc-345">Type or browse a filename where to store the certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="7eddc-346">Cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-346">Click **Next**.</span></span>
11. <span data-ttu-id="7eddc-347">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-347">Click **Finish**.</span></span>
12. <span data-ttu-id="7eddc-348">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="7eddc-349">Importation d’un certificat</span><span class="sxs-lookup"><span data-stu-id="7eddc-349">Import certificate</span></span>
<span data-ttu-id="7eddc-350">Dans l'Assistant Importation de certificat :</span><span class="sxs-lookup"><span data-stu-id="7eddc-350">In the Certificate Import Wizard:</span></span>

1. <span data-ttu-id="7eddc-351">Sélectionnez l’emplacement du magasin.</span><span class="sxs-lookup"><span data-stu-id="7eddc-351">Select the store location.</span></span>
   
   * <span data-ttu-id="7eddc-352">Sélectionnez **Utilisateur actuel** si seuls les processus s’exécutant sous l’utilisateur actuel accèdent au service.</span><span class="sxs-lookup"><span data-stu-id="7eddc-352">Select **Current User** if only processes running under current user will access the service</span></span>
   * <span data-ttu-id="7eddc-353">Sélectionnez **Ordinateur local** si d’autres processus de cet ordinateur accèdent au service</span><span class="sxs-lookup"><span data-stu-id="7eddc-353">Select **Local Machine** if other processes in this computer will access the service</span></span>
2. <span data-ttu-id="7eddc-354">Cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-354">Click **Next**.</span></span>
3. <span data-ttu-id="7eddc-355">Si vous importez depuis un fichier, vérifiez le chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="7eddc-355">If importing from a file, confirm the file path.</span></span>
4. <span data-ttu-id="7eddc-356">Si vous importez depuis un fichier .PFX :</span><span class="sxs-lookup"><span data-stu-id="7eddc-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="7eddc-357">Entrez le mot de passe protégeant la clé privée</span><span class="sxs-lookup"><span data-stu-id="7eddc-357">Enter the password protecting the private key</span></span>
   2. <span data-ttu-id="7eddc-358">Sélectionnez les options d’importation</span><span class="sxs-lookup"><span data-stu-id="7eddc-358">Select import options</span></span>
5. <span data-ttu-id="7eddc-359">Sélectionnez « Placer » les certificats dans le magasin suivant</span><span class="sxs-lookup"><span data-stu-id="7eddc-359">Select "Place" certificates in the following store</span></span>
6. <span data-ttu-id="7eddc-360">Cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-360">Click **Browse**.</span></span>
7. <span data-ttu-id="7eddc-361">Sélectionnez le magasin de votre choix.</span><span class="sxs-lookup"><span data-stu-id="7eddc-361">Select the desired store.</span></span>
8. <span data-ttu-id="7eddc-362">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="7eddc-363">Si le magasin racine des autorités de certification approuvées a été choisi, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-363">If the Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="7eddc-364">Cliquez sur **OK** dans toutes les fenêtres des boîtes de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7eddc-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="7eddc-365">Téléchargement d’un certificat</span><span class="sxs-lookup"><span data-stu-id="7eddc-365">Upload certificate</span></span>
<span data-ttu-id="7eddc-366">Dans le [portail Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="7eddc-366">In the [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="7eddc-367">Sélectionnez **Services Cloud**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="7eddc-368">Sélectionnez le service cloud.</span><span class="sxs-lookup"><span data-stu-id="7eddc-368">Select the cloud service.</span></span>
3. <span data-ttu-id="7eddc-369">Dans le menu supérieur, cliquez sur **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-369">On the top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="7eddc-370">Dans la barre inférieure, cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="7eddc-370">On the bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="7eddc-371">Sélectionnez le fichier de certificat.</span><span class="sxs-lookup"><span data-stu-id="7eddc-371">Select the certificate file.</span></span>
6. <span data-ttu-id="7eddc-372">S’il s’agit d’un fichier .PFX, entrez le mot de passe de la clé privée.</span><span class="sxs-lookup"><span data-stu-id="7eddc-372">If it is a .PFX file, enter the password for the private key.</span></span>
7. <span data-ttu-id="7eddc-373">Lorsque vous avez terminé, copiez l’empreinte de certificat à partir de la nouvelle entrée dans la liste.</span><span class="sxs-lookup"><span data-stu-id="7eddc-373">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="7eddc-374">Autres considérations liées à la sécurité</span><span class="sxs-lookup"><span data-stu-id="7eddc-374">Other security considerations</span></span>
<span data-ttu-id="7eddc-375">Les paramètres SSL décrits dans ce document chiffrent les communications entre le service et ses clients lorsque le point de terminaison HTTPS est utilisé.</span><span class="sxs-lookup"><span data-stu-id="7eddc-375">The SSL settings described in this document encrypt communication between the service and its clients when the HTTPS endpoint is used.</span></span> <span data-ttu-id="7eddc-376">Ceci est important car les informations d’identification pour l’accès à la base de données, et éventuellement à d’autres informations sensibles, sont contenues dans les communications.</span><span class="sxs-lookup"><span data-stu-id="7eddc-376">This is important since credentials for database access and potentially other sensitive information are contained in the communication.</span></span> <span data-ttu-id="7eddc-377">Notez, néanmoins, que le service conserve l'état interne, y compris les informations d'identification, dans ses tables internes de la base de données SQL Azure de Microsoft que vous avez fournies pour le stockage des métadonnées dans votre abonnement Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7eddc-377">Note, however, that the service persists internal status, including credentials, in its internal tables in the Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="7eddc-378">Cette base de données a été définie dans le paramètre suivant dans votre fichier de configuration de service (fichier .CSCFG) :</span><span class="sxs-lookup"><span data-stu-id="7eddc-378">That database was defined as part of the following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="7eddc-379">Les informations d’identification stockées dans cette base de données sont chiffrées.</span><span class="sxs-lookup"><span data-stu-id="7eddc-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="7eddc-380">Toutefois, il est recommandé de s’assurer que les rôles Web et de travail de vos déploiements de service sont mis à jour et sécurisés, car les deux types de rôle ont accès à la base de données de métadonnées et au certificat utilisé pour le chiffrement et le déchiffrement des informations d’identification stockées.</span><span class="sxs-lookup"><span data-stu-id="7eddc-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up to date and secure as they both have access to the metadata database and the certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

