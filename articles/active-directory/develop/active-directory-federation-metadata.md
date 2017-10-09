---
title: "aaaAzure AD métadonnées de fédération | Documents Microsoft"
description: "Cet article décrit le document de métadonnées de fédération hello Azure Active Directory publie des services qui acceptent les jetons d’Azure Active Directory."
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
ms.openlocfilehash: 23535bcd5eeb3e9b2e17d89a9b0420fc98bd3895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="federation-metadata"></a><span data-ttu-id="6d45a-103">Métadonnées de fédération</span><span class="sxs-lookup"><span data-stu-id="6d45a-103">Federation metadata</span></span>
<span data-ttu-id="6d45a-104">Azure Active Directory (Azure AD) publie un document de métadonnées de fédération pour les services qui est configuré tooaccept les jetons de sécurité hello émis par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d45a-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured tooaccept hello security tokens that Azure AD issues.</span></span> <span data-ttu-id="6d45a-105">format de document de métadonnées de fédération Hello est décrite dans hello [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), qui étend [métadonnées pour hello OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span><span class="sxs-lookup"><span data-stu-id="6d45a-105">hello federation metadata document format is described in hello [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for hello OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="6d45a-106">Points de terminaison de métadonnées spécifiques ou indépendants du client</span><span class="sxs-lookup"><span data-stu-id="6d45a-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="6d45a-107">Azure AD publie des points de terminaison spécifiques et indépendants du client.</span><span class="sxs-lookup"><span data-stu-id="6d45a-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="6d45a-108">Les points de terminaison spécifiques du client sont conçus pour un client donné.</span><span class="sxs-lookup"><span data-stu-id="6d45a-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="6d45a-109">métadonnées de fédération spécifiques du client Hello incluent des informations sur le client hello, y compris l’émetteur spécifique du client et les informations de point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="6d45a-109">hello tenant-specific federation metadata includes information about hello tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="6d45a-110">Les applications qui limitent l’accès tooa un seul locataire utilisent des points de terminaison spécifiques du client.</span><span class="sxs-lookup"><span data-stu-id="6d45a-110">Applications that restrict access tooa single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="6d45a-111">Points de terminaison indépendant du client fournissent des informations qui sont communes locataires Azure AD de tooall.</span><span class="sxs-lookup"><span data-stu-id="6d45a-111">Tenant-independent endpoints provide information that is common tooall Azure AD tenants.</span></span> <span data-ttu-id="6d45a-112">Ces informations s’appliquent tootenants hébergé sur *login.microsoftonline.com* et est partagé entre les clients.</span><span class="sxs-lookup"><span data-stu-id="6d45a-112">This information applies tootenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="6d45a-113">Les points de terminaison indépendants du client sont recommandés pour les applications mutualisées, car ils ne sont pas associés à un client particulier.</span><span class="sxs-lookup"><span data-stu-id="6d45a-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="6d45a-114">Points de terminaison de métadonnées de fédération</span><span class="sxs-lookup"><span data-stu-id="6d45a-114">Federation metadata endpoints</span></span>
<span data-ttu-id="6d45a-115">Azure AD publie des métadonnées de fédération dans `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="6d45a-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="6d45a-116">Pour **les points de terminaison spécifiques du client**, hello `TenantDomainName` peut être un des types suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="6d45a-116">For **tenant-specific endpoints**, hello `TenantDomainName` can be one of hello following types:</span></span>

* <span data-ttu-id="6d45a-117">Un nom de domaine enregistré d’un client Azure AD, par exemple `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="6d45a-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="6d45a-118">Hello immuable locataire ID du domaine de hello, par exemple `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="6d45a-118">hello immutable tenant ID of hello domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="6d45a-119">Pour **les points de terminaison indépendant du locataire**, hello `TenantDomainName` est `common`.</span><span class="sxs-lookup"><span data-stu-id="6d45a-119">For **tenant-independent endpoints**, hello `TenantDomainName` is `common`.</span></span> <span data-ttu-id="6d45a-120">Ce document répertorie uniquement les éléments de métadonnées de fédération de hello qui sont les clients Azure AD tooall courants qui sont hébergés au niveau login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="6d45a-120">This document lists only hello Federation Metadata elements that are common tooall Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="6d45a-121">Par exemple, un point de terminaison propre à un client peut être `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="6d45a-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="6d45a-122">point de terminaison indépendant du locataire Hello est [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="6d45a-122">hello tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="6d45a-123">Vous pouvez afficher le document de métadonnées de fédération hello en tapant cette URL dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="6d45a-123">You can view hello federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="6d45a-124">Contenu des métadonnées de fédération</span><span class="sxs-lookup"><span data-stu-id="6d45a-124">Contents of federation Metadata</span></span>
<span data-ttu-id="6d45a-125">Hello section suivante fournit les informations requises par les services qui consomment des jetons hello émis par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d45a-125">hello following section provides information needed by services that consume hello tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="6d45a-126">L’ID d’entité</span><span class="sxs-lookup"><span data-stu-id="6d45a-126">Entity ID</span></span>
<span data-ttu-id="6d45a-127">Hello `EntityDescriptor` élément contient un `EntityID` attribut.</span><span class="sxs-lookup"><span data-stu-id="6d45a-127">hello `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="6d45a-128">Hello valeur Hello `EntityID` attribut représente l’émetteur de hello, autrement dit, hello jeton de sécurité service d’émission de jeton émis hello.</span><span class="sxs-lookup"><span data-stu-id="6d45a-128">hello value of hello `EntityID` attribute represents hello issuer, that is, hello security token service (STS) that issued hello token.</span></span> <span data-ttu-id="6d45a-129">Il est l’émetteur de hello toovalidate important lorsque vous recevez un jeton.</span><span class="sxs-lookup"><span data-stu-id="6d45a-129">It is important toovalidate hello issuer when you receive a token.</span></span>

<span data-ttu-id="6d45a-130">Hello métadonnées suivantes présentent un exemple spécifique du client `EntityDescriptor` élément avec un `EntityID` élément.</span><span class="sxs-lookup"><span data-stu-id="6d45a-130">hello following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="6d45a-131">Vous pouvez remplacer les ID de client hello dans le point de terminaison indépendant du locataire hello par votre toocreate d’ID de client spécifiques du client `EntityID` valeur.</span><span class="sxs-lookup"><span data-stu-id="6d45a-131">You can replace hello tenant ID in hello tenant-independent endpoint with your tenant ID toocreate a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="6d45a-132">valeur de résultat Hello sera hello identique à celle de l’émetteur de jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="6d45a-132">hello resulting value will be hello same as hello token issuer.</span></span> <span data-ttu-id="6d45a-133">stratégie de Hello permet à un émetteur de hello toovalidate application mutualisée pour un client donné.</span><span class="sxs-lookup"><span data-stu-id="6d45a-133">hello strategy allows a multi-tenant application toovalidate hello issuer for a given tenant.</span></span>

<span data-ttu-id="6d45a-134">Hello métadonnées suivantes présentent un exemple indépendant du locataire `EntityID` élément.</span><span class="sxs-lookup"><span data-stu-id="6d45a-134">hello following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="6d45a-135">Notez bien que hello `{tenant}` est un littéral, pas un espace réservé.</span><span class="sxs-lookup"><span data-stu-id="6d45a-135">Please note, that hello `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="6d45a-136">Certificats de signature de jeton</span><span class="sxs-lookup"><span data-stu-id="6d45a-136">Token signing certificates</span></span>
<span data-ttu-id="6d45a-137">Lorsqu’un service reçoit un jeton émis par un client Azure AD, hello signature du jeton de hello doit être validée avec une clé de signature qui est publiée dans le document de métadonnées de fédération hello.</span><span class="sxs-lookup"><span data-stu-id="6d45a-137">When a service receives a token that is issued by a Azure AD tenant, hello signature of hello token must be validated with a signing key that is published in hello federation metadata document.</span></span> <span data-ttu-id="6d45a-138">les métadonnées de fédération de Hello incluent la partie publique de hello des certificats hello clients de hello utilisent pour la signature de jetons.</span><span class="sxs-lookup"><span data-stu-id="6d45a-138">hello federation metadata includes hello public portion of hello certificates that hello tenants use for token signing.</span></span> <span data-ttu-id="6d45a-139">nombre d’octets bruts Hello certificat s’affichent dans hello `KeyDescriptor` élément.</span><span class="sxs-lookup"><span data-stu-id="6d45a-139">hello certificate raw bytes appear in hello `KeyDescriptor` element.</span></span> <span data-ttu-id="6d45a-140">certificat de signature de jeton de Hello n’est valide pour la signature hello uniquement lorsque la valeur de hello `use` attribut est `signing`.</span><span class="sxs-lookup"><span data-stu-id="6d45a-140">hello token signing certificate is valid for signing only when hello value of hello `use` attribute is `signing`.</span></span>

<span data-ttu-id="6d45a-141">Un document de métadonnées de fédération publié par Azure AD peut avoir plusieurs clés de signature, par exemple quand Azure AD s’apprête hello tooupdate certificat de signature.</span><span class="sxs-lookup"><span data-stu-id="6d45a-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing tooupdate hello signing certificate.</span></span> <span data-ttu-id="6d45a-142">Lorsqu’un document de métadonnées de fédération comprend plusieurs certificats, un service qui valide les jetons hello doit prendre en charge tous les certificats dans le document de hello.</span><span class="sxs-lookup"><span data-stu-id="6d45a-142">When a federation metadata document includes more than one certificate, a service that is validating hello tokens should support all certificates in hello document.</span></span>

<span data-ttu-id="6d45a-143">Hello métadonnées suivantes présentent un exemple `KeyDescriptor` élément avec une clé de signature.</span><span class="sxs-lookup"><span data-stu-id="6d45a-143">hello following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="6d45a-144">Hello `KeyDescriptor` élément apparaît dans deux emplacements dans le document de métadonnées de fédération hello ; dans les sections hello WS-Federation-specific et SAML-specific de hello.</span><span class="sxs-lookup"><span data-stu-id="6d45a-144">hello `KeyDescriptor` element appears in two places in hello federation metadata document; in hello WS-Federation-specific section and hello SAML-specific section.</span></span> <span data-ttu-id="6d45a-145">les certificats Hello publiés dans les deux sections sont hello, même.</span><span class="sxs-lookup"><span data-stu-id="6d45a-145">hello certificates published in both sections will be hello same.</span></span>

<span data-ttu-id="6d45a-146">Dans la section de hello WS-Federation-specific, un lecteur de métadonnées WS-Federation lit les certificats hello d’un `RoleDescriptor` élément avec hello `SecurityTokenServiceType` type.</span><span class="sxs-lookup"><span data-stu-id="6d45a-146">In hello WS-Federation-specific section, a WS-Federation metadata reader would read hello certificates from a `RoleDescriptor` element with hello `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="6d45a-147">Hello métadonnées suivantes présentent un exemple `RoleDescriptor` élément.</span><span class="sxs-lookup"><span data-stu-id="6d45a-147">hello following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="6d45a-148">Dans la section de hello SAML-specific, un lecteur de métadonnées WS-Federation lit les certificats hello d’un `IDPSSODescriptor` élément.</span><span class="sxs-lookup"><span data-stu-id="6d45a-148">In hello SAML-specific section, a WS-Federation metadata reader would read hello certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="6d45a-149">Hello métadonnées suivantes présentent un exemple `IDPSSODescriptor` élément.</span><span class="sxs-lookup"><span data-stu-id="6d45a-149">hello following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="6d45a-150">Il n’existe aucune différence au format hello des certificats spécifiques du client et indépendants du client.</span><span class="sxs-lookup"><span data-stu-id="6d45a-150">There are no differences in hello format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="6d45a-151">URL de point de terminaison WS-Federation</span><span class="sxs-lookup"><span data-stu-id="6d45a-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="6d45a-152">métadonnées de fédération Hello incluent hello URL Azure AD utilise pour la connexion et déconnexion uniques dans le protocole WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="6d45a-152">hello federation metadata includes hello URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="6d45a-153">Ce point de terminaison s’affiche dans hello `PassiveRequestorEndpoint` élément.</span><span class="sxs-lookup"><span data-stu-id="6d45a-153">This endpoint appears in hello `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="6d45a-154">Hello métadonnées suivantes présentent un exemple `PassiveRequestorEndpoint` , élément pour un point de terminaison spécifiques du client.</span><span class="sxs-lookup"><span data-stu-id="6d45a-154">hello following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="6d45a-155">Pour le point de terminaison indépendant du locataire hello, hello URL WS-Federation apparaît dans le point de terminaison hello WS-Federation, comme illustré dans hello suivant l’exemple.</span><span class="sxs-lookup"><span data-stu-id="6d45a-155">For hello tenant-independent endpoint, hello WS-Federation URL appears in hello WS-Federation endpoint, as shown in hello following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="6d45a-156">URL de point de terminaison de protocole SAML</span><span class="sxs-lookup"><span data-stu-id="6d45a-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="6d45a-157">métadonnées de fédération Hello incluent hello URL qu’Azure AD utilise pour l’authentification unique et la déconnexion uniques dans le protocole SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="6d45a-157">hello federation metadata includes hello URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="6d45a-158">Ces points de terminaison s’affichent dans hello `IDPSSODescriptor` élément.</span><span class="sxs-lookup"><span data-stu-id="6d45a-158">These endpoints appear in hello `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="6d45a-159">Hello connexion et déconnexion URL apparaissent dans hello `SingleSignOnService` et `SingleLogoutService` éléments.</span><span class="sxs-lookup"><span data-stu-id="6d45a-159">hello sign-in and sign-out URLs appear in hello `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="6d45a-160">Hello métadonnées suivantes présentent un exemple `PassiveResistorEndpoint` pour un point de terminaison spécifiques du client.</span><span class="sxs-lookup"><span data-stu-id="6d45a-160">hello following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="6d45a-161">De même points de terminaison hello points de terminaison de protocole SAML 2.0 commun hello sont publiés dans les métadonnées de fédération indépendantes du locataire hello, comme indiqué dans hello suivant l’exemple.</span><span class="sxs-lookup"><span data-stu-id="6d45a-161">Similarly hello endpoints for hello common SAML 2.0 protocol endpoints are published in hello tenant-independent federation metadata, as shown in hello following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
