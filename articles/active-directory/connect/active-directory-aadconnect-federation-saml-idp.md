---
title: "Azure AD Connect : utiliser un fournisseur d’identité SAML 2.0 pour l’authentification unique | Documents Microsoft"
description: "Cette rubrique décrit l’utilisation d’un IdP compatible SAML 2.0 pour l’authentification unique."
services: active-directory
author: billmath
manager: femila
ms.custom: it-pro
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f9653dc44fb284a9b3c1988f623c33f27ae148cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
#  <a name="use-a-saml-20-identity-provider-idp-for-single-sign-on"></a>Utiliser un fournisseur d’identité (IdP) SAML 2.0 pour l’authentification unique

Cette rubrique contient des informations sur l’utilisation d’un SAML 2.0 profil SP-Lite compatible selon le fournisseur d’identité hello préféré Service de jeton de sécurité (STS) / fournisseur d’identité. Cela est utile lorsque vous avez déjà un répertoire d’utilisateurs et un Store de mots de passe local accessibles à l’aide de SAML 2.0. Annuaire d’utilisateurs existant peut être utilisé pour l’authentification tooOffice 365 et d’autres ressources sécurisées par AD Azure. Hello SP-Lite SAML 2.0 profil repose sur hello largement utilisé tooprovide standard de Security Assertion Markup Language (SAML) fédéré identité une ouverture de session et la structure d’échange d’attributs.

>[!NOTE]
>Pour obtenir la liste de 3e partie Idps qui ont été testés pour une utilisation avec Azure AD voir hello [liste de compatibilité de fédération Azure AD](active-directory-aadconnect-federation-compatibility.md)

Microsoft prend en charge cette expérience d’authentification sous forme d’intégration hello d’un service cloud Microsoft, tels qu’Office 365, avec votre SAML 2.0 correctement configuré profil en fonction des fournisseurs d’identité. Fournisseurs d’identité SAML 2.0 sont des produits tiers, et par conséquent, Microsoft ne fournit aucun support pour le déploiement de hello, configuration, résolution des problèmes de meilleures pratiques concernant les. Une fois correctement configuré, l’intégration de hello avec hello SAML 2.0 fournisseur d’identité peut être testé à l’aide de hello outil Analyseur de connectivité Microsoft décrit plus en détail ci-dessous. Pour plus d’informations sur votre fournisseur d’identité basé sur un profil SP-Lite SAML 2.0, demandez à l’organisation hello qui l’a fournie.

>[!IMPORTANT]
>Seul un ensemble limité de clients est disponible dans ce scénario d’authentification avec les fournisseurs d’identité SAML 2.0, cela inclut :

>- Clients basés sur le Web tels que Outlook Web Access et Sharepoint Online
- Les clients de messagerie riches qui utilisent l’authentification de base et une méthode d’accès Exchange prise en charge comme IMAP, POP, Active Sync, MAPI, etc. (hello Enhanced Client protocole de point de terminaison toobe requis déployé), y compris :
    - Microsoft Outlook 2010/Outlook 2013/Outlook 2016, Apple iPhone (différentes versions d’iOS)
    - Différents appareils Google Android
    - Windows Phone 7, Windows Phone 7.8 et Windows Phone 8.0
    - Client de messagerie Windows 8 et client de messagerie Windows 8.1
    - Client de messagerie Windows 10

Tous les autres clients ne sont pas disponibles dans ce scénario d’authentification avec votre fournisseur d’identité SAML 2.0. Par exemple, client de bureau hello Lync 2010 n’est pas en mesure de toologin en service hello avec votre fournisseur d’identité SAML 2.0 configuré pour l’authentification unique.

## <a name="azure-ad-saml-20-protocol-requirements"></a>Exigences du protocole SAML 2.0 Azure AD
Cette rubrique contient les exigences détaillées sur le protocole de hello et que votre fournisseur d’identité SAML 2.0 doit implémenter toofederate avec Azure AD tooenable authentification tooone ou plusieurs services de cloud de Microsoft (par exemple, Office 365) de la mise en forme des messages. partie de confiance Hello SAML 2.0 (SP-STS) pour un service de cloud Microsoft utilisé dans ce scénario est Azure AD.

