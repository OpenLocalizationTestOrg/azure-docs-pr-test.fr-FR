---
title: "Résoudre les problèmes concernant la connexion de point à site Azure | Microsoft Docs"
description: "Découvrez comment résoudre les problèmes de connexion de point à site."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: de37c8ffd47a2b8e201d18e3a20b5325d528ad59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="d3df9-103">Résolution des problèmes de connexion de point à site Azure</span><span class="sxs-lookup"><span data-stu-id="d3df9-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="d3df9-104">Cet article répertorie les problèmes de connexion de point à site courants que vous pouvez rencontrer.</span><span class="sxs-lookup"><span data-stu-id="d3df9-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="d3df9-105">Il décrit également les causes probables de ces problèmes, ainsi que les solutions possibles.</span><span class="sxs-lookup"><span data-stu-id="d3df9-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="d3df9-106">Erreur du client VPN : le certificat est introuvable</span><span class="sxs-lookup"><span data-stu-id="d3df9-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="d3df9-107">Symptôme</span><span class="sxs-lookup"><span data-stu-id="d3df9-107">Symptom</span></span>

<span data-ttu-id="d3df9-108">Lorsque vous essayez de vous connecter à un réseau virtuel Azure à l’aide du client VPN, vous recevez le message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="d3df9-108">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="d3df9-109">**Impossible de trouver un certificat qui peut être utilisé avec le protocole EAP (Extensible Authentication Protocol). (Erreur 798)**</span><span class="sxs-lookup"><span data-stu-id="d3df9-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="d3df9-110">Cause :</span><span class="sxs-lookup"><span data-stu-id="d3df9-110">Cause</span></span>

<span data-ttu-id="d3df9-111">Ce problème se produit si le certificat client est absent de **Certificats - Utilisateur actuel\Personnel\Certificats**.</span><span class="sxs-lookup"><span data-stu-id="d3df9-111">This problem occurs if the client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="d3df9-112">Solution</span><span class="sxs-lookup"><span data-stu-id="d3df9-112">Solution</span></span>

<span data-ttu-id="d3df9-113">Vérifiez que le certificat client est bien installé dans le magasin de certificats (Certmgr.msc), à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="d3df9-113">Make sure that the client certificate is installed in the following location of the Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="d3df9-114">**Certificats - Utilisateur actuel\Personnel\Certificats**</span><span class="sxs-lookup"><span data-stu-id="d3df9-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="d3df9-115">Pour en savoir plus sur la façon d’installer le certificat client, consultez la page [Générer et exporter des certificats pour les connexions de point à site](vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="d3df9-115">For more information about how to install the client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d3df9-116">Lorsque vous importez le certificat client, ne sélectionnez pas l’option **Activer la protection renforcée par clé privée**.</span><span class="sxs-lookup"><span data-stu-id="d3df9-116">When you import the client certificate, do not select the **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-the-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="d3df9-117">Erreur du client VPN : le message reçu était inattendu ou formaté de façon incorrecte</span><span class="sxs-lookup"><span data-stu-id="d3df9-117">VPN client error: The message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="d3df9-118">Symptôme</span><span class="sxs-lookup"><span data-stu-id="d3df9-118">Symptom</span></span>

