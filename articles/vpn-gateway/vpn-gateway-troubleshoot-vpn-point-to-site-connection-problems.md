---
title: "problèmes de connexion aaaTroubleshoot Azure point-to-site | Documents Microsoft"
description: "Découvrez comment les problèmes de connexion de point-to-site tootroubleshoot."
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
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="37593-103">Résolution des problèmes de connexion de point à site Azure</span><span class="sxs-lookup"><span data-stu-id="37593-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="37593-104">Cet article répertorie les problèmes de connexion de point à site courants que vous pouvez rencontrer.</span><span class="sxs-lookup"><span data-stu-id="37593-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="37593-105">Il décrit également les causes probables de ces problèmes, ainsi que les solutions possibles.</span><span class="sxs-lookup"><span data-stu-id="37593-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="37593-106">Erreur du client VPN : le certificat est introuvable</span><span class="sxs-lookup"><span data-stu-id="37593-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="37593-107">Symptôme</span><span class="sxs-lookup"><span data-stu-id="37593-107">Symptom</span></span>

<span data-ttu-id="37593-108">Lorsque vous essayez tooconnect tooan réseau virtuel Azure à l’aide du client VPN de hello, vous recevez hello message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="37593-108">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="37593-109">**Impossible de trouver un certificat qui peut être utilisé avec le protocole EAP (Extensible Authentication Protocol). (Erreur 798)**</span><span class="sxs-lookup"><span data-stu-id="37593-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="37593-110">Cause :</span><span class="sxs-lookup"><span data-stu-id="37593-110">Cause</span></span>

<span data-ttu-id="37593-111">Ce problème se produit si le certificat de client hello est absent de **certificats - actuel\Personnel\Certificats**.</span><span class="sxs-lookup"><span data-stu-id="37593-111">This problem occurs if hello client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="37593-112">Solution</span><span class="sxs-lookup"><span data-stu-id="37593-112">Solution</span></span>

<span data-ttu-id="37593-113">Vérifiez que ce certificat de client hello est installé dans hello du magasin de certificats hello (Certmgr.msc) de l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="37593-113">Make sure that hello client certificate is installed in hello following location of hello Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="37593-114">**Certificats - Utilisateur actuel\Personnel\Certificats**</span><span class="sxs-lookup"><span data-stu-id="37593-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="37593-115">Pour plus d’informations sur comment tooinstall hello certificat client, consultez [générer et exporter des certificats pour les connexions de point-to-site](vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="37593-115">For more information about how tooinstall hello client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="37593-116">Lorsque vous importez le certificat de client hello, ne sélectionnez pas hello **activer la protection renforcée par clé privée** option.</span><span class="sxs-lookup"><span data-stu-id="37593-116">When you import hello client certificate, do not select hello **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="37593-117">Erreur du client VPN : message de salutation reçu était inattendu ou incorrectement formatée</span><span class="sxs-lookup"><span data-stu-id="37593-117">VPN client error: hello message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="37593-118">Symptôme</span><span class="sxs-lookup"><span data-stu-id="37593-118">Symptom</span></span>

<span data-ttu-id="37593-119">Lorsque vous essayez tooconnect tooan réseau virtuel Azure à l’aide du client VPN de hello, vous recevez hello message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="37593-119">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="37593-120">**message de salutation reçu était inattendu ou incorrectement formatée. (Erreur 0x80090326)**</span><span class="sxs-lookup"><span data-stu-id="37593-120">**hello message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="37593-121">Cause :</span><span class="sxs-lookup"><span data-stu-id="37593-121">Cause</span></span>

<span data-ttu-id="37593-122">Ce problème se produit si la clé publique du certificat racine hello n’est pas téléchargé dans la passerelle VPN Azure hello.</span><span class="sxs-lookup"><span data-stu-id="37593-122">This problem occurs if hello root certificate public key is not uploaded into hello Azure VPN gateway.</span></span> <span data-ttu-id="37593-123">Il peut également se produire si la clé de hello est endommagée ou a expiré.</span><span class="sxs-lookup"><span data-stu-id="37593-123">It can also occur if hello key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="37593-124">Solution</span><span class="sxs-lookup"><span data-stu-id="37593-124">Solution</span></span>