Il est recommandé de vérifier votre identité fournisseur sortie messages être comme similaire toohello fourni traces échantillon que possible de SAML 2.0. En outre, utilisez les valeurs d’attribut spécifiques à partir de hello a fourni des métadonnées Azure AD lorsque cela est possible. Une fois que vous êtes satisfait de vos messages de sortie, vous pouvez tester hello Analyseur de connectivité Microsoft comme décrit ci-dessous.

les métadonnées Hello Azure AD peuvent être téléchargée à partir de cette URL : [https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml](http://https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml).
Pour les clients à l’aide de la Chine hello instance propres à la Chine d’Office 365, hello après le point de terminaison de fédération doit être utilisé : [https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml](https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml).

## <a name="saml-protocol-requirements"></a>Exigences du protocole SAML
Cette section détaille comment les paires de messages de demande et de réponse hello sont regroupés dans ordre toohelp vous tooformat vos messages correctement.

Azure AD peut être configuré toowork aux fournisseurs d’identité qui utilisent le profil SP-Lite SAML 2.0 de hello avec certaines exigences indiquées ci-dessous. Hello exemples SAML demande et réponse de messages en même temps que les tests automatisés et manuels, vous pouvez travailler interopérabilité tooachieve avec Azure AD.

## <a name="signature-block-requirements"></a>Exigences des blocs de signature
Au sein de la réponse SAML de hello nœud de Signature de message hello contient des informations sur la signature numérique de hello pour le message de type hello lui-même. bloc de signature Hello a hello suivant les exigences :

1. nœud d’assertion Hello lui-même doit être signé.
2.  algorithme de Hello RSA-sha1 doit être utilisé comme hello DigestMethod. Les autres algorithmes de signature numérique ne sont pas acceptés.
   `<ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>`
3.  Vous pouvez aussi signer le document XML de hello. 
4.  Hello algorithme Transform doit correspondre les valeurs hello Bonjour suivant l’exemple :`<ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
       <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>`
9.  Hello algorithme SignatureMethod doit correspondre à hello suivant l’exemple :`<ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>`

## <a name="supported-bindings"></a>Liaisons prises en charge
Transport de hello les liaisons sont des paramètres de communication requises liés. suivant les exigences de Hello applique les liaisons de toohello

1. HTTPS est requis de hello transport.
2.  Azure AD exige HTTP POST pour la soumission de jeton au cours de la connexion
3.  Azure AD utilise HTTP POST pour le fournisseur d’identité toohello demande hello d’authentification et de redirection pour le fournisseur d’identité toohello message hello fermeture de session.

## <a name="required-attributes"></a>Attributs requis
Ce tableau présente les exigences des attributs spécifiques dans le message de type hello SAML 2.0.
 
|Attribut|Description|
| ----- | ----- |
|NameID|valeur Hello de cette assertion doit être hello identique ImmutableID de l’utilisateur hello Azure AD. Il peut être des caractères alphanumériques too64. Tous les caractères HTML non sécurisés doivent être encodés, par exemple un caractère « + » est affiché comme «.2B ».|
|IDPEmail|Hello nom d’utilisateur Principal (UPN) est répertorié dans hello SAML le réponse comme un élément avec hello nom IDPEmail ce est hello UserPrincipalName (UPN de l’utilisateur) dans Azure AD/Office 365. Hello UPN est au format d’adresse de messagerie. Valeur UPN dans Windows Office 365 (Azure Active Directory).|
|Émetteur|Il s’agit de toobe requis un URI du fournisseur d’identité hello. Vous ne devez pas réutiliser hello émetteur à partir d’exemples de messages hello. Si vous avez plusieurs domaines de niveau supérieur dans votre hello de locataires Azure AD émetteur doit correspondre à hello spécifié paramètre URI configuré par domaine.|

>[!IMPORTANT]
>Actuellement, Azure AD prend en charge hello suivant l’URI au Format NameID de SAML 2.0:urn:oasis:names:tc:SAML:2.0:nameid-format : persistant.

## <a name="sample-saml-request-and-response-messages"></a>Exemple de messages de requête et de réponse SAML
Une paire de messages de demande et de réponse est indiquée pour l’échange de messages de l’authentification hello.
Il s’agit d’un exemple de message de demande est envoyé à partir du fournisseur d’identité SAML 2.0 Azure AD tooa exemple. fournisseur d’identité SAML 2.0 Hello exemple est que les Services de fédération Active Directory (AD FS) configuré le protocole SAML-P de toouse. Les tests d’interopérabilité ont également été effectués avec d’autres fournisseurs d’identité SAML 2.0.

    `<samlp:AuthnRequest xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" ID="_7171b0b2-19f2-4ba2-8f94-24b5e56b7f1e" IssueInstant="2014-01-30T16:18:35Z" Version="2.0" AssertionConsumerServiceIndex="0" >
    <saml:Issuer>urn:federation:MicrosoftOnline</saml:Issuer>
    <samlp:NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
    </samlp:AuthnRequest>`

Il s’agit d’un exemple de message de réponse est envoyé de hello exemple SAML 2.0 identité fournisseur tooAzure AD / Office 365.

    `<samlp:Response ID="_592c022f-e85e-4d23-b55b-9141c95cd2a5" Version="2.0" IssueInstant="2014-01-31T15:36:31.357Z" Destination="https://login.microsoftonline.com/login.srf" Consent="urn:oasis:names:tc:SAML:2.0:consent:unspecified" InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
    </samlp:Status>
    <Assertion ID="_7e3c1bcd-f180-4f78-83e1-7680920793aa" IssueInstant="2014-01-31T15:36:31.279Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
        <ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
        <ds:Reference URI="#_7e3c1bcd-f180-4f78-83e1-7680920793aa">
          <ds:Transforms>
            <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
            <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
          </ds:Transforms>
          <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
          <ds:DigestValue>CBn/5YqbheaJP425c0pHva9PhNY=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
      <ds:SignatureValue>TciWMyHW2ZODrh/2xrvp5ggmcHBFEd9vrp6DYXp+hZWJzmXMmzwmwS8KNRJKy8H7XqBsdELA1Msqi8I3TmWdnoIRfM/ZAyUppo8suMu6Zw+boE32hoQRnX9EWN/f0vH6zA/YKTzrjca6JQ8gAV1ErwvRWDpyMcwdYCiWALv9ScbkAcebOE1s1JctZ5RBXggdZWrYi72X+I4i6WgyZcIGai/rZ4v2otoWAEHS0y1yh1qT7NDPpl/McDaTGkNU6C+8VfjD78DrUXEcAfKvPgKlKrOMZnD1lCGsViimGY+LSuIdY45MLmyaa5UT4KWph6dA==</ds:SignatureValue>
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
        <ds:X509Data>
          <ds:X509Certificate>MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyhBREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDTE1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9ybWVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/+3ZWxd9T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEMb2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcCAwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvyJOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBySx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==</ds:X509Certificate>
        </ds:X509Data>
      </KeyInfo>
    </ds:Signature>
    <Subject>
      <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">ABCDEG1234567890</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" NotOnOrAfter="2014-01-31T15:41:31.357Z" Recipient="https://login.microsoftonline.com/login.srf" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2014-01-31T15:36:31.263Z" NotOnOrAfter="2014-01-31T16:36:31.263Z">
      <AudienceRestriction>
        <Audience>urn:federation:MicrosoftOnline</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="IDPEmail">
        <AttributeValue>administrator@contoso.com</AttributeValue>
      </Attribute>
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2014-01-31T15:36:30.200Z" SessionIndex="_7e3c1bcd-f180-4f78-83e1-7680920793aa">
      <AuthnContext>
        <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
    </Assertion>
    </samlp:Response>`

## <a name="configure-your-saml-20-compliant-identity-provider"></a>Configurer votre fournisseur d’identité compatible SAML 2.0
Cette rubrique contient des instructions sur la façon dont tooconfigure votre toofederate de fournisseur d’identité SAML 2.0 avec Azure AD tooenable accès avec authentification unique tooone ou plus cloud de Microsoft services (par exemple, Office 365) à l’aide du protocole de hello SAML 2.0. Hello SAML 2.0 de confiance pour un service de cloud Microsoft utilisé dans ce scénario est Azure AD.

## <a name="add-azure-ad-metadata"></a>Ajouter les métadonnées Azure AD
Votre fournisseur d’identité SAML 2.0 doit tooinformation tooadhere sur la partie de confiance hello Azure AD. Azure AD publie des métadonnées sur https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml.

Il est recommandé de toujours importer les métadonnées hello dernière Azure AD lors de la configuration de votre fournisseur d’identité SAML 2.0. Notez que Azure AD ne lit pas les métadonnées du fournisseur d’identité hello.

## <a name="add-azure-ad-as-a-relying-party"></a>Ajouter Azure AD en tant que partie utilisatrice
Vous avez tooenable la communication entre votre fournisseur d’identité SAML 2.0 et le Azure AD. Cette configuration sera dépend de votre fournisseur d’identité spécifique, consultez la toodocumentation pour celle-ci. Vous pouvez généralement affecter hello partie de confiance tiers ID toohello identique à l’entityID hello à partir des métadonnées de hello Azure AD.

>[!NOTE]
>Vérifiez l’horloge de hello sur votre serveur de fournisseur d’identité SAML 2.0 est la source de temps précise tooan synchronisés. Une heure inexacte peut entraîner des connexions fédérées toofail.

## <a name="install-windows-powershell-for-sign-on-with-saml-20-identity-provider"></a>Installez Windows PowerShell pour l’authentification avec le fournisseur d’identité SAML 2.0
Après avoir configuré votre fournisseur d’identité SAML 2.0 pour une utilisation avec l’authentification Azure AD, étape suivante de hello est toodownload et installation Bonjour Azure Module Active Directory pour Windows PowerShell. Une fois installé, vous allez utiliser ces applets de commande tooconfigure vos domaines Azure AD en tant que domaines fédérés.

Bonjour Azure Module Active Directory pour Windows PowerShell est un téléchargement pour la gestion des données de votre organisation dans Azure AD. Ce module installe un ensemble d’applets de commande tooWindows PowerShell ; vous exécutez ces tooset applets de commande d’accès de l’authentification unique tooAzure AD et à son tour tooall Hello cloud services auxquels vous êtes abonné. Pour obtenir des instructions sur la façon dont toodownload et installez hello applets de commande, consultez [http://technet.microsoft.com/library/jj151815.aspx](http://technet.microsoft.com/library/jj151815.aspx)

## <a name="set-up-a-trust-between-your-saml-identity-provider-and-azure-ad"></a>Configurer une approbation entre votre fournisseur d’identité SAML et Azure AD
Avant de configurer la fédération sur un domaine Azure AD, un domaine personnalisé doit être configuré. Vous ne pouvez pas fédérer domaine hello par défaut qui est fourni par Microsoft. domaine par défaut Microsoft Hello se termine par « onmicrosoft.com ».
Vous exécutez une série d’applets de commande dans tooadd d’une interface de ligne hello Windows PowerShell ou convertir des domaines pour l’authentification unique.

Chaque domaine Azure Active Directory que vous souhaitez toofederate à l’aide de votre fournisseur d’identité SAML 2.0 doit soit être ajouté en tant que domaine d’authentification unique ou converti toobe un domaine d’authentification unique à partir d’un domaine standard. L’ajout ou la conversion d’un domaine configure une approbation entre votre fournisseur d’identité SAML 2.0 et Azure AD.

Hello procédure suivante vous guide dans la conversion d’un domaine standard tooa domaine fédéré existant à l’aide de SP-Lite SAML 2.0. Notez que votre domaine peut rencontrer une indisponibilité too2 heures qu’après avoir effectué cette étape.

## <a name="configuring-a-domain-in-your-azure-ad-directory-for-federation"></a>Configuration d’un domaine dans votre répertoire Azure AD pour la fédération


1. Se connecter tooyour annuaire Azure AD en tant qu’un administrateur client : MsolService se connecter.
2.  Configurez votre fédération de toouse domaine Office 365 souhaitée avec SAML 2.0 :`$dom = "contoso.com" $BrandName - "Sample SAML 2.0 IDP" $LogOnUrl = "https://WS2012R2-0.contoso.com/passiveLogon" $LogOffUrl = "https://WS2012R2-0.contoso.com/passiveLogOff" $ecpUrl = "https://WS2012R2-0.contoso.com/PAOS" $MyURI = "urn:uri:MySamlp2IDP" $MySigningCert = @" MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyh BREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDT E1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9yb WVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/kupQ VcjKuKLitVDbssFyqbDTjP7WRjlVMWAHBI3kgNT7oE362Gf2WMJFf1b0HcrsgLin7daRXpq4Qi6OA57 sW1YFMj3sqyuTP0eZV3S4+ZbDVob6amsZIdIwxaLP9Zfywg2bLsGnVldB0+XKedZwDbCLCVg+3ZWxd9 T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEM b2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcC AwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9 eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+ CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvy JOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBy Sx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==" "@ $uri = "http://WS2012R2-0.contoso.com/adfs/services/trust" $Protocol = "SAMLP" Set-MsolDomainAuthentication -DomainName $dom -FederationBrandName $dom -Authentication Federated -PassiveLogOnUri $MyURI -ActiveLogOnUri $ecpUrl -SigningCertificate $MySigningCert -IssuerUri $uri -LogOffUri $url -PreferredAuthenticationProtocol $Protocol` 

3.  Vous pouvez obtenir hello chaîne à partir de votre fichier de métadonnées IDP codé en base64 du certificat de signature. Un exemple de cet emplacement a été spécifié mais peut varier légèrement en fonction de votre mise en œuvre.

    `<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol"> <KeyDescriptor use="signing"> <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#"> <X509Data> <X509Certificate>MIIC5jCCAc6gAwIBAgIQLnaxUPzay6ZJsC8HVv/QfTANBgkqhkiG9w0BAQsFADAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwHhcNMTMxMTA0MTgxMzMyWhcNMTQxMTA0MTgxMzMyWjAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCwMdVLTr5YTSRp+ccbSpuuFeXMfABD9mVCi2wtkRwC30TIyPdORz642MkurdxdPCWjwgJ0HW6TvXwcO9afH3OC5V//wEGDoNcI8PV4enCzTYFe/h//w51uqyv48Fbb3lEXs+aVl8155OAj2sO9IX64OJWKey82GQWK3g7LfhWWpp17j5bKpSd9DBH5pvrV+Q1ESU3mx71TEOvikHGCZYitEPywNeVMLRKrevdWI3FAhFjcCSO6nWDiMqCqiTDYOURXIcHVYTSof1YotkJ4tG6mP5Kpjzd4VQvnR7Pjb47nhIYG6iZ3mR1F85Ns9+hBWukQWNN2hcD/uGdPXhpdMVpBAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAK7h7jF7wPzhZ1dPl4e+XMAr8I7TNbhgEU3+oxKyW/IioQbvZVw1mYVCbGq9Rsw4KE06eSMybqHln3w5EeBbLS0MEkApqHY+p68iRpguqa+W7UHKXXQVgPMCpqxMFKonX6VlSQOR64FgpBme2uG+LJ8reTgypEKspQIN0WvtPWmiq4zAwBp08hAacgv868c0MM4WbOYU0rzMIR6Q+ceGVRImlCwZ5b7XKp4mJZ9hlaRjeuyVrDuzBkzROSurX1OXoci08yJvhbtiBJLf3uPOJHrhjKRwIt2TnzS9ElgFZlJiDIA26Athe73n43CT0af2IG6yC7e6sK4L3NEXJrwwUZk=</X509Certificate> </X509Data> </KeyInfo> </KeyDescriptor>` 

Pour plus d’informations sur « Set-MsolDomainAuthentication », consultez : [http://technet.microsoft.com/library/dn194112.aspx](http://technet.microsoft.com/library/dn194112.aspx).

>[!NOTE]
>Vous devez exécutez utiliser « $ecpUrl = « https://WS2012R2-0.contoso.com/PAOS » » uniquement si vous définissez une extension ECP pour votre fournisseur d’identité. Les clients Exchange Online, à l’exception d’Outlook Web Application (OWA), s’appuient sur un point de terminaison actif basé sur POST. Si votre STS SAML 2.0 implémente un point de terminaison actif de l’implémentation ECP d’un tooShibboleth comme point de terminaison actif, il peut être possible pour ces toointeract clients riches avec hello service Exchange Online.

Une fois la fédération a été configurée. vous pouvez basculer trop « non fédéré » (ou « géré »), mais cette modification prend tootwo heures toocomplete et elle nécessite l’attribution de nouveaux mots de passe aléatoires pour le cloud en fonction de connexion tooeach utilisateur. Cette approche trop « géré » peut être nécessaire dans certains scénarios tooreset une erreur dans vos paramètres. Pour plus d’informations sur la conversion de domaine, consultez : [http://msdn.microsoft.com/library/windowsazure/dn194122.aspx](http://msdn.microsoft.com/library/windowsazure/dn194122.aspx).

## <a name="provision-user-principals-tooazure-ad--office-365"></a>Configurer les utilisateurs principaux tooAzure AD / Office 365
Avant de vous authentifier votre tooOffice utilisateurs 365, vous devez configurer Azure AD avec l’utilisateur de revendication principaux qui correspondent assertion toohello Bonjour SAML 2.0. Si ces principaux d’utilisateur n’est pas connus tooAzure AD à l’avance qu’ils ne peut pas être utilisés pour la connexion fédérée. Azure AD Connect ou Windows PowerShell peut être utilisé tooprovision principaux d’utilisateur.

Azure AD Connect peut être utilisé tooprovision principaux tooyour domaines dans votre annuaire Azure AD hello Active Directory sur site. Pour obtenir plus d’informations, consultez [Intégrer vos répertoires locaux avec Azure Active Directory](active-directory-aadconnect.md).

Windows PowerShell peut également être utilisé tooautomate Ajout de nouveaux utilisateurs tooAzure AD et toosynchronize change de hello des services locaux. toouse hello applets de commande Windows PowerShell vous devez télécharger hello [module Azure Active Directory](https://docs.microsoft.com/powershell/azure/install-adv2?view=azureadps-2.0).

Cette procédure montre comment tooadd un tooAzure unique utilisateur AD.


1. Se connecter tooyour annuaire Azure AD en tant qu’un administrateur client : MsolService se connecter.
2.  Créer un nouveau principal d’utilisateur : ` New-MsolUser
        -UserPrincipalName elwoodf1@contoso.com
        -ImmutableId ABCDEFG1234567890
        -DisplayName "Elwood Folk"
        -FirstName Elwood 
        -LastName Folk 
        -AlternateEmailAddresses "Elwood.Folk@contoso.com" 
        -LicenseAssignment "samlp2test:ENTERPRISEPACK" 
        -UsageLocation "US" ` 

Pour plus d’informations sur la vérification de « New-MsolUser », [http://technet.microsoft.com/library/dn194096.aspx](http://technet.microsoft.com/library/dn194096.aspx)

>[!NOTE]
>Hello « UserPrinciplName » valeur doit correspondre à valeur hello à envoyer dans votre revendication SAML 2.0 et le hello « ImmutableID » valeur doit correspondre à valeur de hello envoyée dans votre assertion « NameID » pour « IDPEmail ».

## <a name="verify-single-sign-on-with-your-saml-20-idp"></a>Vérifiez l’authentification unique avec votre fournisseur d’identité SAML 2.0
En tant qu’administrateur de hello, avant de vérifier et gérer l’authentification unique (également appelée fédération des identités), passez en revue les informations hello et effectuez des opérations de hello Bonjour suivant tooset articles configuré l’authentification unique avec votre fournisseur d’identité SP-Lite SAML 2.0 :


1.  Vous avez consulté hello exigences du protocole SAML 2.0 Azure AD
2.  Vous avez configuré votre fournisseur d’identité SAML 2.0
3.  Installez Windows PowerShell pour l’authentification unique avec le fournisseur d’identité SAML 2.0
4.  Configurez une approbation entre votre fournisseur d’identité SAML 2.0 et Azure AD
5.  Configurer un utilisateur de test connus principal tooAzure Active Directory (Office 365) par le biais de Windows PowerShell ou Azure AD Connect.
6.  Configurez la synchronisation de répertoires à l’aide de [Azure AD Connect](active-directory-aadconnect.md).

Après avoir configuré l’authentification unique avec votre fournisseur d’identité basé sur SP-Lite SAML 2.0, vous devez vérifier qu’elle fonctionne correctement.

>[!NOTE]
>Si vous avez converti un domaine, au lieu d’ajouter un, il peut falloir tooset d’heures too24 configuré l’authentification unique.
Avant de vérifier l’authentification unique, vous devez terminer la configuration de la synchronisation Active Directory, synchroniser vos répertoires et activer vos utilisateurs synchronisés.

### <a name="use-hello-tool-tooverify-that-single-sign-on-has-been-set-up-correctly"></a>Utilisez hello outil tooverify que l’authentification unique a été configuré correctement
tooverify que l’authentification unique a été correctement configuré, vous pouvez effectuer les hello suivant tooconfirm procédure que vous êtes en mesure de toosign dans le service cloud toohello avec vos informations d’identification d’entreprise.

Microsoft fournit un outil que vous pouvez utiliser tootest votre SAML 2.0 en fonction de fournisseur d’identité. Avant d’exécuter hello tester l’outil, vous devez configurer un toofederate de locataire Azure AD avec votre fournisseur d’identité.

>[!NOTE]
>Hello Analyseur de connectivité requiert Internet Explorer 10 ou version ultérieure.



1. Téléchargement hello Analyseur de connectivité à [https://testconnectivity.microsoft.com/?tabid=Client](https://testconnectivity.microsoft.com/?tabid=Client).
2.  Cliquez sur Installer maintenant toobegin téléchargement et installation de l’outil de hello.
3.  Sélectionnez « Je ne peux pas configurer la fédération avec Office 365, Azure ou d’autres services qui utilisent Azure Active Directory ».
4.  Une fois que l’outil de hello est téléchargé et en cours d’exécution, vous verrez la fenêtre de Diagnostics de connectivité hello. outil de Hello pas, vous allez tester votre connexion de fédération.
5.  Hello Analyseur de connectivité s’ouvre de votre fournisseur d’identité SAML 2.0 pour vous toologon, entrez des informations d’identification de hello pour UPN hello vous testez : ![SAML](media/active-directory-aadconnect-federation-saml-idp/saml1.png)
6.  À hello fédération tester dans la fenêtre connexion que vous devez entrer un nom de compte et un mot de passe pour le locataire Azure AD hello qui est configuré toobe fédéré avec votre fournisseur d’identité SAML 2.0. outil de Hello tentera de toosign à l’aide de ces informations d’identification et les résultats détaillés des tests effectués au cours de la tentative de connexion hello seront fournies en tant que sortie.
![SAML](media/active-directory-aadconnect-federation-saml-idp/saml2.png)
7. Cette fenêtre affiche un résultat d’échec du test. Cliquez sur examiner les résultats détaillés afficher des informations sur les résultats de hello pour chaque test qui a été effectuée. Vous pouvez également enregistrer hello résultats toodisk dans l’ordre tooshare les.
 
>[!NOTE]
>Hello Analyseur de connectivité teste également fédération Active à l’aide de hello WS *-protocoles en fonction ECP/paos. Si vous les utilisez pas, vous pouvez ignorer hello l’erreur suivante : test hello flux de connexion Active à l’aide du point de terminaison de fédération Active de votre fournisseur d’identité.

### <a name="manually-verify-that-single-sign-on-has-been-set-up-correctly"></a>Vérifiez manuellement que l’authentification unique a été correctement configurée
La vérification manuelle comprend des étapes supplémentaires que vous pouvez prendre tooensure votre fournisseur d’identité SAML 2.0 fonctionne correctement dans de nombreux scénarios.
tooverify que l’authentification unique a été configuré correctement, suivez hello suivantes comme suit :


1. Sur un ordinateur joint au domaine, connectez-vous tooyour service de cloud à l’aide de hello même nom que vous utilisez pour vos informations d’identification d’entreprise de la connexion.
2.  Cliquez dans la zone de mot de passe hello. Si l’authentification unique est configurée, zone de mot de passe hello sera grisé et vous verrez hello message suivant : « vous êtes maintenant toosign requis dans à <your company>. »
3.  Cliquez sur hello vous connecter à <your company> lien. Si vous êtes en mesure de toosign dans, puis l’authentification unique a été configurée.

## <a name="next-steps"></a>Étapes suivantes


- [Gestion des services AD FS (Active Directory Federation Services) et personnalisation avec Azure AD Connect](active-directory-aadconnect-federation-management.md)
- [Liste de compatibilité de fédération Azure AD](active-directory-aadconnect-federation-compatibility.md)
- [Installation personnalisée d’Azure AD Connect](active-directory-aadconnect-get-started-custom.md)
