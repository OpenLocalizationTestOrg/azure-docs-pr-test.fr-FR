---
title: "Métadonnées de fédération Azure AD | Microsoft Docs"
description: "Cet article décrit le document de métadonnées de fédération publié par Azure Active Directory pour les services qui acceptent les jetons Azure Active Directory."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c2d5f80b-aa74-452c-955b-d8eb3ed62652
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ecafb02a6ac13d1c3cd1fe77ef710cd8525e32b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="federation-metadata"></a><span data-ttu-id="319d0-103">Métadonnées de fédération</span><span class="sxs-lookup"><span data-stu-id="319d0-103">Federation metadata</span></span>
<span data-ttu-id="319d0-104">Azure Active Directory (Azure AD) publie un document de métadonnées de fédération pour les services qui sont configurés pour accepter les jetons de sécurité émis par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="319d0-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured to accept the security tokens that Azure AD issues.</span></span> <span data-ttu-id="319d0-105">Le format de document des métadonnées de fédération est décrit dans la page [Web Services Federation Language (WS-Federation) Version 1.2 (Langage WS-Federation [Web Services Federation Language] version 1.2)](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), qui étend les [métadonnées pour la spécification SAML (Security Assertion Markup Language) OASIS v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span><span class="sxs-lookup"><span data-stu-id="319d0-105">The federation metadata document format is described in the [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for the OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="319d0-106">Points de terminaison de métadonnées spécifiques ou indépendants du client</span><span class="sxs-lookup"><span data-stu-id="319d0-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="319d0-107">Azure AD publie des points de terminaison spécifiques et indépendants du client.</span><span class="sxs-lookup"><span data-stu-id="319d0-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="319d0-108">Les points de terminaison spécifiques du client sont conçus pour un client donné.</span><span class="sxs-lookup"><span data-stu-id="319d0-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="319d0-109">Les métadonnées de fédération spécifiques du client contiennent des informations sur le client, y compris des informations sur l’émetteur et le point de terminaison propres au client.</span><span class="sxs-lookup"><span data-stu-id="319d0-109">The tenant-specific federation metadata includes information about the tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="319d0-110">Les applications qui limitent l’accès à un seul client utilisent des points de terminaison spécifiques du client.</span><span class="sxs-lookup"><span data-stu-id="319d0-110">Applications that restrict access to a single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="319d0-111">Les points de terminaison indépendants du client fournissent des informations qui sont communes à tous les clients Azure AD.</span><span class="sxs-lookup"><span data-stu-id="319d0-111">Tenant-independent endpoints provide information that is common to all Azure AD tenants.</span></span> <span data-ttu-id="319d0-112">Ces informations s’appliquent aux clients hébergés sur *login.microsoftonline.com* et sont partagées entre les clients.</span><span class="sxs-lookup"><span data-stu-id="319d0-112">This information applies to tenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="319d0-113">Les points de terminaison indépendants du client sont recommandés pour les applications mutualisées, car ils ne sont pas associés à un client particulier.</span><span class="sxs-lookup"><span data-stu-id="319d0-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="319d0-114">Points de terminaison de métadonnées de fédération</span><span class="sxs-lookup"><span data-stu-id="319d0-114">Federation metadata endpoints</span></span>
<span data-ttu-id="319d0-115">Azure AD publie des métadonnées de fédération dans `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="319d0-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="319d0-116">Pour les **points de terminaison spécifiques du client**, le `TenantDomainName` peut être de l’un des types suivants :</span><span class="sxs-lookup"><span data-stu-id="319d0-116">For **tenant-specific endpoints**, the `TenantDomainName` can be one of the following types:</span></span>

* <span data-ttu-id="319d0-117">Un nom de domaine enregistré d’un client Azure AD, par exemple `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="319d0-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="319d0-118">L’ID client non modifiable du domaine, tel que `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="319d0-118">The immutable tenant ID of the domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="319d0-119">Pour les **points de terminaison indépendants du client**, le `TenantDomainName` est `common`.</span><span class="sxs-lookup"><span data-stu-id="319d0-119">For **tenant-independent endpoints**, the `TenantDomainName` is `common`.</span></span> <span data-ttu-id="319d0-120">Ce document répertorie uniquement les éléments de métadonnées de fédération communs à tous les clients Azure AD, hébergés à l’adresse login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="319d0-120">This document lists only the Federation Metadata elements that are common to all Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="319d0-121">Par exemple, un point de terminaison propre à un client peut être `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="319d0-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="319d0-122">Le point de terminaison indépendant du client est [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="319d0-122">The tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="319d0-123">Vous pouvez afficher le document de métadonnées de fédération en tapant cette URL dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="319d0-123">You can view the federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="319d0-124">Contenu des métadonnées de fédération</span><span class="sxs-lookup"><span data-stu-id="319d0-124">Contents of federation Metadata</span></span>
<span data-ttu-id="319d0-125">La section suivante fournit les informations nécessaires aux services qui utilisent des jetons émis par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="319d0-125">The following section provides information needed by services that consume the tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="319d0-126">L’ID d’entité</span><span class="sxs-lookup"><span data-stu-id="319d0-126">Entity ID</span></span>
<span data-ttu-id="319d0-127">L’élément `EntityDescriptor` contient un attribut `EntityID`.</span><span class="sxs-lookup"><span data-stu-id="319d0-127">The `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="319d0-128">La valeur de l’attribut `EntityID` représente l’émetteur, autrement dit, le service d’émission de jeton de sécurité (STS) qui a émis le jeton.</span><span class="sxs-lookup"><span data-stu-id="319d0-128">The value of the `EntityID` attribute represents the issuer, that is, the security token service (STS) that issued the token.</span></span> <span data-ttu-id="319d0-129">Il est important de valider l’émetteur lorsque vous recevez un jeton.</span><span class="sxs-lookup"><span data-stu-id="319d0-129">It is important to validate the issuer when you receive a token.</span></span>

<span data-ttu-id="319d0-130">Les métadonnées suivantes montrent un exemple d’élément `EntityDescriptor` propre au client avec un élément `EntityID`.</span><span class="sxs-lookup"><span data-stu-id="319d0-130">The following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="319d0-131">Vous pouvez remplacer l’ID client dans le point de terminaison indépendant du client par votre ID client pour créer une valeur `EntityID` propre au client .</span><span class="sxs-lookup"><span data-stu-id="319d0-131">You can replace the tenant ID in the tenant-independent endpoint with your tenant ID to create a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="319d0-132">La valeur qui en résulte est identique à celle de l’émetteur du jeton.</span><span class="sxs-lookup"><span data-stu-id="319d0-132">The resulting value will be the same as the token issuer.</span></span> <span data-ttu-id="319d0-133">La stratégie permet à une application mutualisée de valider l’émetteur pour un client donné.</span><span class="sxs-lookup"><span data-stu-id="319d0-133">The strategy allows a multi-tenant application to validate the issuer for a given tenant.</span></span>

<span data-ttu-id="319d0-134">Les métadonnées suivantes montrent un exemple d’élément `EntityID` indépendant du client.</span><span class="sxs-lookup"><span data-stu-id="319d0-134">The following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="319d0-135">Notez que le `{tenant}` est un littéral et non un espace réservé.</span><span class="sxs-lookup"><span data-stu-id="319d0-135">Please note, that the `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="319d0-136">Certificats de signature de jeton</span><span class="sxs-lookup"><span data-stu-id="319d0-136">Token signing certificates</span></span>
<span data-ttu-id="319d0-137">Lorsqu’un service reçoit un jeton émis par un client Azure AD, la signature du jeton doit être validée avec une clé de signature qui est publiée dans le document des métadonnées de fédération.</span><span class="sxs-lookup"><span data-stu-id="319d0-137">When a service receives a token that is issued by a Azure AD tenant, the signature of the token must be validated with a signing key that is published in the federation metadata document.</span></span> <span data-ttu-id="319d0-138">Les métadonnées de fédération incluent la partie publique des certificats utilisés par les clients pour la signature de jetons.</span><span class="sxs-lookup"><span data-stu-id="319d0-138">The federation metadata includes the public portion of the certificates that the tenants use for token signing.</span></span> <span data-ttu-id="319d0-139">Les octets bruts du certificat s’affichent dans l’élément `KeyDescriptor` .</span><span class="sxs-lookup"><span data-stu-id="319d0-139">The certificate raw bytes appear in the `KeyDescriptor` element.</span></span> <span data-ttu-id="319d0-140">Le certificat de signature de jetons est valide pour la signature uniquement si la valeur de l’attribut `use` est `signing`.</span><span class="sxs-lookup"><span data-stu-id="319d0-140">The token signing certificate is valid for signing only when the value of the `use` attribute is `signing`.</span></span>

<span data-ttu-id="319d0-141">Un document des métadonnées de fédération publié par Azure AD peut avoir plusieurs clés de signature, par exemple lorsqu’Azure AD se prépare à mettre à jour le certificat de signature.</span><span class="sxs-lookup"><span data-stu-id="319d0-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing to update the signing certificate.</span></span> <span data-ttu-id="319d0-142">Lorsqu’un document des métadonnées de fédération comprend plusieurs certificats, un service qui valide les jetons doit prendre en charge tous les certificats du document.</span><span class="sxs-lookup"><span data-stu-id="319d0-142">When a federation metadata document includes more than one certificate, a service that is validating the tokens should support all certificates in the document.</span></span>

<span data-ttu-id="319d0-143">Les métadonnées suivantes montrent un exemple d’élément `KeyDescriptor` avec une clé de signature.</span><span class="sxs-lookup"><span data-stu-id="319d0-143">The following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

```
<KeyDescriptor use="signing">
<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
<X509Data>
<X509Certificate>
MIIDPjCCAiqgAwIBAgIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTIwNjA3MDcwMDAwWhcNMTQwNjA3MDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEArCz8Sn3GGXmikH2MdTeGY1D711EORX/lVXpr+ecGgqfUWF8MPB07XkYuJ54DAuYT318+2XrzMjOtqkT94VkXmxv6dFGhG8YZ8vNMPd4tdj9c0lpvWQdqXtL1TlFRpD/P6UMEigfN0c9oWDg9U7Ilymgei0UXtf1gtcQbc5sSQU0S4vr9YJp2gLFIGK11Iqg4XSGdcI0QWLLkkC6cBukhVnd6BCYbLjTYy3fNs4DzNdemJlxGl8sLexFytBF6YApvSdus3nFXaMCtBGx16HzkK9ne3lobAwL2o79bP4imEGqg+ibvyNmbrwFGnQrBc1jTF9LyQX9q+louxVfHs6ZiVwIDAQABo2IwYDBeBgNVHQEEVzBVgBCxDDsLd8xkfOLKm4Q/SzjtoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAA4IBAQAkJtxxm/ErgySlNk69+1odTMP8Oy6L0H17z7XGG3w4TqvTUSWaxD4hSFJ0e7mHLQLQD7oV/erACXwSZn2pMoZ89MBDjOMQA+e6QzGB7jmSzPTNmQgMLA8fWCfqPrz6zgH+1F1gNp8hJY57kfeVPBiyjuBmlTEBsBlzolY9dd/55qqfQk6cgSeCbHCy/RU/iep0+UsRMlSgPNNmqhj5gmN2AFVCN96zF694LwuPae5CeR2ZcVknexOWHYjFM0MgUSw0ubnGl0h9AJgGyhvNGcjQqu9vd1xkupFgaN+f7P3p3EVN5csBg5H94jEcQZT7EKeTiZ6bTrpDAnrr8tDCy8ng
</X509Certificate>
</X509Data>
</KeyInfo>
</KeyDescriptor>
  ```

<span data-ttu-id="319d0-144">L’élément `KeyDescriptor` apparaît à deux emplacements du document des métadonnées de fédération : dans la section propre à WS-Federation et dans la section propre à SAML.</span><span class="sxs-lookup"><span data-stu-id="319d0-144">The `KeyDescriptor` element appears in two places in the federation metadata document; in the WS-Federation-specific section and the SAML-specific section.</span></span> <span data-ttu-id="319d0-145">Les certificats publiés dans les deux sections sont identiques.</span><span class="sxs-lookup"><span data-stu-id="319d0-145">The certificates published in both sections will be the same.</span></span>

<span data-ttu-id="319d0-146">Dans la section WS-Federation, un lecteur de métadonnées WS-Federation lit les certificats d’un élément `RoleDescriptor` avec le type `SecurityTokenServiceType`.</span><span class="sxs-lookup"><span data-stu-id="319d0-146">In the WS-Federation-specific section, a WS-Federation metadata reader would read the certificates from a `RoleDescriptor` element with the `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="319d0-147">Les métadonnées suivantes montrent un exemple d’élément `RoleDescriptor` .</span><span class="sxs-lookup"><span data-stu-id="319d0-147">The following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="319d0-148">Dans la section SAML, un lecteur de métadonnées WS-Federation lit les certificats d’un élément `IDPSSODescriptor` .</span><span class="sxs-lookup"><span data-stu-id="319d0-148">In the SAML-specific section, a WS-Federation metadata reader would read the certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="319d0-149">Les métadonnées suivantes montrent un exemple d’élément `IDPSSODescriptor` .</span><span class="sxs-lookup"><span data-stu-id="319d0-149">The following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="319d0-150">Il n’existe aucune différence de format entre les certificats spécifiques du client et ceux indépendants du client.</span><span class="sxs-lookup"><span data-stu-id="319d0-150">There are no differences in the format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="319d0-151">URL de point de terminaison WS-Federation</span><span class="sxs-lookup"><span data-stu-id="319d0-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="319d0-152">Les métadonnées de fédération incluent l’URL qu’utilise Azure AD pour la connexion et la déconnexion dans le protocole WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="319d0-152">The federation metadata includes the URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="319d0-153">Ce point de terminaison s’affiche dans l’élément `PassiveRequestorEndpoint` .</span><span class="sxs-lookup"><span data-stu-id="319d0-153">This endpoint appears in the `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="319d0-154">Les métadonnées suivantes montrent un exemple d’élément `PassiveRequestorEndpoint` pour un point de terminaison propre au client.</span><span class="sxs-lookup"><span data-stu-id="319d0-154">The following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="319d0-155">Pour le point de terminaison indépendant du client, l’URL WS-Federation apparaît dans le point de terminaison WS-Federation, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="319d0-155">For the tenant-independent endpoint, the WS-Federation URL appears in the WS-Federation endpoint, as shown in the following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="319d0-156">URL de point de terminaison de protocole SAML</span><span class="sxs-lookup"><span data-stu-id="319d0-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="319d0-157">Les métadonnées de fédération incluent l’URL qu’utilise Azure AD pour la connexion et la déconnexion dans le protocole SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="319d0-157">The federation metadata includes the URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="319d0-158">Ces points de terminaison s’affichent dans l’élément `IDPSSODescriptor` .</span><span class="sxs-lookup"><span data-stu-id="319d0-158">These endpoints appear in the `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="319d0-159">Les URL de connexion et de déconnexion s’affichent dans les éléments `SingleSignOnService` et `SingleLogoutService`.</span><span class="sxs-lookup"><span data-stu-id="319d0-159">The sign-in and sign-out URLs appear in the `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="319d0-160">Les métadonnées suivantes montrent un exemple d’élément `PassiveResistorEndpoint` pour un point de terminaison propre au client.</span><span class="sxs-lookup"><span data-stu-id="319d0-160">The following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="319d0-161">De la même façon, les points de terminaison communs du protocole SAML 2.0 sont publiés dans les métadonnées de fédération indépendantes du client, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="319d0-161">Similarly the endpoints for the common SAML 2.0 protocol endpoints are published in the tenant-independent federation metadata, as shown in the following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
