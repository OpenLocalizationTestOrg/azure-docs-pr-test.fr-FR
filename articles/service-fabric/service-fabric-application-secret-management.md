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
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="5d30d-103">Gestion des secrets dans des applications Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5d30d-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="5d30d-104">Ce guide vous guide tout au long des étapes de hello de la gestion des clés secrètes dans une application de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5d30d-104">This guide walks you through hello steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="5d30d-105">Les secrets peuvent être des informations sensibles quelconques, notamment des chaînes de connexion de stockage, des mots de passe ou d’autres valeurs qui ne doivent pas être traitées en texte brut.</span><span class="sxs-lookup"><span data-stu-id="5d30d-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="5d30d-106">Ce guide utilise les clés secrètes et des clés de toomanage de coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="5d30d-106">This guide uses Azure Key Vault toomanage keys and secrets.</span></span> <span data-ttu-id="5d30d-107">Toutefois, *à l’aide de* les clés secrètes dans une application est le cluster déployé tooa toobe cloud indépendant de la plateforme tooallow applications hébergées en tout lieu.</span><span class="sxs-lookup"><span data-stu-id="5d30d-107">However, *using* secrets in an application is cloud platform-agnostic tooallow applications toobe deployed tooa cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="5d30d-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5d30d-108">Overview</span></span>
<span data-ttu-id="5d30d-109">Hello paramètres de configuration de service toomanage recommandée s’effectue via [packages de configuration de service][config-package].</span><span class="sxs-lookup"><span data-stu-id="5d30d-109">hello recommended way toomanage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="5d30d-110">Les versions des packages de configuration sont gérées et peuvent être mises à jour par le biais de mises à niveau propagées gérées avec validation de l’intégrité et la restauration automatique.</span><span class="sxs-lookup"><span data-stu-id="5d30d-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="5d30d-111">Il s’agit de configuration de tooglobal préférée car cela réduit les risques de hello d’une panne de service global.</span><span class="sxs-lookup"><span data-stu-id="5d30d-111">This is preferred tooglobal configuration as it reduces hello chances of a global service outage.</span></span> <span data-ttu-id="5d30d-112">Les secrets chiffrés ne font pas exception.</span><span class="sxs-lookup"><span data-stu-id="5d30d-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="5d30d-113">Service Fabric dispose de fonctionnalités intégrées pour chiffrer et déchiffrer des valeurs dans un fichier de package de configuration Settings.xml à l’aide du cryptage de certificat.</span><span class="sxs-lookup"><span data-stu-id="5d30d-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="5d30d-114">Hello diagramme suivant illustre les flux de base hello pour la gestion de secret principal dans une application de Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="5d30d-114">hello following diagram illustrates hello basic flow for secret management in a Service Fabric application:</span></span>

![vue d’ensemble de la gestion des secrets][overview]

<span data-ttu-id="5d30d-116">Ce flux comprend quatre étapes principales :</span><span class="sxs-lookup"><span data-stu-id="5d30d-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="5d30d-117">Obtenez un certificat de chiffrement de données.</span><span class="sxs-lookup"><span data-stu-id="5d30d-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="5d30d-118">Installer le certificat de hello dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="5d30d-118">Install hello certificate in your cluster.</span></span>
3. <span data-ttu-id="5d30d-119">Chiffrer les valeurs des secrets lors du déploiement d’une application avec un certificat de hello et les injecter dans le fichier de configuration d’un service Settings.xml.</span><span class="sxs-lookup"><span data-stu-id="5d30d-119">Encrypt secret values when deploying an application with hello certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="5d30d-120">Valeurs en lecture chiffré hors Settings.xml en déchiffrant avec hello même certificat de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="5d30d-120">Read encrypted values out of Settings.xml by decrypting with hello same encipherment certificate.</span></span> 