<span data-ttu-id="d3df9-119">Lorsque vous essayez de vous connecter à un réseau virtuel Azure à l’aide du client VPN, vous recevez le message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="d3df9-119">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="d3df9-120">**Le message reçu était inattendu ou formaté de façon incorrecte. (Erreur 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="d3df9-120">**The message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="d3df9-121">Cause :</span><span class="sxs-lookup"><span data-stu-id="d3df9-121">Cause</span></span>

<span data-ttu-id="d3df9-122">Ce problème se produit si la clé publique du certificat racine n’est pas téléchargée dans la passerelle VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="d3df9-122">This problem occurs if the root certificate public key is not uploaded into the Azure VPN gateway.</span></span> <span data-ttu-id="d3df9-123">Il peut également se produire si la clé est endommagée ou a expiré.</span><span class="sxs-lookup"><span data-stu-id="d3df9-123">It can also occur if the key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="d3df9-124">Solution</span><span class="sxs-lookup"><span data-stu-id="d3df9-124">Solution</span></span>

<span data-ttu-id="d3df9-125">Pour résoudre ce problème, vérifiez l’état du certificat racine dans le portail Azure. Vous pourrez voir si le certificat a été révoqué ou non.</span><span class="sxs-lookup"><span data-stu-id="d3df9-125">To resolve this problem, check the status of the root certificate in the Azure portal to see whether it was revoked.</span></span> <span data-ttu-id="d3df9-126">S’il n’est pas révoqué, essayez de supprimer le certificat racine et de le télécharger une nouvelle fois.</span><span class="sxs-lookup"><span data-stu-id="d3df9-126">If it is not revoked, try to delete the root certificate and reupload.</span></span> <span data-ttu-id="d3df9-127">Pour en savoir plus, consultez la section [Créer des certificats](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span><span class="sxs-lookup"><span data-stu-id="d3df9-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="d3df9-128">Erreur du client VPN : une chaîne de certificats a été traitée mais s’est terminée</span><span class="sxs-lookup"><span data-stu-id="d3df9-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="d3df9-129">Symptôme</span><span class="sxs-lookup"><span data-stu-id="d3df9-129">Symptom</span></span> 

<span data-ttu-id="d3df9-130">Lorsque vous essayez de vous connecter à un réseau virtuel Azure à l’aide du client VPN, vous recevez le message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="d3df9-130">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="d3df9-131">**Une chaîne de certificats a été traitée mais s’est terminée par un certificat racine qui n’est pas approuvé par le fournisseur d’approbation.**</span><span class="sxs-lookup"><span data-stu-id="d3df9-131">**A certificate chain processed but terminated in a root certificate which is not trusted by the trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="d3df9-132">Solution</span><span class="sxs-lookup"><span data-stu-id="d3df9-132">Solution</span></span>

1. <span data-ttu-id="d3df9-133">Assurez-vous que les certificats suivants se trouvent au bon emplacement :</span><span class="sxs-lookup"><span data-stu-id="d3df9-133">Make sure that the following certificates are in the correct location:</span></span>

    | <span data-ttu-id="d3df9-134">Certificat</span><span class="sxs-lookup"><span data-stu-id="d3df9-134">Certificate</span></span> | <span data-ttu-id="d3df9-135">Emplacement</span><span class="sxs-lookup"><span data-stu-id="d3df9-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="d3df9-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="d3df9-136">AzureClient.pfx</span></span>  | <span data-ttu-id="d3df9-137">Utilisateur actuel\Personnel\Certificats</span><span class="sxs-lookup"><span data-stu-id="d3df9-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="d3df9-138">Azuregateway-*GUID*.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="d3df9-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="d3df9-139">Utilisateur actuel\Autorités de certification racines de confiance</span><span class="sxs-lookup"><span data-stu-id="d3df9-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="d3df9-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="d3df9-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="d3df9-141">Ordinateur local\Autorités de certification racines de confiance</span><span class="sxs-lookup"><span data-stu-id="d3df9-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="d3df9-142">Si les certificats se trouvent déjà dans cet emplacement, essayez de les supprimer et de les réinstaller.</span><span class="sxs-lookup"><span data-stu-id="d3df9-142">If the certificates are already in the location, try to delete the certificates and reinstall them.</span></span> <span data-ttu-id="d3df9-143">Le certificat **azuregateway-*GUID*.cloudapp.net** se trouve dans le package de configuration du client VPN, téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d3df9-143">The **azuregateway-*GUID*.cloudapp.net** certificate is in the VPN client configuration package that you downloaded from the Azure portal.</span></span> <span data-ttu-id="d3df9-144">Vous pouvez vous servir des programmes d’archivage de fichiers afin d’extraire les fichiers du package.</span><span class="sxs-lookup"><span data-stu-id="d3df9-144">You can use file archivers to extract the files from the package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="d3df9-145">Erreur de téléchargement du fichier : L’URI cible n’est pas spécifié</span><span class="sxs-lookup"><span data-stu-id="d3df9-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="d3df9-146">Symptôme</span><span class="sxs-lookup"><span data-stu-id="d3df9-146">Symptom</span></span>

<span data-ttu-id="d3df9-147">Vous recevez le message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="d3df9-147">You receive the following error message:</span></span>

<span data-ttu-id="d3df9-148">**Erreur de téléchargement du fichier. L’URI cible n’est pas spécifié.**</span><span class="sxs-lookup"><span data-stu-id="d3df9-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="d3df9-149">Cause :</span><span class="sxs-lookup"><span data-stu-id="d3df9-149">Cause</span></span> 

<span data-ttu-id="d3df9-150">Ce problème se produit lorsque le type de passerelle est incorrecte.</span><span class="sxs-lookup"><span data-stu-id="d3df9-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="d3df9-151">Solution</span><span class="sxs-lookup"><span data-stu-id="d3df9-151">Solution</span></span>

<span data-ttu-id="d3df9-152">Le type de passerelle VPN doit être défini sur la valeur **VPN**, tandis que le type de VPN doit être défini sur la valeur **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="d3df9-152">The VPN gateway type must be **VPN**, and the VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="d3df9-153">Erreur du client VPN : échec du script VPN personnalisé Azure</span><span class="sxs-lookup"><span data-stu-id="d3df9-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="d3df9-154">Symptôme</span><span class="sxs-lookup"><span data-stu-id="d3df9-154">Symptom</span></span>

<span data-ttu-id="d3df9-155">Lorsque vous essayez de vous connecter à un réseau virtuel Azure à l’aide du client VPN, vous recevez le message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="d3df9-155">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="d3df9-156">**Échec du script personnalisé (pour mettre à jour votre table de routage) (Erreur 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="d3df9-156">**Custom script (to update your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="d3df9-157">Cause :</span><span class="sxs-lookup"><span data-stu-id="d3df9-157">Cause</span></span>

<span data-ttu-id="d3df9-158">Ce problème peut se produire si vous essayez d’ouvrir la connexion VPN de point à site à l’aide d’un raccourci.</span><span class="sxs-lookup"><span data-stu-id="d3df9-158">This problem might occur if you are trying to open the site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="d3df9-159">Solution</span><span class="sxs-lookup"><span data-stu-id="d3df9-159">Solution</span></span> 

<span data-ttu-id="d3df9-160">Ouvrez directement le package VPN au lieu de l’ouvrir à partir d’un raccourci.</span><span class="sxs-lookup"><span data-stu-id="d3df9-160">Open the VPN package directly instead of opening it from the shortcut.</span></span>

## <a name="cannot-install-the-vpn-client"></a><span data-ttu-id="d3df9-161">Impossible d’installer le client VPN</span><span class="sxs-lookup"><span data-stu-id="d3df9-161">Cannot install the VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="d3df9-162">Cause :</span><span class="sxs-lookup"><span data-stu-id="d3df9-162">Cause</span></span> 

<span data-ttu-id="d3df9-163">Afin de faire confiance à la passerelle VPN pour votre réseau virtuel, un certificat supplémentaire est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d3df9-163">An additional certificate is required to trust the VPN gateway for your virtual network.</span></span> <span data-ttu-id="d3df9-164">Le certificat est inclus dans le package de configuration du client VPN, généré à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d3df9-164">The certificate is included in the VPN client configuration package that is generated from the Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="d3df9-165">Solution</span><span class="sxs-lookup"><span data-stu-id="d3df9-165">Solution</span></span>

<span data-ttu-id="d3df9-166">Extrayez le package de configuration du client VPN et localisez le fichier .cer.</span><span class="sxs-lookup"><span data-stu-id="d3df9-166">Extract the VPN client configuration package, and find the .cer file.</span></span> <span data-ttu-id="d3df9-167">Pour installer le certificat, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d3df9-167">To install the certificate, follow these steps:</span></span>

1. <span data-ttu-id="d3df9-168">Ouvrez mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="d3df9-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="d3df9-169">Ajoutez le composant logiciel enfichable **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="d3df9-169">Add the **Certificates** snap-in.</span></span>
3. <span data-ttu-id="d3df9-170">Sélectionnez le compte **Ordinateur** de l’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="d3df9-170">Select the **Computer** account for the local computer.</span></span>
4. <span data-ttu-id="d3df9-171">Cliquez sur le nœud **Autorités de certification racines de confiance** avec le bouton droit de la souris.</span><span class="sxs-lookup"><span data-stu-id="d3df9-171">Right-click the **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="d3df9-172">Cliquez sur **All-Task (Toutes les tâches)** > **Import**, puis naviguez vers le fichier .cer extrait du package de configuration du client VPN.</span><span class="sxs-lookup"><span data-stu-id="d3df9-172">Click **All-Task** > **Import**, and browse to the .cer file you extracted from the VPN client configuration package.</span></span>
5. <span data-ttu-id="d3df9-173">Redémarrez l'ordinateur.</span><span class="sxs-lookup"><span data-stu-id="d3df9-173">Restart the computer.</span></span> 
6. <span data-ttu-id="d3df9-174">Essayez d’installer le client VPN.</span><span class="sxs-lookup"><span data-stu-id="d3df9-174">Try to install the VPN client.</span></span>

## <a name="azure-portal-error-failed-to-save-the-vpn-gateway-and-the-data-is-invalid"></a><span data-ttu-id="d3df9-175">Erreur du portail Azure : échec de l’enregistrement. Les données de la passerelle VPN ne sont pas valides</span><span class="sxs-lookup"><span data-stu-id="d3df9-175">Azure portal error: Failed to save the VPN gateway, and the data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="d3df9-176">Symptôme</span><span class="sxs-lookup"><span data-stu-id="d3df9-176">Symptom</span></span>

<span data-ttu-id="d3df9-177">Lorsque vous essayez d’enregistrer les modifications apportées à la passerelle VPN dans le portail Azure, vous recevez le message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="d3df9-177">When you try to save the changes for the VPN gateway in the Azure portal, you receive the following error message:</span></span>

<span data-ttu-id="d3df9-178">**Échec de l’enregistrement de la passerelle de réseau virtuel &lt;*nom de la passerelle*&gt;.</span><span class="sxs-lookup"><span data-stu-id="d3df9-178">**Failed to save virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="d3df9-179">Les données du certificat &lt;*ID de certificat*&gt; ne sont pas valides.**</span><span class="sxs-lookup"><span data-stu-id="d3df9-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="d3df9-180">Cause :</span><span class="sxs-lookup"><span data-stu-id="d3df9-180">Cause</span></span> 

<span data-ttu-id="d3df9-181">Ce problème peut se produire si la clé publique de certificat racine que vous avez téléchargée contient un caractère non valide, comme un espace.</span><span class="sxs-lookup"><span data-stu-id="d3df9-181">This problem might occur if the root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="d3df9-182">Solution</span><span class="sxs-lookup"><span data-stu-id="d3df9-182">Solution</span></span>

<span data-ttu-id="d3df9-183">Vérifiez que les données du certificat ne contiennent pas de caractères non valides, comme des sauts de ligne (retours chariot).</span><span class="sxs-lookup"><span data-stu-id="d3df9-183">Make sure that the data in the certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="d3df9-184">La valeur entière doit être une longue ligne.</span><span class="sxs-lookup"><span data-stu-id="d3df9-184">The entire value should be one long line.</span></span> <span data-ttu-id="d3df9-185">Le texte ci-après est un extrait du certificat :</span><span class="sxs-lookup"><span data-stu-id="d3df9-185">The following text is a sample of the certificate:</span></span>

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-to-save-the-vpn-gateway-and-the-resource-name-is-invalid"></a><span data-ttu-id="d3df9-186">Erreur du portail Azure : échec de l’enregistrement de la passerelle VPN. Le nom de la ressource n’est pas valide</span><span class="sxs-lookup"><span data-stu-id="d3df9-186">Azure portal error: Failed to save the VPN gateway, and the resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="d3df9-187">Symptôme</span><span class="sxs-lookup"><span data-stu-id="d3df9-187">Symptom</span></span>

<span data-ttu-id="d3df9-188">Lorsque vous essayez d’enregistrer les modifications apportées à la passerelle VPN dans le portail Azure, vous recevez le message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="d3df9-188">When you try to save the changes for the VPN gateway in the Azure portal, you receive the following error message:</span></span> 

<span data-ttu-id="d3df9-189">**Échec de l’enregistrement de la passerelle de réseau virtuel &lt;*nom de la passerelle*&gt;.</span><span class="sxs-lookup"><span data-stu-id="d3df9-189">**Failed to save virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="d3df9-190">Erreur : le nom de la ressource &lt;*nom du certificat à télécharger*&gt; n’est pas valide**.</span><span class="sxs-lookup"><span data-stu-id="d3df9-190">Resource name &lt;*certificate name you try to upload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="d3df9-191">Cause :</span><span class="sxs-lookup"><span data-stu-id="d3df9-191">Cause</span></span>

<span data-ttu-id="d3df9-192">Ce problème se produit car le nom du certificat contient un caractère non valide, comme un espace.</span><span class="sxs-lookup"><span data-stu-id="d3df9-192">This problem occurs because the name of the certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="d3df9-193">Erreur du portail Azure : téléchargement du fichier de package VPN (Erreur 503)</span><span class="sxs-lookup"><span data-stu-id="d3df9-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="d3df9-194">Symptôme</span><span class="sxs-lookup"><span data-stu-id="d3df9-194">Symptom</span></span>

<span data-ttu-id="d3df9-195">Lorsque vous essayez de télécharger le package de configuration du client VPN, vous recevez le message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="d3df9-195">When you try to download the VPN client configuration package, you receive the following error message:</span></span>

<span data-ttu-id="d3df9-196">**Impossible de télécharger le fichier. Détails de l’erreur : erreur 503. Le serveur est occupé.**</span><span class="sxs-lookup"><span data-stu-id="d3df9-196">**Failed to download the file. Error details: error 503. The server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="d3df9-197">Solution</span><span class="sxs-lookup"><span data-stu-id="d3df9-197">Solution</span></span>

<span data-ttu-id="d3df9-198">Cette erreur peut être due à un problème réseau temporaire.</span><span class="sxs-lookup"><span data-stu-id="d3df9-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="d3df9-199">Patientez quelques minutes, puis essayez à nouveau de télécharger le package VPN.</span><span class="sxs-lookup"><span data-stu-id="d3df9-199">Try to download the VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-to-connect"></a><span data-ttu-id="d3df9-200">Mise à niveau de la passerelle VPN Azure, aucun client P2S ne peut se connecter</span><span class="sxs-lookup"><span data-stu-id="d3df9-200">Azure VPN Gateway upgrade: All P2S clients are unable to connect</span></span>

### <a name="cause"></a><span data-ttu-id="d3df9-201">Cause :</span><span class="sxs-lookup"><span data-stu-id="d3df9-201">Cause</span></span>

<span data-ttu-id="d3df9-202">Si le certificat a atteint plus de 50 % de sa durée de vie, il est restauré.</span><span class="sxs-lookup"><span data-stu-id="d3df9-202">If the certificate is more than 50 percent through its lifetime, the certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="d3df9-203">Solution</span><span class="sxs-lookup"><span data-stu-id="d3df9-203">Solution</span></span>

<span data-ttu-id="d3df9-204">Pour résoudre ce problème, créez des certificats et redistribuez-les aux clients VPN.</span><span class="sxs-lookup"><span data-stu-id="d3df9-204">To resolve this problem, create and redistribute new certificates to the VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="d3df9-205">Trop de clients VPN sont connectés</span><span class="sxs-lookup"><span data-stu-id="d3df9-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="d3df9-206">Chaque passerelle VPN autorise un nombre de connexions maximal de 128.</span><span class="sxs-lookup"><span data-stu-id="d3df9-206">For each VPN gateway, the maximum number of allowable connections is 128.</span></span> <span data-ttu-id="d3df9-207">Vous pouvez voir le nombre total de clients connectés dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d3df9-207">You can see the total number of connected clients in the Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-to-the-route-table"></a><span data-ttu-id="d3df9-208">Le VPN de point à site ajoute incorrectement un itinéraire pour 10.0.0.0/8 à la table de routage</span><span class="sxs-lookup"><span data-stu-id="d3df9-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 to the route table</span></span>

### <a name="symptom"></a><span data-ttu-id="d3df9-209">Symptôme</span><span class="sxs-lookup"><span data-stu-id="d3df9-209">Symptom</span></span>

<span data-ttu-id="d3df9-210">Lorsque vous appelez la connexion VPN sur le client de point à site, le client VPN doit ajouter un itinéraire vers le réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="d3df9-210">When you dial the VPN connection on the point-to-site client, the VPN client should add a route toward the Azure virtual network.</span></span> <span data-ttu-id="d3df9-211">Le service d’assistance IP doit ajouter un itinéraire pour le sous-réseau des clients VPN.</span><span class="sxs-lookup"><span data-stu-id="d3df9-211">The IP helper service should add a route for the subnet of the VPN clients.</span></span> 

<span data-ttu-id="d3df9-212">La plage de clients VPN appartient à un plus petit sous-réseau de 10.0.0.0/8, comme 10.0.12.0/24.</span><span class="sxs-lookup"><span data-stu-id="d3df9-212">The VPN client range belongs to a smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="d3df9-213">Au lieu d’un itinéraire pour 10.0.12.0/24, un itinéraire pour 10.0.0.0/8 ayant une priorité plus élevée est ajouté.</span><span class="sxs-lookup"><span data-stu-id="d3df9-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="d3df9-214">Cet itinéraire incorrect arrête la connectivité avec d’autres réseaux locaux pouvant appartenir à un autre sous-réseau dans la plage 10.0.0.0/8, comme 10.50.0.0/24 qui ne possède pas d’itinéraire spécifique.</span><span class="sxs-lookup"><span data-stu-id="d3df9-214">This incorrect route breaks connectivity with other on-premises networks that might belong to another subnet within the 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="d3df9-215">Cause :</span><span class="sxs-lookup"><span data-stu-id="d3df9-215">Cause</span></span>

<span data-ttu-id="d3df9-216">Ce comportement est lié aux clients Windows.</span><span class="sxs-lookup"><span data-stu-id="d3df9-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="d3df9-217">Lorsque le client utilise le protocole PPP IPCP, il obtient l’adresse IP de l’interface de tunnel à partir du serveur (la passerelle VPN dans ce cas).</span><span class="sxs-lookup"><span data-stu-id="d3df9-217">When the client uses the PPP IPCP protocol, it obtains the IP address for the tunnel interface from the server (the VPN gateway in this case).</span></span> <span data-ttu-id="d3df9-218">Cependant, à cause de la limitation du protocole, le client ne possède pas de masque de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="d3df9-218">However, because of a limitation in the protocol, the client does not have the subnet mask.</span></span> <span data-ttu-id="d3df9-219">Étant donné qu’il n’existe aucun autre moyen de l’obtenir, le client essaie de deviner le masque de sous-réseau en se basant sur la classe de l’adresse IP de l’interface de tunnel.</span><span class="sxs-lookup"><span data-stu-id="d3df9-219">Because there is no other way to get it, the client tries to guess the subnet mask based on the class of the tunnel interface IP address.</span></span> 

<span data-ttu-id="d3df9-220">Par conséquent, un itinéraire est ajouté sur la base du mappage statique suivant :</span><span class="sxs-lookup"><span data-stu-id="d3df9-220">Therefore, a route is added based on the following static mapping:</span></span> 

<span data-ttu-id="d3df9-221">Si l’adresse appartient à la classe A --> appliquer la valeur /8</span><span class="sxs-lookup"><span data-stu-id="d3df9-221">If address belongs to class A --> apply /8</span></span>

<span data-ttu-id="d3df9-222">Si l’adresse appartient à la classe B --> appliquer la valeur /16</span><span class="sxs-lookup"><span data-stu-id="d3df9-222">If address belongs to class B --> apply /16</span></span>

<span data-ttu-id="d3df9-223">Si l’adresse appartient à la classe C --> appliquer la valeur /24</span><span class="sxs-lookup"><span data-stu-id="d3df9-223">If address belongs to class C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="d3df9-224">Les clients VPN ne peuvent pas accéder aux partages de fichiers réseau</span><span class="sxs-lookup"><span data-stu-id="d3df9-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="d3df9-225">Symptôme</span><span class="sxs-lookup"><span data-stu-id="d3df9-225">Symptom</span></span>

<span data-ttu-id="d3df9-226">Le client VPN s’est connecté au réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="d3df9-226">The VPN client has connected to the Azure virtual network.</span></span> <span data-ttu-id="d3df9-227">Toutefois, le client ne peut pas accéder aux partages réseau.</span><span class="sxs-lookup"><span data-stu-id="d3df9-227">However, the client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="d3df9-228">Cause :</span><span class="sxs-lookup"><span data-stu-id="d3df9-228">Cause</span></span>

<span data-ttu-id="d3df9-229">Le protocole SMB est utilisé pour l’accès au partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="d3df9-229">The SMB protocol is used for file share access.</span></span> <span data-ttu-id="d3df9-230">Au moment où la connexion est établie, le client VPN ajoute les informations d’identification de la session et l’échec se produit.</span><span class="sxs-lookup"><span data-stu-id="d3df9-230">When the connection is initiated, the VPN client adds the session credentials and the failure occurs.</span></span> <span data-ttu-id="d3df9-231">Une fois la connexion établie, le client est forcé d’utiliser les informations d’identification en cache pour l’authentification Kerberos.</span><span class="sxs-lookup"><span data-stu-id="d3df9-231">After the connection is established, the client is forced to use the cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="d3df9-232">Ce processus lance les requêtes sur le centre de distribution de clés (un contrôleur de domaine) afin d’obtenir un jeton.</span><span class="sxs-lookup"><span data-stu-id="d3df9-232">This process initiates queries to the Key Distribution Center (a domain controller) to get a token.</span></span> <span data-ttu-id="d3df9-233">Étant donné que le client se connecte à partir d’Internet, il n’est peut-être pas en mesure d’atteindre le contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="d3df9-233">Because the client connects from the Internet, it might not be able to reach the domain controller.</span></span> <span data-ttu-id="d3df9-234">Par conséquent, le client ne peut pas basculer de Kerberos à NTLM.</span><span class="sxs-lookup"><span data-stu-id="d3df9-234">Therefore, the client cannot fail over from Kerberos to NTLM.</span></span> 

<span data-ttu-id="d3df9-235">Le client est uniquement invité à fournir des informations d’identification quand il possède un certificat valide (avec SAN = UPN) émis par le domaine auquel il est joint.</span><span class="sxs-lookup"><span data-stu-id="d3df9-235">The only time that the client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by the domain to which it is joined.</span></span> <span data-ttu-id="d3df9-236">Le client doit également être physiquement connecté au réseau avec domaine.</span><span class="sxs-lookup"><span data-stu-id="d3df9-236">The client also must be physically connected to the domain network.</span></span> <span data-ttu-id="d3df9-237">Dans ce cas, le client tente d’utiliser le certificat et d’atteindre le contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="d3df9-237">In this case, the client tries to use the certificate and reaches out to the domain controller.</span></span> <span data-ttu-id="d3df9-238">Le centre de distribution de clés renvoie alors une erreur « KDC_ERR_C_PRINCIPAL_UNKNOWN ».</span><span class="sxs-lookup"><span data-stu-id="d3df9-238">Then the Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="d3df9-239">Cette erreur force le client à basculer vers NTLM.</span><span class="sxs-lookup"><span data-stu-id="d3df9-239">The client is forced to fail over to NTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="d3df9-240">Solution</span><span class="sxs-lookup"><span data-stu-id="d3df9-240">Solution</span></span>

<span data-ttu-id="d3df9-241">Pour contourner le problème, désactivez la mise en cache des informations d’identification de domaine à partir de la sous-clé de Registre suivante :</span><span class="sxs-lookup"><span data-stu-id="d3df9-241">To work around the problem, disable the caching of domain credentials from the following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set the value to 1 


## <a name="cannot-find-the-point-to-site-vpn-connection-in-windows-after-reinstalling-the-vpn-client"></a><span data-ttu-id="d3df9-242">Impossible de trouver la connexion VPN de point à site dans Windows après la réinstallation du client VPN</span><span class="sxs-lookup"><span data-stu-id="d3df9-242">Cannot find the point-to-site VPN connection in Windows after reinstalling the VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="d3df9-243">Symptôme</span><span class="sxs-lookup"><span data-stu-id="d3df9-243">Symptom</span></span>

<span data-ttu-id="d3df9-244">Supprimez la connexion VPN de point à site, puis réinstallez le client VPN.</span><span class="sxs-lookup"><span data-stu-id="d3df9-244">You remove the point-to-site VPN connection and then reinstall the VPN client.</span></span> <span data-ttu-id="d3df9-245">Dans ce cas, la connexion VPN n’est pas configurée correctement.</span><span class="sxs-lookup"><span data-stu-id="d3df9-245">In this situation, the VPN connection is not configured successfully.</span></span> <span data-ttu-id="d3df9-246">Vous ne voyez pas la connexion VPN dans les paramètres **Connexions réseau** dans Windows.</span><span class="sxs-lookup"><span data-stu-id="d3df9-246">You do not see the VPN connection in the **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="d3df9-247">Solution</span><span class="sxs-lookup"><span data-stu-id="d3df9-247">Solution</span></span>

<span data-ttu-id="d3df9-248">Pour résoudre le problème, supprimez les anciens fichiers de configuration du client VPN à partir de **C:\Utilisateurs\Nomdel’utilisateur\AppData\Roaming\Microsoft\Network\Connections**, puis exécutez à nouveau le programme d’installation du client VPN.</span><span class="sxs-lookup"><span data-stu-id="d3df9-248">To resolve the problem, delete the old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run the VPN client installer again.</span></span>
