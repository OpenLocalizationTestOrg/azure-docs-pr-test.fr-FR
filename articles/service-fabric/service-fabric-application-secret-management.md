---
title: les secrets aaaManaging dans les applications de Service Fabric | Documents Microsoft
description: "Cet article décrit comment les valeurs dans une application de Service Fabric toosecure secret."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 94a67e45-7094-4fbd-9c88-51f4fc3c523a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: b8cafcb681d95aaa1b8e9a1afaac78ba5b7f58b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a>Gestion des secrets dans des applications Service Fabric
Ce guide vous guide tout au long des étapes de hello de la gestion des clés secrètes dans une application de Service Fabric. Les secrets peuvent être des informations sensibles quelconques, notamment des chaînes de connexion de stockage, des mots de passe ou d’autres valeurs qui ne doivent pas être traitées en texte brut.

Ce guide utilise les clés secrètes et des clés de toomanage de coffre de clés Azure. Toutefois, *à l’aide de* les clés secrètes dans une application est le cluster déployé tooa toobe cloud indépendant de la plateforme tooallow applications hébergées en tout lieu. 

## <a name="overview"></a>Vue d'ensemble
Hello paramètres de configuration de service toomanage recommandée s’effectue via [packages de configuration de service][config-package]. Les versions des packages de configuration sont gérées et peuvent être mises à jour par le biais de mises à niveau propagées gérées avec validation de l’intégrité et la restauration automatique. Il s’agit de configuration de tooglobal préférée car cela réduit les risques de hello d’une panne de service global. Les secrets chiffrés ne font pas exception. Service Fabric dispose de fonctionnalités intégrées pour chiffrer et déchiffrer des valeurs dans un fichier de package de configuration Settings.xml à l’aide du cryptage de certificat.

Hello diagramme suivant illustre les flux de base hello pour la gestion de secret principal dans une application de Service Fabric :

![vue d’ensemble de la gestion des secrets][overview]

Ce flux comprend quatre étapes principales :

1. Obtenez un certificat de chiffrement de données.
2. Installer le certificat de hello dans votre cluster.
3. Chiffrer les valeurs des secrets lors du déploiement d’une application avec un certificat de hello et les injecter dans le fichier de configuration d’un service Settings.xml.
4. Valeurs en lecture chiffré hors Settings.xml en déchiffrant avec hello même certificat de chiffrement. 

[Azure Key Vault] [ key-vault-get-started] est utilisé ici comme un emplacement de stockage sécurisé pour les certificats et comme un moyen tooget certificats installés sur des clusters Service Fabric dans Azure. Si vous ne déployez pas tooAzure, il est inutile secrets de toomanage toouse le coffre de clés dans les applications de Service Fabric.

## <a name="data-encipherment-certificate"></a>Certificat de chiffrement de données
Un certificat de chiffrement de données est utilisé exclusivement pour le chiffrement et déchiffrement des valeurs de configuration dans le fichier Settings.xml d’un service et n’est pas utilisé à des fins d’authentification ou de signature du texte chiffré. certificat de Hello doit respecter hello suivant les exigences :

* certificat de Hello doit contenir une clé privée.
* certificat de Hello doit être créé pour l’échange de clés, exportable tooa fichier d’échange d’informations personnelles (.pfx).
* utilisation de clé de certificat Hello doit inclure le chiffrement de données (10) et ne doit pas inclure l’authentification du serveur ou l’authentification du Client. 
  
  Par exemple, lorsque vous créez un certificat auto-signé à l’aide de PowerShell, hello `KeyUsage` indicateur doit être défini trop`DataEncipherment`:
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a>Installer le certificat de hello dans votre cluster
Ce certificat doit être installé sur chaque nœud de cluster de hello. Il sera utilisé au runtime toodecrypt les valeurs stockées dans un service Settings.xml. Consultez [comment toocreate un cluster à l’aide du Gestionnaire de ressources Azure] [ service-fabric-cluster-creation-via-arm] pour obtenir des instructions d’installation. 

## <a name="encrypt-application-secrets"></a>Chiffrement de secrets d’application
Hello SDK de l’infrastructure de Service dispose de fonctions intégrées de chiffrement et déchiffrement de secret principal. Les valeurs de clé secrète peuvent être chiffrées au moment de leur génération, puis déchiffrés et lues par programme dans un code de service. 

Hello suivant de commande PowerShell est tooencrypt utilisé une clé secrète. Cette commande chiffre uniquement la valeur de hello ; Il effectue **pas** signer du texte de chiffrement hello. Vous devez utiliser hello même certificat de chiffrement qui est installé dans votre texte chiffré tooproduce de cluster pour les valeurs de clé secrètes :

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

Hello chaîne en base 64 qui en résulte contient à la fois texte chiffré de secret principal hello ainsi que des informations sur le certificat hello qui a été utilisé tooencrypt il.  Hello chaîne codée en base 64 peut être insérée dans un paramètre dans le fichier de configuration de votre service Settings.xml avec hello `IsEncrypted` attribut défini trop`true`:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a>Injection de secrets d’application dans des instances d’application
Dans l’idéal, les environnements de déploiement toodifferent doivent être possible d’automatiser. Cela peut être accompli en effectuer un chiffrement de clé secrète dans un environnement de génération et en fournissant des secrets de hello chiffré en tant que paramètres lors de la création d’instances de l’application.