<span data-ttu-id="5d30d-121">[Azure Key Vault] [ key-vault-get-started] est utilisé ici comme un emplacement de stockage sécurisé pour les certificats et comme un moyen tooget certificats installés sur des clusters Service Fabric dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5d30d-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way tooget certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="5d30d-122">Si vous ne déployez pas tooAzure, il est inutile secrets de toomanage toouse le coffre de clés dans les applications de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5d30d-122">If you are not deploying tooAzure, you do not need toouse Key Vault toomanage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="5d30d-123">Certificat de chiffrement de données</span><span class="sxs-lookup"><span data-stu-id="5d30d-123">Data encipherment certificate</span></span>
<span data-ttu-id="5d30d-124">Un certificat de chiffrement de données est utilisé exclusivement pour le chiffrement et déchiffrement des valeurs de configuration dans le fichier Settings.xml d’un service et n’est pas utilisé à des fins d’authentification ou de signature du texte chiffré.</span><span class="sxs-lookup"><span data-stu-id="5d30d-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="5d30d-125">certificat de Hello doit respecter hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="5d30d-125">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="5d30d-126">certificat de Hello doit contenir une clé privée.</span><span class="sxs-lookup"><span data-stu-id="5d30d-126">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="5d30d-127">certificat de Hello doit être créé pour l’échange de clés, exportable tooa fichier d’échange d’informations personnelles (.pfx).</span><span class="sxs-lookup"><span data-stu-id="5d30d-127">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="5d30d-128">utilisation de clé de certificat Hello doit inclure le chiffrement de données (10) et ne doit pas inclure l’authentification du serveur ou l’authentification du Client.</span><span class="sxs-lookup"><span data-stu-id="5d30d-128">hello certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="5d30d-129">Par exemple, lorsque vous créez un certificat auto-signé à l’aide de PowerShell, hello `KeyUsage` indicateur doit être défini trop`DataEncipherment`:</span><span class="sxs-lookup"><span data-stu-id="5d30d-129">For example, when creating a self-signed certificate using PowerShell, hello `KeyUsage` flag must be set too`DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a><span data-ttu-id="5d30d-130">Installer le certificat de hello dans votre cluster</span><span class="sxs-lookup"><span data-stu-id="5d30d-130">Install hello certificate in your cluster</span></span>
<span data-ttu-id="5d30d-131">Ce certificat doit être installé sur chaque nœud de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="5d30d-131">This certificate must be installed on each node in hello cluster.</span></span> <span data-ttu-id="5d30d-132">Il sera utilisé au runtime toodecrypt les valeurs stockées dans un service Settings.xml.</span><span class="sxs-lookup"><span data-stu-id="5d30d-132">It will be used at runtime toodecrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="5d30d-133">Consultez [comment toocreate un cluster à l’aide du Gestionnaire de ressources Azure] [ service-fabric-cluster-creation-via-arm] pour obtenir des instructions d’installation.</span><span class="sxs-lookup"><span data-stu-id="5d30d-133">See [how toocreate a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="5d30d-134">Chiffrement de secrets d’application</span><span class="sxs-lookup"><span data-stu-id="5d30d-134">Encrypt application secrets</span></span>
<span data-ttu-id="5d30d-135">Hello SDK de l’infrastructure de Service dispose de fonctions intégrées de chiffrement et déchiffrement de secret principal.</span><span class="sxs-lookup"><span data-stu-id="5d30d-135">hello Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="5d30d-136">Les valeurs de clé secrète peuvent être chiffrées au moment de leur génération, puis déchiffrés et lues par programme dans un code de service.</span><span class="sxs-lookup"><span data-stu-id="5d30d-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="5d30d-137">Hello suivant de commande PowerShell est tooencrypt utilisé une clé secrète.</span><span class="sxs-lookup"><span data-stu-id="5d30d-137">hello following PowerShell command is used tooencrypt a secret.</span></span> <span data-ttu-id="5d30d-138">Cette commande chiffre uniquement la valeur de hello ; Il effectue **pas** signer du texte de chiffrement hello.</span><span class="sxs-lookup"><span data-stu-id="5d30d-138">This command only encrypts hello value; it does **not** sign hello cipher text.</span></span> <span data-ttu-id="5d30d-139">Vous devez utiliser hello même certificat de chiffrement qui est installé dans votre texte chiffré tooproduce de cluster pour les valeurs de clé secrètes :</span><span class="sxs-lookup"><span data-stu-id="5d30d-139">You must use hello same encipherment certificate that is installed in your cluster tooproduce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="5d30d-140">Hello chaîne en base 64 qui en résulte contient à la fois texte chiffré de secret principal hello ainsi que des informations sur le certificat hello qui a été utilisé tooencrypt il.</span><span class="sxs-lookup"><span data-stu-id="5d30d-140">hello resulting base-64 string contains both hello secret ciphertext as well as information about hello certificate that was used tooencrypt it.</span></span>  <span data-ttu-id="5d30d-141">Hello chaîne codée en base 64 peut être insérée dans un paramètre dans le fichier de configuration de votre service Settings.xml avec hello `IsEncrypted` attribut défini trop`true`:</span><span class="sxs-lookup"><span data-stu-id="5d30d-141">hello base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with hello `IsEncrypted` attribute set too`true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="5d30d-142">Injection de secrets d’application dans des instances d’application</span><span class="sxs-lookup"><span data-stu-id="5d30d-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="5d30d-143">Dans l’idéal, les environnements de déploiement toodifferent doivent être possible d’automatiser.</span><span class="sxs-lookup"><span data-stu-id="5d30d-143">Ideally, deployment toodifferent environments should be as automated as possible.</span></span> <span data-ttu-id="5d30d-144">Cela peut être accompli en effectuer un chiffrement de clé secrète dans un environnement de génération et en fournissant des secrets de hello chiffré en tant que paramètres lors de la création d’instances de l’application.</span><span class="sxs-lookup"><span data-stu-id="5d30d-144">This can be accomplished by performing secret encryption in a build environment and providing hello encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="5d30d-145">Utilisation de paramètres substituables dans Settings.xml</span><span class="sxs-lookup"><span data-stu-id="5d30d-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="5d30d-146">fichier de configuration Hello Settings.xml permet les paramètres substituables qui peuvent être fournies au moment de la création d’application.</span><span class="sxs-lookup"><span data-stu-id="5d30d-146">hello Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="5d30d-147">Hello d’utilisation `MustOverride` attribut au lieu de fournir une valeur pour un paramètre :</span><span class="sxs-lookup"><span data-stu-id="5d30d-147">Use hello `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="5d30d-148">valeurs toooverride dans Settings.xml, déclarez un paramètre de remplacement pour le service hello dans ApplicationManifest.xml :</span><span class="sxs-lookup"><span data-stu-id="5d30d-148">toooverride values in Settings.xml, declare an override parameter for hello service in ApplicationManifest.xml:</span></span>

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

<span data-ttu-id="5d30d-149">Maintenant la valeur de hello peut être spécifiée comme un *paramètre application* lors de la création d’une instance de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5d30d-149">Now hello value can be specified as an *application parameter* when creating an instance of hello application.</span></span> <span data-ttu-id="5d30d-150">La création d’une instance d’application peut être scriptée à l’aide de PowerShell ou écrite en C# pour faciliter l’intégration dans un processus de génération.</span><span class="sxs-lookup"><span data-stu-id="5d30d-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="5d30d-151">À l’aide de PowerShell, le paramètre hello est fourni toohello `New-ServiceFabricApplication` commande comme un [table de hachage](https://technet.microsoft.com/library/ee692803.aspx):</span><span class="sxs-lookup"><span data-stu-id="5d30d-151">Using PowerShell, hello parameter is supplied toohello `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="5d30d-152">Avec C#, les paramètres de l’application sont spécifiés dans un `ApplicationDescription` en tant que `NameValueCollection` :</span><span class="sxs-lookup"><span data-stu-id="5d30d-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

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

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="5d30d-153">Déchiffrement de secrets à partir du code de service</span><span class="sxs-lookup"><span data-stu-id="5d30d-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="5d30d-154">Services dans l’infrastructure de Service s’exécutent sous le SERVICE réseau par défaut sur Windows et n’avez pas accès toocertificates installées sur le nœud hello sans une configuration complémentaire.</span><span class="sxs-lookup"><span data-stu-id="5d30d-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access toocertificates installed on hello node without some extra setup.</span></span>

<span data-ttu-id="5d30d-155">Lorsque vous utilisez un certificat de chiffrement de données, vous devez toomake que SERVICE réseau ou n’importe quel service hello du compte utilisateur est en cours d’exécution sous possède la clé privée du certificat d’accès toohello.</span><span class="sxs-lookup"><span data-stu-id="5d30d-155">When using a data encipherment certificate, you need toomake sure NETWORK SERVICE or whatever user account hello service is running under has access toohello certificate's private key.</span></span> <span data-ttu-id="5d30d-156">Service Fabric gérera octroyer l’accès à votre service automatiquement si vous configurez toodo donc.</span><span class="sxs-lookup"><span data-stu-id="5d30d-156">Service Fabric will handle granting access for your service automatically if you configure it toodo so.</span></span> <span data-ttu-id="5d30d-157">Cette configuration est possible dans ApplicationManifest.xml en définissant des utilisateurs et des stratégies de sécurité pour les certificats.</span><span class="sxs-lookup"><span data-stu-id="5d30d-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="5d30d-158">Dans l’exemple suivant de hello, certificat de tooa d’accès en lecture défini par son empreinte numérique est fourni à hello compte SERVICE réseau :</span><span class="sxs-lookup"><span data-stu-id="5d30d-158">In hello following example, hello NETWORK SERVICE account is given read access tooa certificate defined by its thumbprint:</span></span>

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
> <span data-ttu-id="5d30d-159">Lors de la copie d’une empreinte numérique du certificat de hello stocker les composants logiciels enfichables sur Windows, un caractère invisible est placé au début de hello de chaîne d’empreinte numérique hello.</span><span class="sxs-lookup"><span data-stu-id="5d30d-159">When copying a certificate thumbprint from hello certificate store snap-in on Windows, an invisible character is placed at hello beginning of hello thumbprint string.</span></span> <span data-ttu-id="5d30d-160">Ce caractère invisible peut provoquer une erreur lors de la tentative de toolocate un certificat par l’empreinte numérique, par conséquent, être toodelete que ce caractère supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="5d30d-160">This invisible character can cause an error when trying toolocate a certificate by thumbprint, so be sure toodelete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="5d30d-161">Utilisation de secrets d’application dans le code de service</span><span class="sxs-lookup"><span data-stu-id="5d30d-161">Use application secrets in service code</span></span>
<span data-ttu-id="5d30d-162">permet de Hello API pour accéder aux valeurs de configuration à partir de Settings.xml dans un package de configuration pour le déchiffrement facile de valeurs qui ont hello `IsEncrypted` attribut défini trop`true`.</span><span class="sxs-lookup"><span data-stu-id="5d30d-162">hello API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have hello `IsEncrypted` attribute set too`true`.</span></span> <span data-ttu-id="5d30d-163">Étant donné que le texte hello chiffrée contienne des informations sur le certificat hello utilisé pour le chiffrement, il est inutile certificat de hello toomanually rechercher.</span><span class="sxs-lookup"><span data-stu-id="5d30d-163">Since hello encrypted text contains information about hello certificate used for encryption, you do not need toomanually find hello certificate.</span></span> <span data-ttu-id="5d30d-164">certificat de Hello doit simplement toobe installé sur le nœud de hello hello service s’exécute sur.</span><span class="sxs-lookup"><span data-stu-id="5d30d-164">hello certificate just needs toobe installed on hello node that hello service is running on.</span></span> <span data-ttu-id="5d30d-165">Appelez simplement hello `DecryptValue()` tooretrieve hello d’origine secrète valeur de la méthode :</span><span class="sxs-lookup"><span data-stu-id="5d30d-165">Simply call hello `DecryptValue()` method tooretrieve hello original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="5d30d-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5d30d-166">Next Steps</span></span>
<span data-ttu-id="5d30d-167">En savoir plus sur [l’exécution d’applications avec des autorisations de sécurité différentes](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="5d30d-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
