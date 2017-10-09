---
title: "aaaAzure l’authentification unique sur protocole SAML | Documents Microsoft"
description: "Cet article décrit le protocole d’authentification unique sur SAML hello dans Azure Active Directory"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: ad8437f5-b887-41ff-bd77-779ddafc33fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 435cfe0e7be3f2defd34e8b6f6b0f08596ee1f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Protocole SAML d’authentification unique
Cet article traite des demandes d’authentification hello SAML 2.0 et réponses Azure Active Directory (Azure AD) prend en charge pour l’authentification unique.

schéma de protocole Hello ci-dessous décrit la séquence d’authentification unique de l’hello. le service de cloud (fournisseur de services hello) Hello utilise un toopass de liaison de redirection HTTP un `AuthnRequest` (demande d’authentification) élément tooAzure AD (fournisseur d’identité hello). Azure AD puis utilise une toopost de liaison HTTP post un `Response` service de cloud toohello élément.

![Workflow d’authentification unique](media/active-directory-single-sign-on-protocol-reference/active-directory-saml-single-sign-on-workflow.png)

## AuthnRequest
envoient des services de cloud computing toorequest une authentification utilisateur, un `AuthnRequest` élément tooAzure AD. Voici un exemple d’élément `AuthnRequest` SAML 2.0 :

```
<samlp:AuthnRequest
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="id6c1c178c166d486687be4aaf5e482730"
Version="2.0" IssueInstant="2013-03-18T03:28:54.1839884Z"
xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
</samlp:AuthnRequest>
```