#### <a name="use-overridable-parameters-in-settingsxml"></a>Utilisation de paramètres substituables dans Settings.xml
fichier de configuration Hello Settings.xml permet les paramètres substituables qui peuvent être fournies au moment de la création d’application. Hello d’utilisation `MustOverride` attribut au lieu de fournir une valeur pour un paramètre :

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

valeurs toooverride dans Settings.xml, déclarez un paramètre de remplacement pour le service hello dans ApplicationManifest.xml :

```xml
<ApplicationManifest ... >
  <Parameters>
    <Parameter Name="MySecret" DefaultValue="" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides>
      <ConfigOverride Name="Config">
        <Settings>
          <Section Name="MySettings">
            <Parameter Name="MySecret" Value="[MySecret]" IsEncrypted="true" />
          </Section>
        </Settings>
      </ConfigOverride>
    </ConfigOverrides>
  </ServiceManifestImport>
 ```

Maintenant la valeur de hello peut être spécifiée comme un *paramètre application* lors de la création d’une instance de l’application hello. La création d’une instance d’application peut être scriptée à l’aide de PowerShell ou écrite en C# pour faciliter l’intégration dans un processus de génération.

À l’aide de PowerShell, le paramètre hello est fourni toohello `New-ServiceFabricApplication` commande comme un [table de hachage](https://technet.microsoft.com/library/ee692803.aspx):

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

Avec C#, les paramètres de l’application sont spécifiés dans un `ApplicationDescription` en tant que `NameValueCollection` :

```csharp
FabricClient fabricClient = new FabricClient();

NameValueCollection applicationParameters = new NameValueCollection();
applicationParameters["MySecret"] = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=";

ApplicationDescription applicationDescription = new ApplicationDescription(
    applicationName: new Uri("fabric:/MyApp"),
    applicationTypeName: "MyAppType",
    applicationTypeVersion: "1.0.0",
    applicationParameters: applicationParameters)
);

await fabricClient.ApplicationManager.CreateApplicationAsync(applicationDescription);
```

## <a name="decrypt-secrets-from-service-code"></a>Déchiffrement de secrets à partir du code de service
Services dans l’infrastructure de Service s’exécutent sous le SERVICE réseau par défaut sur Windows et n’avez pas accès toocertificates installées sur le nœud hello sans une configuration complémentaire.

Lorsque vous utilisez un certificat de chiffrement de données, vous devez toomake que SERVICE réseau ou n’importe quel service hello du compte utilisateur est en cours d’exécution sous possède la clé privée du certificat d’accès toohello. Service Fabric gérera octroyer l’accès à votre service automatiquement si vous configurez toodo donc. Cette configuration est possible dans ApplicationManifest.xml en définissant des utilisateurs et des stratégies de sécurité pour les certificats. Dans l’exemple suivant de hello, certificat de tooa d’accès en lecture défini par son empreinte numérique est fourni à hello compte SERVICE réseau :

```xml
<ApplicationManifest … >
    <Principals>
        <Users>
            <User Name="Service1" AccountType="NetworkService" />
        </Users>
    </Principals>
  <Policies>
    <SecurityAccessPolicies>
      <SecurityAccessPolicy GrantRights=”Read” PrincipalRef="Service1" ResourceRef="MyCert" ResourceType="Certificate"/>
    </SecurityAccessPolicies>
  </Policies>
  <Certificates>
    <SecretsCertificate Name="MyCert" X509FindType="FindByThumbprint" X509FindValue="[YourCertThumbrint]"/>
  </Certificates>
</ApplicationManifest>
```

> [!NOTE]
> Lors de la copie d’une empreinte numérique du certificat de hello stocker les composants logiciels enfichables sur Windows, un caractère invisible est placé au début de hello de chaîne d’empreinte numérique hello. Ce caractère invisible peut provoquer une erreur lors de la tentative de toolocate un certificat par l’empreinte numérique, par conséquent, être toodelete que ce caractère supplémentaire.
> 
> 

### <a name="use-application-secrets-in-service-code"></a>Utilisation de secrets d’application dans le code de service
permet de Hello API pour accéder aux valeurs de configuration à partir de Settings.xml dans un package de configuration pour le déchiffrement facile de valeurs qui ont hello `IsEncrypted` attribut défini trop`true`. Étant donné que le texte hello chiffrée contienne des informations sur le certificat hello utilisé pour le chiffrement, il est inutile certificat de hello toomanually rechercher. certificat de Hello doit simplement toobe installé sur le nœud de hello hello service s’exécute sur. Appelez simplement hello `DecryptValue()` tooretrieve hello d’origine secrète valeur de la méthode :

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur [l’exécution d’applications avec des autorisations de sécurité différentes](service-fabric-application-runas-security.md)

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
