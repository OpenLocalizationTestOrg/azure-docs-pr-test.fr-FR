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
# <a name="federation-metadata"></a>Métadonnées de fédération
Azure Active Directory (Azure AD) publie un document de métadonnées de fédération pour les services qui est configuré tooaccept les jetons de sécurité hello émis par Azure AD. format de document de métadonnées de fédération Hello est décrite dans hello [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), qui étend [métadonnées pour hello OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a>Points de terminaison de métadonnées spécifiques ou indépendants du client
Azure AD publie des points de terminaison spécifiques et indépendants du client.

Les points de terminaison spécifiques du client sont conçus pour un client donné. métadonnées de fédération spécifiques du client Hello incluent des informations sur le client hello, y compris l’émetteur spécifique du client et les informations de point de terminaison. Les applications qui limitent l’accès tooa un seul locataire utilisent des points de terminaison spécifiques du client.

Points de terminaison indépendant du client fournissent des informations qui sont communes locataires Azure AD de tooall. Ces informations s’appliquent tootenants hébergé sur *login.microsoftonline.com* et est partagé entre les clients. Les points de terminaison indépendants du client sont recommandés pour les applications mutualisées, car ils ne sont pas associés à un client particulier.

## <a name="federation-metadata-endpoints"></a>Points de terminaison de métadonnées de fédération
Azure AD publie des métadonnées de fédération dans `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.

Pour **les points de terminaison spécifiques du client**, hello `TenantDomainName` peut être un des types suivants de hello :

* Un nom de domaine enregistré d’un client Azure AD, par exemple `contoso.onmicrosoft.com`.
* Hello immuable locataire ID du domaine de hello, par exemple `72f988bf-86f1-41af-91ab-2d7cd011db45`.

Pour **les points de terminaison indépendant du locataire**, hello `TenantDomainName` est `common`. Ce document répertorie uniquement les éléments de métadonnées de fédération de hello qui sont les clients Azure AD tooall courants qui sont hébergés au niveau login.microsoftonline.com.

Par exemple, un point de terminaison propre à un client peut être `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`. point de terminaison indépendant du locataire Hello est [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml). Vous pouvez afficher le document de métadonnées de fédération hello en tapant cette URL dans un navigateur.

## <a name="contents-of-federation-metadata"></a>Contenu des métadonnées de fédération
Hello section suivante fournit les informations requises par les services qui consomment des jetons hello émis par Azure AD.

### <a name="entity-id"></a>L’ID d’entité
Hello `EntityDescriptor` élément contient un `EntityID` attribut. Hello valeur Hello `EntityID` attribut représente l’émetteur de hello, autrement dit, hello jeton de sécurité service d’émission de jeton émis hello. Il est l’émetteur de hello toovalidate important lorsque vous recevez un jeton.

Hello métadonnées suivantes présentent un exemple spécifique du client `EntityDescriptor` élément avec un `EntityID` élément.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
Vous pouvez remplacer les ID de client hello dans le point de terminaison indépendant du locataire hello par votre toocreate d’ID de client spécifiques du client `EntityID` valeur. valeur de résultat Hello sera hello identique à celle de l’émetteur de jeton de hello. stratégie de Hello permet à un émetteur de hello toovalidate application mutualisée pour un client donné.

Hello métadonnées suivantes présentent un exemple indépendant du locataire `EntityID` élément. Notez bien que hello `{tenant}` est un littéral, pas un espace réservé.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a>Certificats de signature de jeton
Lorsqu’un service reçoit un jeton émis par un client Azure AD, hello signature du jeton de hello doit être validée avec une clé de signature qui est publiée dans le document de métadonnées de fédération hello. les métadonnées de fédération de Hello incluent la partie publique de hello des certificats hello clients de hello utilisent pour la signature de jetons. nombre d’octets bruts Hello certificat s’affichent dans hello `KeyDescriptor` élément. certificat de signature de jeton de Hello n’est valide pour la signature hello uniquement lorsque la valeur de hello `use` attribut est `signing`.

Un document de métadonnées de fédération publié par Azure AD peut avoir plusieurs clés de signature, par exemple quand Azure AD s’apprête hello tooupdate certificat de signature. Lorsqu’un document de métadonnées de fédération comprend plusieurs certificats, un service qui valide les jetons hello doit prendre en charge tous les certificats dans le document de hello.

Hello métadonnées suivantes présentent un exemple `KeyDescriptor` élément avec une clé de signature.

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

Hello `KeyDescriptor` élément apparaît dans deux emplacements dans le document de métadonnées de fédération hello ; dans les sections hello WS-Federation-specific et SAML-specific de hello. les certificats Hello publiés dans les deux sections sont hello, même.

Dans la section de hello WS-Federation-specific, un lecteur de métadonnées WS-Federation lit les certificats hello d’un `RoleDescriptor` élément avec hello `SecurityTokenServiceType` type.

Hello métadonnées suivantes présentent un exemple `RoleDescriptor` élément.

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

Dans la section de hello SAML-specific, un lecteur de métadonnées WS-Federation lit les certificats hello d’un `IDPSSODescriptor` élément.

Hello métadonnées suivantes présentent un exemple `IDPSSODescriptor` élément.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
Il n’existe aucune différence au format hello des certificats spécifiques du client et indépendants du client.

### <a name="ws-federation-endpoint-url"></a>URL de point de terminaison WS-Federation
métadonnées de fédération Hello incluent hello URL Azure AD utilise pour la connexion et déconnexion uniques dans le protocole WS-Federation. Ce point de terminaison s’affiche dans hello `PassiveRequestorEndpoint` élément.

Hello métadonnées suivantes présentent un exemple `PassiveRequestorEndpoint` , élément pour un point de terminaison spécifiques du client.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
Pour le point de terminaison indépendant du locataire hello, hello URL WS-Federation apparaît dans le point de terminaison hello WS-Federation, comme illustré dans hello suivant l’exemple.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a>URL de point de terminaison de protocole SAML
métadonnées de fédération Hello incluent hello URL qu’Azure AD utilise pour l’authentification unique et la déconnexion uniques dans le protocole SAML 2.0. Ces points de terminaison s’affichent dans hello `IDPSSODescriptor` élément.

Hello connexion et déconnexion URL apparaissent dans hello `SingleSignOnService` et `SingleLogoutService` éléments.

Hello métadonnées suivantes présentent un exemple `PassiveResistorEndpoint` pour un point de terminaison spécifiques du client.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

De même points de terminaison hello points de terminaison de protocole SAML 2.0 commun hello sont publiés dans les métadonnées de fédération indépendantes du locataire hello, comme indiqué dans hello suivant l’exemple.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