| Paramètre |  | Description |
| --- | --- | --- |
| ID |required |Azure AD utilise cette hello de toopopulate attribut `InResponseTo` attribut Hello a retourné une réponse. ID ne doit pas commencer avec un nombre, par conséquent, une stratégie commune est tooprepend une chaîne comme représentation sous forme de chaîne de toohello « id » d’un GUID. Par exemple, `id6c1c178c166d486687be4aaf5e482730` est un ID valide. |
| Version |required |Il doit s’agir de **2.0**. |
| IssueInstant |required |Chaîne DateTime associée à une valeur UTC et comportant le [format aller-retour (« o »)](https://msdn.microsoft.com/library/az4se3k1.aspx). Azure Active Directory attend une valeur DateTime de ce type, mais pas évaluer ou utilisez la valeur de hello. |
| AssertionConsumerServiceUrl |facultatif |Si fourni, il doit correspondre à hello `RedirectUri` du service de cloud hello dans Azure AD. |
| ForceAuthn |facultatif | Il s’agit d’une valeur booléenne. Si la valeur est true, cela signifie que l’utilisateur hello sera forcé toore-authentifier, même s’ils ont une session valide auprès d’Azure AD. |
| IsPassive |facultatif |Il s’agit d’une valeur booléenne qui spécifie si Azure AD doit authentifier hello utilisateur en mode silencieux, sans intervention de l’utilisateur, à l’aide de cookie de session hello s’il en existe. Si la valeur est true, Azure AD va tenter d’utilisateur de hello tooauthenticate à l’aide de cookie de session hello. |

Tous les autres attributs `AuthnRequest` , tels que Consent, Destination, AssertionConsumerServiceIndex, AttributeConsumerServiceIndex and ProviderName, sont **ignorés**.

Azure AD ignore également hello `Conditions` élément `AuthnRequest`.

### Émetteur
Hello `Issuer` élément dans une `AuthnRequest` doit correspondre exactement à celle de hello **ServicePrincipalNames** dans le service cloud hello dans Azure AD. En règle générale, cette option est définie toohello **URI ID d’application** qui est spécifié pendant l’inscription d’application.

Un exemple d’extrait SAML contenant hello `Issuer` élément ressemble à ceci :

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
```

### NameIDPolicy
Cet élément demande un format d’ID de nom particulier dans la réponse de hello et qu’il est facultatif dans `AuthnRequest` éléments envoyés tooAzure AD.

Voici à quoi ressemble un exemple d’élément `NameIdPolicy` :

```
<NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
```

Si `NameIDPolicy` est fourni, vous pouvez inclure son attribut `Format` facultatif. Hello `Format` attribut peut avoir une seule des valeurs suivantes de hello ; toute autre valeur génère une erreur.

* `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent`: Azure Active Directory émet la revendication NameID de hello comme identificateur par paire.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`: Azure Active Directory émet la revendication NameID de hello au format d’adresse de messagerie.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`: Cette valeur permet de format de revendication d’Azure Active Directory tooselect hello. Azure Active Directory émet hello NameID comme identificateur par paire.
* `urn:oasis:names:tc:SAML:2.0:nameid-format:transient`: Azure Active Directory émet hello NameID revendication comme une valeur générée de manière aléatoire qui est l’opération de l’authentification unique en cours toohello unique. Cela signifie que la valeur de hello est temporaire et ne peut pas être utilisé tooidentify hello l’authentification utilisateur.

Azure AD ignore hello `AllowCreate` attribut.

### RequestAuthnContext
Hello `RequestedAuthnContext` élément spécifie les méthodes d’authentification hello souhaité. Il est facultatif dans `AuthnRequest` éléments envoyés tooAzure AD. Azure AD prend en charge une seule valeur `AuthnContextClassRef` : `urn:oasis:names:tc:SAML:2.0:ac:classes:Password`.

### Scoping
Hello `Scoping` élément, qui inclut une liste de fournisseurs d’identité, est facultatif dans `AuthnRequest` éléments envoyés tooAzure AD.

Si spécifié, n’incluez pas hello `ProxyCount` attribut, `IDPListOption` ou `RequesterID` élément, car elles ne sont pas prises en charge.

### Signature
N’incluez pas d’élément `Signature` dans les éléments `AuthnRequest`, car Azure AD ne prend pas en charge les demandes d’authentification signées.

### Objet
Azure AD ignore hello `Subject` élément de `AuthnRequest` éléments.

## Réponse
Quand une demandé l’authentification réussit, Azure AD publie un service de cloud de toohello de réponse. Une exemple réponse tooa tentative réussie d’ouverture de session ressemble à ceci :

```
<samlp:Response ID="_a4958bfd-e107-4e67-b06d-0d85ade2e76a" Version="2.0" IssueInstant="2013-03-18T07:38:15.144Z" Destination="https://contoso.com/identity/inboundsso.aspx" InResponseTo="id758d0ef385634593a77bdf7e632984b6" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
    ...
  </ds:Signature>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
  <Assertion ID="_bf9c623d-cc20-407a-9a59-c2d0aee84d12" IssueInstant="2013-03-18T07:38:15.144Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      ...
    </ds:Signature>
    <Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
  </Assertion>
</samlp:Response>
```

### Réponse
Hello `Response` élément inclut le résultat de hello de demande d’autorisation de hello. Azure AD définit hello `ID`, `Version` et `IssueInstant` valeurs Bonjour `Response` élément. Il définit également hello suivant d’attributs :

* `Destination`: Quand l’authentification réussit, il a la valeur toohello `RedirectUri` hello fournisseur de services (service cloud).
* `InResponseTo`: Ce paramètre est défini toohello `ID` attribut Hello `AuthnRequest` élément qui a initié la réponse de hello.

### Émetteur
Azure AD définit hello `Issuer` élément trop`https://login.microsoftonline.com/<TenantIDGUID>/` où <TenantIDGUID> est ID de client hello du client de hello Azure AD.

Exemple de réponse contenant l’élément Issuer :

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

### État
Hello `Status` élément transmet la réussite de hello ou l’échec de l’authentification. Il inclut hello `StatusCode` élément, qui contient un code ou un ensemble de codes imbriqués qui représentent l’état hello de demande de hello. Il inclut également hello `StatusMessage` élément, qui contient les messages d’erreur personnalisés générés pendant le processus d’authentification hello.

<!-- TODO: Add a authentication protocol error reference -->

Hello Voici une SAML réponse tooan authentification tentative infructueuse.

```
<samlp:Response ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Requester">
      <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:RequestUnsupported" />
    </samlp:StatusCode>
    <samlp:StatusMessage>AADSTS75006: An error occurred while processing a SAML2 Authentication request. AADSTS90011: hello SAML authentication request property 'NameIdentifierPolicy/SPNameQualifier' is not supported.
Trace ID: 66febed4-e737-49ff-ac23-464ba090d57c
Timestamp: 2013-03-18 08:49:24Z</samlp:StatusMessage>
  </samlp:Status>
```

### Assertion
En outre toohello `ID`, `IssueInstant` et `Version`, AD Azure définit hello suivant éléments Bonjour `Assertion` élément de réponse de hello.

#### Émetteur
Ce paramètre est défini trop`https://sts.windows.net/<TenantIDGUID>/`où <TenantIDGUID> est hello ID hello Azure AD du client.

```
<Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

#### Signature
Azure AD signes hello assertion de réponse tooa réussi l’authentification. Hello `Signature` élément contient une signature numérique que le service cloud hello peut utiliser tooauthenticate hello source tooverify hello l’intégrité de l’assertion de hello.

toogenerate cette signature numérique, Azure AD utilise hello clé de signature Bonjour `IDPSSODescriptor` élément de son document de métadonnées.

```
<ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      digital_signature_here
    </ds:Signature>
```

#### Objet
Cela spécifie le principal hello sujet hello d’instructions hello l’assertion hello. Il contient un `NameID` l’élément, qui représente l’utilisateur authentifié de hello. Hello `NameID` valeur est un identificateur ciblé qui est le fournisseur de service dirigé toohello uniquement audience hello pour le jeton de hello. Elle est persistante : elle peut être révoquée, mais n’est jamais réaffectée. Il est également opaque, elle ne révèle rien sur l’utilisateur de hello et ne peut pas être utilisée comme identificateur pour les requêtes d’attribut.

Hello `Method` attribut Hello `SubjectConfirmation` élément est toujours défini trop`urn:oasis:names:tc:SAML:2.0:cm:bearer`.

```
<Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
</Subject>
```

#### Conditions
Cet élément spécifie les conditions qui définissent hello acceptable utilisent d’assertions SAML.

```
<Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
</Conditions>
```

Hello `NotBefore` et `NotOnOrAfter` attributs spécifient l’intervalle de salutation pendant le hello assertion est valide.

* Hello valeur Hello `NotBefore` attribut est égale tooor légèrement (moins d’une seconde) valeur hello plus tard `IssueInstant` attribut Hello `Assertion` élément. Azure AD ne tient pas compte des différences de temps entre lui-même et hello cloud service (fournisseur de services) et n’ajoute pas de tout temps toothis de mémoire tampon.
* Hello valeur Hello `NotOnOrAfter` attribut est de 70 minutes plus tard que valeur hello hello `NotBefore` attribut.

#### Public ciblé
Contient un URI qui identifie une audience visée. Azure AD définit cette valeur toohello d’élément de valeur hello `Issuer` élément Hello `AuthnRequest` qui hello authentification unique initiée par. tooevaluate hello `Audience` , utilisez la valeur hello hello `App ID URI` spécifié lors de l’inscription d’application.

```
<AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
</AudienceRestriction>
```

Comme hello `Issuer` valeur hello `Audience` valeur doit correspondre exactement à un des noms principaux de hello service qui représente le service de cloud computing hello dans Azure AD. Toutefois, si hello valeur Hello `Issuer` élément n’est pas une valeur d’URI, hello `Audience` valeur dans la réponse de hello est hello `Issuer` value préfixé avec `spn:`.

#### AttributeStatement
Contient des revendications sur le sujet de hello ou un utilisateur. Hello extrait de code suivant contient un exemple de `AttributeStatement` élément. points de suspension Hello indique cet élément hello peut inclure plusieurs attributs et valeurs d’attribut.

```
<AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
</AttributeStatement>
```        

* **Revendication Name** : hello valeur Hello `Name` attribut (`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`) est le nom d’utilisateur hello principal d’utilisateur de hello authentifié, tel que `testuser@managedtenant.com`.
* **Revendication ObjectIdentifier** : hello valeur Hello `ObjectIdentifier` attribut (`http://schemas.microsoft.com/identity/claims/objectidentifier`) est hello `ObjectId` d’objet de répertoire hello représentant hello utilisateur authentifié dans Azure AD. `ObjectId`est immuable, globalement unique et réutilisable sécurisé identificateur Hello authentifié l’utilisateur.

#### AuthnStatement
Cet élément déclare que l’objet hello assertion a été authentifié par un moyen précis à un moment donné.

* Hello `AuthnInstant` attribut spécifie la durée hello utilisateur hello authentifié auprès d’Azure AD.
* Hello `AuthnContext` élément spécifie le contexte d’authentification hello utilisé utilisateur de hello tooauthenticate.

```
<AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
</AuthnStatement>
```