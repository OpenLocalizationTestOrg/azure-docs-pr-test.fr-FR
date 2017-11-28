---
title: "aaaAzure l’authentification unique à protocole SAML | Documents Microsoft"
description: "Cet article décrit hello seul protocole SAML de déconnexion dans Azure Active Directory"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 0e4aa75d-d1ad-4bde-a94c-d8a41fb0abe6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 889c9b3397a601c16ba6971d2b15bfee305576de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Protocole SAML de déconnexion unique
Azure Active Directory (Azure AD) prend en charge hello profil déconnexion unique de navigateur web SAML 2.0. Pour toowork de déconnexion unique correctement, hello **LogoutURL** pour l’application hello doit être inscrits explicitement avec Azure AD lors de l’inscription d’application. Azure AD utilise les utilisateurs de hello LogoutURL tooredirect une fois qu’ils sont déconnectés.

Ce diagramme illustre le flux de travail hello du processus de déconnexion unique hello Azure AD.

![Workflow de déconnexion unique](media/active-directory-single-sign-out-protocol-reference/active-directory-saml-single-sign-out-workflow.png)

## LogoutRequest
Hello service cloud envoie un `LogoutRequest` tooindicate tooAzure AD de message qu’une session a été arrêtée. Hello extrait de code suivant montre un exemple `LogoutRequest` élément.

```
<samlp:LogoutRequest xmlns="urn:oasis:names:tc:SAML:2.0:metadata" ID="idaa6ebe6839094fe4abc4ebd5281ec780" Version="2.0" IssueInstant="2013-03-28T07:10:49.6004822Z" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.workaad.com</Issuer>
  <NameID xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
</samlp:LogoutRequest>
```

### LogoutRequest
Hello `LogoutRequest` élément envoyées tooAzure AD requiert hello suivant d’attributs :

* `ID`: Identifie la demande de déconnexion hello. Hello la valeur de `ID` ne doit pas commencer par un chiffre. Hello typique consiste tooappend **id** toohello représentation sous forme de chaîne d’un GUID.
* `Version`: Valeur hello de cet élément trop**2.0**. Cette valeur est obligatoire.
* `IssueInstant` : chaîne `DateTime` associée à une valeur UTC et ayant le [format aller-retour (« o »)](https://msdn.microsoft.com/library/az4se3k1.aspx). Azure Active Directory attend une valeur de ce type, mais ne l’applique pas.

### Émetteur
Hello `Issuer` élément dans une `LogoutRequest` doit correspondre exactement à celle de hello **ServicePrincipalNames** dans le service cloud hello dans Azure AD. En règle générale, cette option est définie toohello **URI ID d’application** qui est spécifié pendant l’inscription d’application.

### NameID
Hello valeur Hello `NameID` élément doit correspondre exactement à hello `NameID` d’utilisateur de hello est déconnecté.

## LogoutResponse
Azure AD envoie un `LogoutResponse` dans la réponse tooa `LogoutRequest` élément. Hello extrait de code suivant montre un exemple `LogoutResponse`.

```
<samlp:LogoutResponse ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
</samlp:LogoutResponse>
```

### LogoutResponse
Azure AD définit hello `ID`, `Version` et `IssueInstant` valeurs Bonjour `LogoutResponse` élément. Il définit également hello `InResponseTo` toohello valeur de l’élément de hello `ID` attribut Hello `LogoutRequest` qui a obtenu la réponse de hello.

### Émetteur
Azure AD définit cette valeur trop`https://login.microsoftonline.com/<TenantIdGUID>/` où <TenantIdGUID> est ID de client hello du client de hello Azure AD.

valeur hello tooevaluate hello `Issuer` élément, utiliser la valeur hello Hello **URI ID d’application** fourni pendant l’inscription d’application.

### État
Azure AD utilise hello `StatusCode` élément Bonjour `Status` réussite de hello tooindicate élément ou l’échec de la déconnexion. Lorsque hello déconnexion tentative échoue, hello `StatusCode` élément peut également contenir des messages d’erreur personnalisés.