<span data-ttu-id="37593-125">tooresolve ce problème, vérifiez l’état de la racine de hello hello certificats Bonjour Azure toosee portail si elle a été révoqué.</span><span class="sxs-lookup"><span data-stu-id="37593-125">tooresolve this problem, check hello status of hello root certificate in hello Azure portal toosee whether it was revoked.</span></span> <span data-ttu-id="37593-126">Si elle n’est pas révoqué, essayez de reupload et un certificat racine de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="37593-126">If it is not revoked, try toodelete hello root certificate and reupload.</span></span> <span data-ttu-id="37593-127">Pour en savoir plus, consultez la section [Créer des certificats](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span><span class="sxs-lookup"><span data-stu-id="37593-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="37593-128">Erreur du client VPN : une chaîne de certificats a été traitée mais s’est terminée</span><span class="sxs-lookup"><span data-stu-id="37593-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="37593-129">Symptôme</span><span class="sxs-lookup"><span data-stu-id="37593-129">Symptom</span></span> 

<span data-ttu-id="37593-130">Lorsque vous essayez tooconnect tooan réseau virtuel Azure à l’aide du client VPN de hello, vous recevez hello message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="37593-130">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="37593-131">**Une chaîne de certificats traitée mais s’est terminée par un certificat racine qui n’est pas approuvé par le fournisseur d’approbation hello.**</span><span class="sxs-lookup"><span data-stu-id="37593-131">**A certificate chain processed but terminated in a root certificate which is not trusted by hello trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="37593-132">Solution</span><span class="sxs-lookup"><span data-stu-id="37593-132">Solution</span></span>

1. <span data-ttu-id="37593-133">Assurez-vous que hello certificats suivants sont dans l’emplacement correct de hello :</span><span class="sxs-lookup"><span data-stu-id="37593-133">Make sure that hello following certificates are in hello correct location:</span></span>

    | <span data-ttu-id="37593-134">Certificat</span><span class="sxs-lookup"><span data-stu-id="37593-134">Certificate</span></span> | <span data-ttu-id="37593-135">Emplacement</span><span class="sxs-lookup"><span data-stu-id="37593-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="37593-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="37593-136">AzureClient.pfx</span></span>  | <span data-ttu-id="37593-137">Utilisateur actuel\Personnel\Certificats</span><span class="sxs-lookup"><span data-stu-id="37593-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="37593-138">Azuregateway-*GUID*.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="37593-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="37593-139">Utilisateur actuel\Autorités de certification racines de confiance</span><span class="sxs-lookup"><span data-stu-id="37593-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="37593-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="37593-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="37593-141">Ordinateur local\Autorités de certification racines de confiance</span><span class="sxs-lookup"><span data-stu-id="37593-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="37593-142">Si les certificats hello sont déjà dans l’emplacement de hello, essayez les certificats toodelete hello et réinstallez-les.</span><span class="sxs-lookup"><span data-stu-id="37593-142">If hello certificates are already in hello location, try toodelete hello certificates and reinstall them.</span></span> <span data-ttu-id="37593-143">Hello  **azuregateway -*GUID*. cloudapp.net** certificat est dans le package de configuration hello VPN client que vous avez téléchargé à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="37593-143">hello **azuregateway-*GUID*.cloudapp.net** certificate is in hello VPN client configuration package that you downloaded from hello Azure portal.</span></span> <span data-ttu-id="37593-144">Vous pouvez utiliser archivers tooextract hello des fichiers à partir du package de hello.</span><span class="sxs-lookup"><span data-stu-id="37593-144">You can use file archivers tooextract hello files from hello package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="37593-145">Erreur de téléchargement du fichier : L’URI cible n’est pas spécifié</span><span class="sxs-lookup"><span data-stu-id="37593-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="37593-146">Symptôme</span><span class="sxs-lookup"><span data-stu-id="37593-146">Symptom</span></span>

<span data-ttu-id="37593-147">Hello, message d’erreur suivant s’affiche :</span><span class="sxs-lookup"><span data-stu-id="37593-147">You receive hello following error message:</span></span>

<span data-ttu-id="37593-148">**Erreur de téléchargement du fichier. L’URI cible n’est pas spécifié.**</span><span class="sxs-lookup"><span data-stu-id="37593-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="37593-149">Cause :</span><span class="sxs-lookup"><span data-stu-id="37593-149">Cause</span></span> 

<span data-ttu-id="37593-150">Ce problème se produit lorsque le type de passerelle est incorrecte.</span><span class="sxs-lookup"><span data-stu-id="37593-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="37593-151">Solution</span><span class="sxs-lookup"><span data-stu-id="37593-151">Solution</span></span>

<span data-ttu-id="37593-152">Hello, type de passerelle VPN doit être **VPN**, et hello type VPN doit être **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="37593-152">hello VPN gateway type must be **VPN**, and hello VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="37593-153">Erreur du client VPN : échec du script VPN personnalisé Azure</span><span class="sxs-lookup"><span data-stu-id="37593-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="37593-154">Symptôme</span><span class="sxs-lookup"><span data-stu-id="37593-154">Symptom</span></span>

<span data-ttu-id="37593-155">Lorsque vous essayez tooconnect tooan réseau virtuel Azure à l’aide du client VPN de hello, vous recevez hello message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="37593-155">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="37593-156">**Script personnalisé (tooupdate votre table de routage) a échoué. (Erreur 8007026f)**</span><span class="sxs-lookup"><span data-stu-id="37593-156">**Custom script (tooupdate your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="37593-157">Cause :</span><span class="sxs-lookup"><span data-stu-id="37593-157">Cause</span></span>

<span data-ttu-id="37593-158">Ce problème peut se produire si la tentative de connexion VPN de tooopen hello-à-point de site à l’aide d’un raccourci.</span><span class="sxs-lookup"><span data-stu-id="37593-158">This problem might occur if you are trying tooopen hello site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="37593-159">Solution</span><span class="sxs-lookup"><span data-stu-id="37593-159">Solution</span></span> 

<span data-ttu-id="37593-160">Ouvrez le package VPN hello directement au lieu d’ouvrir à partir du raccourci de hello.</span><span class="sxs-lookup"><span data-stu-id="37593-160">Open hello VPN package directly instead of opening it from hello shortcut.</span></span>

## <a name="cannot-install-hello-vpn-client"></a><span data-ttu-id="37593-161">Impossible d’installer hello VPN client</span><span class="sxs-lookup"><span data-stu-id="37593-161">Cannot install hello VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="37593-162">Cause :</span><span class="sxs-lookup"><span data-stu-id="37593-162">Cause</span></span> 

<span data-ttu-id="37593-163">Un certificat supplémentaire est la passerelle VPN hello tootrust requis pour votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="37593-163">An additional certificate is required tootrust hello VPN gateway for your virtual network.</span></span> <span data-ttu-id="37593-164">certificat de Hello est inclus dans le package de configuration hello VPN client qui est généré à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="37593-164">hello certificate is included in hello VPN client configuration package that is generated from hello Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="37593-165">Solution</span><span class="sxs-lookup"><span data-stu-id="37593-165">Solution</span></span>

<span data-ttu-id="37593-166">Extraire le package de configuration de client VPN hello et recherchez le fichier .cer de hello.</span><span class="sxs-lookup"><span data-stu-id="37593-166">Extract hello VPN client configuration package, and find hello .cer file.</span></span> <span data-ttu-id="37593-167">tooinstall hello certificat, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="37593-167">tooinstall hello certificate, follow these steps:</span></span>

1. <span data-ttu-id="37593-168">Ouvrez mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="37593-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="37593-169">Ajouter hello **certificats** enfichable.</span><span class="sxs-lookup"><span data-stu-id="37593-169">Add hello **Certificates** snap-in.</span></span>
3. <span data-ttu-id="37593-170">Sélectionnez hello **ordinateur** compte pour l’ordinateur local de hello.</span><span class="sxs-lookup"><span data-stu-id="37593-170">Select hello **Computer** account for hello local computer.</span></span>
4. <span data-ttu-id="37593-171">Avec le bouton hello **autorités de Certification racines de confiance** nœud.</span><span class="sxs-lookup"><span data-stu-id="37593-171">Right-click hello **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="37593-172">Cliquez sur **All-tâche** > **importation**et le fichier .cer de consultation toohello vous avez extrait à partir du package de configuration de client VPN hello.</span><span class="sxs-lookup"><span data-stu-id="37593-172">Click **All-Task** > **Import**, and browse toohello .cer file you extracted from hello VPN client configuration package.</span></span>
5. <span data-ttu-id="37593-173">Redémarrez l’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="37593-173">Restart hello computer.</span></span> 
6. <span data-ttu-id="37593-174">Essayez de client VPN de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="37593-174">Try tooinstall hello VPN client.</span></span>

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a><span data-ttu-id="37593-175">Erreur de portail Azure : Échec de la passerelle VPN de hello toosave, et les données de salutation ne sont pas valides</span><span class="sxs-lookup"><span data-stu-id="37593-175">Azure portal error: Failed toosave hello VPN gateway, and hello data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="37593-176">Symptôme</span><span class="sxs-lookup"><span data-stu-id="37593-176">Symptom</span></span>

<span data-ttu-id="37593-177">Lorsque vous essayez de modifications de hello toosave pour la passerelle VPN de hello Bonjour portail Azure, vous recevez hello message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="37593-177">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span>

<span data-ttu-id="37593-178">**Passerelle de réseau virtuel a échoué toosave &lt;* nom de la passerelle*&gt;.</span><span class="sxs-lookup"><span data-stu-id="37593-178">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="37593-179">Les données du certificat &lt;*ID de certificat*&gt; ne sont pas valides.**</span><span class="sxs-lookup"><span data-stu-id="37593-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="37593-180">Cause :</span><span class="sxs-lookup"><span data-stu-id="37593-180">Cause</span></span> 

<span data-ttu-id="37593-181">Ce problème peut se produire si hello racine certificat clé publique que vous avez téléchargé contient un caractère non valide, tels qu’un espace.</span><span class="sxs-lookup"><span data-stu-id="37593-181">This problem might occur if hello root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="37593-182">Solution</span><span class="sxs-lookup"><span data-stu-id="37593-182">Solution</span></span>

<span data-ttu-id="37593-183">Assurez-vous que les données hello dans le certificat de hello ne contient pas de caractères non valides, tels que les sauts de ligne (retour chariot).</span><span class="sxs-lookup"><span data-stu-id="37593-183">Make sure that hello data in hello certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="37593-184">valeur entière de Hello doit être une longue ligne.</span><span class="sxs-lookup"><span data-stu-id="37593-184">hello entire value should be one long line.</span></span> <span data-ttu-id="37593-185">Hello suivant le texte est un exemple de certificat de hello :</span><span class="sxs-lookup"><span data-stu-id="37593-185">hello following text is a sample of hello certificate:</span></span>

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

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a><span data-ttu-id="37593-186">Erreur de portail Azure : Échec de la passerelle VPN de hello toosave et nom de la ressource hello n’est pas valide</span><span class="sxs-lookup"><span data-stu-id="37593-186">Azure portal error: Failed toosave hello VPN gateway, and hello resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="37593-187">Symptôme</span><span class="sxs-lookup"><span data-stu-id="37593-187">Symptom</span></span>

<span data-ttu-id="37593-188">Lorsque vous essayez de modifications de hello toosave pour la passerelle VPN de hello Bonjour portail Azure, vous recevez hello message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="37593-188">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span> 

<span data-ttu-id="37593-189">**Passerelle de réseau virtuel a échoué toosave &lt;* nom de la passerelle*&gt;.</span><span class="sxs-lookup"><span data-stu-id="37593-189">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="37593-190">Nom de la ressource &lt; *nom de certificat que vous essayez de tooupload* &gt; n’est pas valide **.</span><span class="sxs-lookup"><span data-stu-id="37593-190">Resource name &lt;*certificate name you try tooupload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="37593-191">Cause :</span><span class="sxs-lookup"><span data-stu-id="37593-191">Cause</span></span>

<span data-ttu-id="37593-192">Ce problème se produit parce que le nom hello du certificat de hello contient un caractère non valide, tels qu’un espace.</span><span class="sxs-lookup"><span data-stu-id="37593-192">This problem occurs because hello name of hello certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="37593-193">Erreur du portail Azure : téléchargement du fichier de package VPN (Erreur 503)</span><span class="sxs-lookup"><span data-stu-id="37593-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="37593-194">Symptôme</span><span class="sxs-lookup"><span data-stu-id="37593-194">Symptom</span></span>

<span data-ttu-id="37593-195">Lorsque vous essayez de package de configuration client toodownload hello VPN, vous recevez hello message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="37593-195">When you try toodownload hello VPN client configuration package, you receive hello following error message:</span></span>

<span data-ttu-id="37593-196">**Échec de toodownload hello fichier. Détails de l’erreur : erreur 503. Hello serveur est occupé.**</span><span class="sxs-lookup"><span data-stu-id="37593-196">**Failed toodownload hello file. Error details: error 503. hello server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="37593-197">Solution</span><span class="sxs-lookup"><span data-stu-id="37593-197">Solution</span></span>

<span data-ttu-id="37593-198">Cette erreur peut être due à un problème réseau temporaire.</span><span class="sxs-lookup"><span data-stu-id="37593-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="37593-199">Réessayez dans le package VPN toodownload hello quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="37593-199">Try toodownload hello VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a><span data-ttu-id="37593-200">Mise à niveau de passerelle VPN Azure : P2S tous les clients sont tooconnect Impossible</span><span class="sxs-lookup"><span data-stu-id="37593-200">Azure VPN Gateway upgrade: All P2S clients are unable tooconnect</span></span>

### <a name="cause"></a><span data-ttu-id="37593-201">Cause :</span><span class="sxs-lookup"><span data-stu-id="37593-201">Cause</span></span>

<span data-ttu-id="37593-202">Si le certificat de hello est plus de 50 % à sa durée de vie, les certificats hello sont restaurée.</span><span class="sxs-lookup"><span data-stu-id="37593-202">If hello certificate is more than 50 percent through its lifetime, hello certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="37593-203">Solution</span><span class="sxs-lookup"><span data-stu-id="37593-203">Solution</span></span>

<span data-ttu-id="37593-204">tooresolve ce problème, créez et redistribuer les clients VPN de nouveaux certificats toohello.</span><span class="sxs-lookup"><span data-stu-id="37593-204">tooresolve this problem, create and redistribute new certificates toohello VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="37593-205">Trop de clients VPN sont connectés</span><span class="sxs-lookup"><span data-stu-id="37593-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="37593-206">Pour chaque passerelle VPN, hello de nombre maximal de connexions autorisées est de 128.</span><span class="sxs-lookup"><span data-stu-id="37593-206">For each VPN gateway, hello maximum number of allowable connections is 128.</span></span> <span data-ttu-id="37593-207">Vous pouvez voir le nombre total de hello de clients connectés Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="37593-207">You can see hello total number of connected clients in hello Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a><span data-ttu-id="37593-208">Point-to-site VPN ajoute incorrectement un itinéraire pour la table d’itinéraires toohello 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="37593-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 toohello route table</span></span>

### <a name="symptom"></a><span data-ttu-id="37593-209">Symptôme</span><span class="sxs-lookup"><span data-stu-id="37593-209">Symptom</span></span>

<span data-ttu-id="37593-210">Lorsque vous composez hello connexion VPN sur le client de point-to-site hello, client VPN de hello doit ajouter un itinéraire vers le réseau virtuel Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="37593-210">When you dial hello VPN connection on hello point-to-site client, hello VPN client should add a route toward hello Azure virtual network.</span></span> <span data-ttu-id="37593-211">service de programme d’assistance IP Hello doit ajouter un itinéraire pour le sous-réseau hello de clients VPN de hello.</span><span class="sxs-lookup"><span data-stu-id="37593-211">hello IP helper service should add a route for hello subnet of hello VPN clients.</span></span> 

<span data-ttu-id="37593-212">Hello plage de client VPN appartient tooa plus petit sous-réseau 10.0.0.0/8, telles que 10.0.12.0/24.</span><span class="sxs-lookup"><span data-stu-id="37593-212">hello VPN client range belongs tooa smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="37593-213">Au lieu d’un itinéraire pour 10.0.12.0/24, un itinéraire pour 10.0.0.0/8 ayant une priorité plus élevée est ajouté.</span><span class="sxs-lookup"><span data-stu-id="37593-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="37593-214">Cet itinéraire incorrect rompt la connectivité avec d’autres réseaux locaux qui peuvent appartenir sous-réseau tooanother plage hello 10.0.0.0/8, telles que 10.50.0.0/24, qui n’ont pas un itinéraire spécifique défini.</span><span class="sxs-lookup"><span data-stu-id="37593-214">This incorrect route breaks connectivity with other on-premises networks that might belong tooanother subnet within hello 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="37593-215">Cause :</span><span class="sxs-lookup"><span data-stu-id="37593-215">Cause</span></span>

<span data-ttu-id="37593-216">Ce comportement est lié aux clients Windows.</span><span class="sxs-lookup"><span data-stu-id="37593-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="37593-217">Lorsque le client de hello utilise le protocole PPP IPCP de hello, il obtient adresse hello pour l’interface de tunnel hello du serveur de hello (hello passerelle VPN dans ce cas).</span><span class="sxs-lookup"><span data-stu-id="37593-217">When hello client uses hello PPP IPCP protocol, it obtains hello IP address for hello tunnel interface from hello server (hello VPN gateway in this case).</span></span> <span data-ttu-id="37593-218">Toutefois, en raison d’une limitation dans le protocole de hello, client de hello n’a pas de masque de sous-réseau hello.</span><span class="sxs-lookup"><span data-stu-id="37593-218">However, because of a limitation in hello protocol, hello client does not have hello subnet mask.</span></span> <span data-ttu-id="37593-219">Étant donné qu’aucun autre tooget de façon il, client de hello essaie en fonction de la classe hello d’adresse IP de hello tunnel interface le masque de sous-réseau tooguess hello.</span><span class="sxs-lookup"><span data-stu-id="37593-219">Because there is no other way tooget it, hello client tries tooguess hello subnet mask based on hello class of hello tunnel interface IP address.</span></span> 

<span data-ttu-id="37593-220">Par conséquent, ajoutez un itinéraire en fonction de hello suivant mappage statique :</span><span class="sxs-lookup"><span data-stu-id="37593-220">Therefore, a route is added based on hello following static mapping:</span></span> 

<span data-ttu-id="37593-221">Si l’adresse appartient tooclass A--> appliquer la valeur/8</span><span class="sxs-lookup"><span data-stu-id="37593-221">If address belongs tooclass A --> apply /8</span></span>

<span data-ttu-id="37593-222">Si l’adresse appartient tooclass B--> appliquer /16</span><span class="sxs-lookup"><span data-stu-id="37593-222">If address belongs tooclass B --> apply /16</span></span>

<span data-ttu-id="37593-223">Si l’adresse appartient tooclass C--> appliquer /24</span><span class="sxs-lookup"><span data-stu-id="37593-223">If address belongs tooclass C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="37593-224">Les clients VPN ne peuvent pas accéder aux partages de fichiers réseau</span><span class="sxs-lookup"><span data-stu-id="37593-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="37593-225">Symptôme</span><span class="sxs-lookup"><span data-stu-id="37593-225">Symptom</span></span>

<span data-ttu-id="37593-226">Hello VPN client s’est connecté toohello réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="37593-226">hello VPN client has connected toohello Azure virtual network.</span></span> <span data-ttu-id="37593-227">Toutefois, les clients hello ne peut pas accéder aux partages réseau.</span><span class="sxs-lookup"><span data-stu-id="37593-227">However, hello client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="37593-228">Cause :</span><span class="sxs-lookup"><span data-stu-id="37593-228">Cause</span></span>

<span data-ttu-id="37593-229">Hello protocole SMB est utilisé pour l’accès de partage de fichier.</span><span class="sxs-lookup"><span data-stu-id="37593-229">hello SMB protocol is used for file share access.</span></span> <span data-ttu-id="37593-230">Lors de la connexion à hello est lancée, client VPN de hello ajoute des informations d’identification de session hello et hello échec se produit.</span><span class="sxs-lookup"><span data-stu-id="37593-230">When hello connection is initiated, hello VPN client adds hello session credentials and hello failure occurs.</span></span> <span data-ttu-id="37593-231">Après hello est établie, un client de hello forcé toouse hello cache informations d’identification pour l’authentification Kerberos.</span><span class="sxs-lookup"><span data-stu-id="37593-231">After hello connection is established, hello client is forced toouse hello cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="37593-232">Ce processus lance les requêtes toohello centre de Distribution de clés (un contrôleur de domaine) tooget un jeton.</span><span class="sxs-lookup"><span data-stu-id="37593-232">This process initiates queries toohello Key Distribution Center (a domain controller) tooget a token.</span></span> <span data-ttu-id="37593-233">Étant donné que le client de hello se connecte à partir de hello Internet, il peut être contrôleur de domaine en mesure de tooreach hello.</span><span class="sxs-lookup"><span data-stu-id="37593-233">Because hello client connects from hello Internet, it might not be able tooreach hello domain controller.</span></span> <span data-ttu-id="37593-234">Par conséquent, les clients hello ne peuvent pas basculer à partir de tooNTLM de Kerberos.</span><span class="sxs-lookup"><span data-stu-id="37593-234">Therefore, hello client cannot fail over from Kerberos tooNTLM.</span></span> 

<span data-ttu-id="37593-235">Hello uniquement de temps que le client hello est invité à fournir pour une information d’identification est lorsqu’il possède un certificat valide (avec SAN = UPN) émis par toowhich de domaine hello il est joint.</span><span class="sxs-lookup"><span data-stu-id="37593-235">hello only time that hello client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by hello domain toowhich it is joined.</span></span> <span data-ttu-id="37593-236">Hello client également doit être connectée physiquement toohello un réseau avec domaine.</span><span class="sxs-lookup"><span data-stu-id="37593-236">hello client also must be physically connected toohello domain network.</span></span> <span data-ttu-id="37593-237">Dans ce cas, les clients hello tente de certificat de hello toouse et contacte le contrôleur de domaine toohello.</span><span class="sxs-lookup"><span data-stu-id="37593-237">In this case, hello client tries toouse hello certificate and reaches out toohello domain controller.</span></span> <span data-ttu-id="37593-238">Hello, Key Distribution Center retourne ensuite une erreur « KDC_ERR_C_PRINCIPAL_UNKNOWN ».</span><span class="sxs-lookup"><span data-stu-id="37593-238">Then hello Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="37593-239">client de Hello est forcé toofail sur tooNTLM.</span><span class="sxs-lookup"><span data-stu-id="37593-239">hello client is forced toofail over tooNTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="37593-240">Solution</span><span class="sxs-lookup"><span data-stu-id="37593-240">Solution</span></span>

<span data-ttu-id="37593-241">toowork problème de hello, désactiver hello mise en cache des informations d’identification de domaine à partir de hello suivant la sous-clé de Registre :</span><span class="sxs-lookup"><span data-stu-id="37593-241">toowork around hello problem, disable hello caching of domain credentials from hello following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a><span data-ttu-id="37593-242">Ne peut pas trouver la connexion de hello point-to-site VPN dans Windows après la réinstallation du client VPN de hello</span><span class="sxs-lookup"><span data-stu-id="37593-242">Cannot find hello point-to-site VPN connection in Windows after reinstalling hello VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="37593-243">Symptôme</span><span class="sxs-lookup"><span data-stu-id="37593-243">Symptom</span></span>

<span data-ttu-id="37593-244">Vous supprimez la connexion VPN de point-to-site hello et puis réinstallez le client VPN de hello.</span><span class="sxs-lookup"><span data-stu-id="37593-244">You remove hello point-to-site VPN connection and then reinstall hello VPN client.</span></span> <span data-ttu-id="37593-245">Dans ce cas, hello connexion VPN n’est pas configuré correctement.</span><span class="sxs-lookup"><span data-stu-id="37593-245">In this situation, hello VPN connection is not configured successfully.</span></span> <span data-ttu-id="37593-246">Vous ne voyez pas la connexion VPN de hello Bonjour **des connexions réseau** sous Windows.</span><span class="sxs-lookup"><span data-stu-id="37593-246">You do not see hello VPN connection in hello **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="37593-247">Solution</span><span class="sxs-lookup"><span data-stu-id="37593-247">Solution</span></span>

<span data-ttu-id="37593-248">problème de hello tooresolve, delete hello ancien VPN client des fichiers de configuration **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, puis exécutez à nouveau le programme d’installation client hello VPN.</span><span class="sxs-lookup"><span data-stu-id="37593-248">tooresolve hello problem, delete hello old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run hello VPN client installer again.</span></span>
