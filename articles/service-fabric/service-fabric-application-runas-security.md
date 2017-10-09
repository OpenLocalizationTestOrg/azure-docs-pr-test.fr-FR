---
title: "aaaLearn sur les stratégies de sécurité Azure microservices | Documents Microsoft"
description: "Vue d’ensemble de comment toorun une application de Service Fabric sous système et des comptes de sécurité locaux, notamment le point de SetupEntry hello lorsqu’une application doit tooperform certaines privilégié action avant de commencer"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: mfussell
ms.openlocfilehash: f5afba69e09aa4f3c9efa4d3efc6995c813a1f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-security-policies-for-your-application"></a>Configurer les stratégies de sécurité de votre application
À l’aide de l’infrastructure de Service Azure, vous pouvez sécuriser les applications qui s’exécutent dans le cluster hello sous différents comptes d’utilisateurs. Service Fabric permet également de certificats, les fichiers, les répertoires et les ressources hello sécurisée qui sont utilisés par les applications au moment de hello du déploiement sous des comptes d’utilisateur hello--par exemple. Ainsi, les applications en cours d’exécution sont plus sécurisées, même dans un environnement hébergé partagé.

Par défaut, les applications de Service Fabric s’exécutent sous le compte de hello hello Fabric.exe processus s’exécute sous. Service Fabric permet aussi hello toorun des applications sous un compte d’utilisateur local ou le compte système local, qui est spécifié dans le manifeste de l’application hello. Les types de comptes système locaux pris en charge sont **LocalUser**, **NetworkService**, **LocalService** et **LocalSystem**.

 Lorsque vous exécutez l’infrastructure de Service sur Windows Server dans votre centre de données à l’aide du programme d’installation autonome de hello, vous pouvez utiliser des comptes de domaine Active Directory, y compris les comptes de service administrés de groupe.

Vous pouvez définir et créer des groupes d’utilisateurs afin qu’un ou plusieurs utilisateurs peuvent être ajoutés tooeach toobe de groupe géré ensemble. Cela est utile quand il existe plusieurs utilisateurs pour les points d’entrée de service différent et doivent toohave certains privilèges courants qui sont disponibles au niveau du groupe hello.

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a>Configurer une stratégie de hello pour un point d’entrée de service d’installation
Comme décrit dans hello [modèle d’application](service-fabric-application-model.md), hello point d’entrée, le programme d’installation, **SetupEntryPoint**, est un point d’entrée privilégiés qui s’exécute avec hello même les informations d’identification en tant que Service Fabric (généralement hello *NetworkService* compte) avant de n’importe quel autre point d’entrée. fichier exécutable Hello spécifié par **EntryPoint** est habituellement hello longue service hôte. Donc avoir une entrée d’installation distinct point évite hôte de service toorun hello exécutable avec des privilèges élevés pour de longues périodes. Hello exécutable qui **EntryPoint** Spécifie s’exécute après **SetupEntryPoint** se termine avec succès. Hello processus résultant est surveillé et redémarré et recommence avec **SetupEntryPoint** si elle se termine ou se bloque de jamais.

Hello Voici un exemple de manifeste de service simple qu’affiche hello SetupEntryPoint et hello point d’entrée principal pour le service de hello.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>
  <ConfigPackage Name="Config" Version="1.0.0" />
</ServiceManifest>
```

### <a name="configure-hello-policy-by-using-a-local-account"></a>Configurer la stratégie de hello en utilisant un compte local
Après avoir configuré le service de hello toohave un point d’entrée le programme d’installation, vous pouvez modifier les autorisations de sécurité hello il s’exécute sous dans le manifeste de l’application hello. Bonjour à l’exemple suivant montre comment tooconfigure hello toorun service sous des privilèges de compte d’utilisateur administrateur.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupAdminUser" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupAdminUser">
            <MemberOf>
               <SystemGroup Name="Administrators" />
            </MemberOf>
         </User>
      </Users>
   </Principals>
</ApplicationManifest>
```

Tout d’abord, créez une section **Principals** avec un nom d’utilisateur, par exemple SetupAdminUser. Cela indique que l’utilisateur hello est un membre du groupe de hello administrateurs système.

Ensuite, sous hello **ServiceManifestImport** section, configurer, une stratégie tooapply ce principal trop**SetupEntryPoint**. Cela indique à l’infrastructure de Service qui lorsque hello **MySetup.bat** fichier est exécuté, il doit être `RunAs` avec des privilèges d’administrateur. Étant donné que vous avez *pas* appliqué un point d’entrée principal toohello stratégie, le code hello dans **MyServiceHost.exe** s’exécute sous un système de hello **NetworkService** compte. Il s’agit de compte par défaut hello exécutés en tant que tous les points d’entrée de service.

Vous allez maintenant ajouter hello fichier MySetup.bat toohello Visual Studio projet tootest hello des privilèges d’administrateur. Dans Visual Studio, cliquez sur le projet de service hello et ajoutez un nouveau fichier appelé MySetup.bat.

Vérifiez ensuite que ce fichier de MySetup.bat hello est inclus dans le package de service hello. Par défaut, il ne l’est pas. Sélectionnez le fichier de hello, tooget hello contexte menu contextuel et choisissez **propriétés**. Dans la boîte de dialogue de propriétés hello, vérifiez que **copier tooOutput active** est défini trop**Copier si plus récent**. Consultez hello suivant capture d’écran.

![Visual Studio CopyToOutput pour fichier batch SetupEntryPoint][image1]

Maintenant ouvrir le fichier de MySetup.bat hello et ajouter hello suivant de commandes :

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

Ensuite, générer et déployer le cluster de développement local tooa hello solution. Après hello a démarrage du service, comme indiqué dans l’Explorateur de l’infrastructure de Service, vous pouvez voir le que fichier MySetup.bat hello réussie de deux manières. Ouvrez une invite de commandes PowerShell et entrez :

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

Ensuite, notez hello nom du nœud hello où le service de hello a été déployé et lancé dans le Service Fabric Explorer--par exemple, nœud 2. Ensuite, accédez toohello application instance travail toofind hello out.txt fichiers du dossier qui affiche la valeur hello **TestVariable**. Par exemple, si ce service a été déployé tooNode 2, vous pouvez passer toothis chemin hello **MyApplicationType**:

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a>Configurer la stratégie de hello en utilisant des comptes système local
Souvent, c’est le script de démarrage hello toorun préférable à l’aide d’un compte système local plutôt que d’un compte d’administrateur. Exécution de la stratégie de RunAs hello en tant que membre du groupe Administrateurs généralement ne fonctionne pas correctement, car les ordinateurs ont accès contrôle utilisateur (UAC) activé par défaut de hello. Dans ce cas, **recommandation de hello est toorun hello SetupEntryPoint en tant que LocalSystem, au lieu d’en tant qu’un groupe d’utilisateurs local ajouté tooAdministrators**. Hello suivant montre paramètre hello SetupEntryPoint toorun en tant que LocalSystem :

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupLocalSystem" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupLocalSystem" AccountType="LocalSystem" />
      </Users>
   </Principals>
</ApplicationManifest>
```

## <a name="start-powershell-commands-from-a-setup-entry-point"></a>Lancer des commandes PowerShell à partir d’un point d’entrée de configuration
toorun PowerShell à partir de hello **SetupEntryPoint** point, vous pouvez exécuter **PowerShell.exe** dans un fichier de commandes qui pointe tooa PowerShell de fichiers. Tout d’abord, ajoutez un projet de service PowerShell fichier toohello--par exemple, **MySetup.ps1**. N’oubliez pas de tooset hello *Copier si plus récent* propriété pour ce fichier hello est également inclus dans le package de service hello. Hello suivant montre un exemple de fichier de traitement par lots qui démarre un fichier PowerShell appelé MySetup.ps1, qui définit une variable d’environnement système appelée **TestVariable**.

MySetup.bat toostart un fichier de PowerShell :

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

Dans le fichier de PowerShell hello, ajoutez hello suivant tooset une variable d’environnement système :

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> Par défaut, lorsque le fichier de commandes hello s’exécute, il examine appelé dossier de l’application hello **fonctionne** pour les fichiers. Dans ce cas, MySetup.bat s’exécute, nous souhaitons cette hello toofind MySetup.ps1 fichier Bonjour même dossier, qui est l’application hello **package de code** dossier. toochange ce dossier, le dossier de travail ensemble hello :
> 
> 

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    </ExeHost>
</SetupEntryPoint>
```

## <a name="use-console-redirection-for-local-debugging"></a>Utiliser la console de redirection pour le débogage local
Il est parfois utile toosee sortie de console hello à partir d’un script pour le débogage en cours d’exécution. toodo, vous pouvez définir une stratégie de redirection de console, qui écrit le fichier de sortie de tooa hello. Hello fichier de sortie est appelée de dossier de l’application écrit toohello **journal** sur le nœud hello où l’application hello est déployée et exécutée. (Consultez la rubrique toofind cela Bonjour précédent exemple.)

> [!WARNING]
> N’utilisez jamais de stratégie de redirection de console hello dans une application est déployée en production, car cela peut affecter le basculement d’application hello. N’utilisez cette stratégie *que* pour le développement local et à des fins de débogage.  
> 
> 

Hello exemple suivant illustre la redirection de la console hello de paramètre avec la valeur FileRetentionCount :

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

Si vous modifiez maintenant hello MySetup.ps1 fichier toowrite une **Echo** commande, il écrit le fichier de sortie toohello à des fins de débogage :

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

**Une fois que vous avez débogué votre script, supprimez immédiatement cette stratégie de redirection de console**.

## <a name="configure-a-policy-for-service-code-packages"></a>Configurer une stratégie pour les packages de code de service
Bonjour étapes précédentes, vous avez vu comment tooapply un tooSetupEntryPoint de stratégie d’identification. Examinons un peu plus loin comment toocreate principaux différents qui peut être appliquées en tant que stratégies de service.

### <a name="create-local-user-groups"></a>Création de groupes d'utilisateurs locaux
Vous pouvez définir et créer des groupes d’utilisateurs qui permet d’utiliser un ou plusieurs utilisateurs toobe tooa ajouté. Cela est utile s’il existe plusieurs utilisateurs pour les points d’entrée de service différent et ils doivent toohave certains privilèges courants qui sont disponibles au niveau du groupe hello. Hello suivant montre un groupe local appelé **LocalAdminGroup** disposant des privilèges d’administrateur. Deux utilisateurs, Customer1 et Customer2, deviennent membres de ce groupe local.

```xml
<Principals>
 <Groups>
   <Group Name="LocalAdminGroup">
     <Membership>
       <SystemGroup Name="Administrators"/>
     </Membership>
   </Group>
 </Groups>
  <Users>
     <User Name="Customer1">
        <MemberOf>
           <Group NameRef="LocalAdminGroup" />
        </MemberOf>
     </User>
    <User Name="Customer2">
      <MemberOf>
        <Group NameRef="LocalAdminGroup" />
      </MemberOf>
    </User>
  </Users>
</Principals>
```

### <a name="create-local-users"></a>Création d'utilisateurs locaux
Vous pouvez créer un utilisateur local qui peut être utilisé toohelp sécurisée un service au sein de l’application hello. Lorsqu’un **UtilisateurLocal** type de compte est spécifié dans la section de principaux de hello de manifeste de l’application hello, Service Fabric crée des comptes d’utilisateurs locaux sur les ordinateurs où l’application hello est déployée. Par défaut, ces comptes n’ont pas de hello mêmes noms que ceux spécifiés dans l’application hello manifeste (par exemple, Customer3 Bonjour suivant l’exemple). Ils sont générés dynamiquement et sont associés à des mots de passe aléatoires.

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

Si une application nécessite que le mot de passe et le compte d’utilisateur hello être même sur tous les ordinateurs (par exemple, l’authentification NTLM tooenable), le manifeste du cluster hello doit définir NTLMAuthenticationEnabled tootrue. Hello manifeste du cluster doit également spécifier un NTLMAuthenticationPasswordSecret utilisé toogenerate hello même mot de passe sur tous les ordinateurs.

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a>Affecter des stratégies toohello packages de code de service
Hello **RunAsPolicy** section pour un **ServiceManifestImport** Spécifie le compte hello à partir de la section principaux hello qui doit être toorun utilisé un package de code. Il associe également code packages à partir du service de hello manifeste avec des comptes d’utilisateur dans la section des principaux hello. Vous pouvez le spécifier pour le programme d’installation hello ou des points d’entrée principal, ou vous pouvez spécifier `All` tooapply il tooboth. Hello suivant montre différentes stratégies appliquées :

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

Si **EntryPointType** n’est pas spécifié, a la valeur par défaut de hello tooEntryPointType = « Main ». Spécification de **SetupEntryPoint** s’avère particulièrement utile lorsque vous souhaitez toorun certaines opérations à privilèges élevés le programme d’installation sous un compte système. code de service réel Hello peut exécuter sous un compte de plus faible privilège.

### <a name="apply-a-default-policy-tooall-service-code-packages"></a>Appliquer un packages de code de service par défaut stratégie tooall
Vous utilisez hello **DefaultRunAsPolicy** section toospecify un compte d’utilisateur par défaut pour tous les packages de code qui n’ont pas un spécifique **RunAsPolicy** défini. Si la plupart des packages de code hello qui sont spécifiés dans le manifeste du service utilisé par une application hello devez toorun sous hello même utilisateur, hello application peut définir simplement une stratégie de d’identification par défaut avec ce compte d’utilisateur. Hello exemple suivant spécifie que si un package de code n’a pas un **RunAsPolicy** spécifié, le package de code hello doit s’exécuter sous hello **MyDefaultAccount** spécifié dans la section des principaux hello.

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a>Utiliser un utilisateur ou groupe de domaine Active Directory
Pour une instance de l’infrastructure de Service qui a été installé sur Windows Server à l’aide du programme d’installation autonome de hello, vous pouvez exécuter le service hello sous les informations d’identification hello pour un compte d’utilisateur ou un groupe Active Directory. Il s’agit d’Active Directory en local au sein de votre domaine et non avec Azure Active Directory (Azure AD). À l’aide un utilisateur de domaine ou un groupe, vous pouvez ensuite accéder autres ressources dans le domaine hello (par exemple, les partages de fichiers) qui dispose d’autorisations.

Hello suivant montre un utilisateur Active Directory appelé *TestUser* avec leur domaine mot de passe chiffré à l’aide d’un certificat appelé *MonCert*. Vous pouvez utiliser hello `Invoke-ServiceFabricEncryptText` texte de chiffrement secrètes PowerShell commande toocreate hello. Consultez [Gestion des secrets dans des applications Service Fabric](service-fabric-application-secret-management.md) pour en savoir plus.

Vous devez déployer la clé privée hello hello certificat toodecrypt hello mot de passe toohello ordinateur local à l’aide d’une méthode hors-bande (dans Azure, il s’agit de via Azure Resource Manager). Ensuite, lorsque le Service Fabric déploie le package toohello ordinateur hello service, il est en mesure de toodecrypt hello secret et (ainsi que le nom d’utilisateur hello) auprès de toorun d’Active Directory avec les informations d’identification.

```xml
<Principals>
  <Users>
    <User Name="TestUser" AccountType="DomainUser" AccountName="Domain\User" Password="[Put encrypted password here using MyCert certificate]" PasswordEncrypted="true" />
  </Users>
</Principals>
<Policies>
  <DefaultRunAsPolicy UserRef="TestUser" />
  <SecurityAccessPolicies>
    <SecurityAccessPolicy ResourceRef="MyCert" PrincipalRef="TestUser" GrantRights="Full" ResourceType="Certificate" />
  </SecurityAccessPolicies>
</Policies>
<Certificates>
```
### <a name="use-a-group-managed-service-account"></a>Utilisez un compte de service géré de groupe.
Pour une instance de l’infrastructure de Service qui a été installé sur Windows Server à l’aide du programme d’installation autonome de hello, vous pouvez exécuter le service de hello en tant que groupe (gMSA) du compte de Service administré. Remarque : il s’agit d’Active Directory en local au sein de votre domaine et non avec Azure Active Directory (Azure AD). À l’aide d’un compte gMSA il n’existe aucun mot de passe ou le mot de passe chiffré stocké dans hello `Application Manifest`.

Hello exemple suivant montre comment toocreate un compte de service administré de groupe appelée *Test-svc$*; la méthode de gestion de toodeploy que nœuds de cluster de toohello de compte de service, et comment tooconfigure hello principal de l’utilisateur.

##### <a name="prerequisites"></a>Composants requis.
- domaine de Hello a besoin d’une clé racine KDS.
- domaine de Hello doit toobe au plus tard le niveau fonctionnel de Windows Server 2012 ou.

##### <a name="example"></a>Exemple
1. Avoir un administrateur de domaine active directory de créer un compte de service administrés de groupe à l’aide de hello `New-ADServiceAccount` applet de commande et assurez-vous que hello `PrincipalsAllowedToRetrieveManagedPassword` inclut tous les nœuds de cluster de l’infrastructure de service hello. Notez que `AccountName`, `DnsHostName` et `ServicePrincipalName` doivent être uniques.
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. Sur chaque nœud de cluster hello service fabric (par exemple, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), installer et de test de service administré de groupe hello.
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. Configurez l’UPN hello et configurer hello RunAsPolicy tooreference hello utilisateur.
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="DomaingMSA"/>
      </Policies>
   </ServiceManifestImport>
  <Principals>
    <Users>
      <User Name="DomaingMSA" AccountType="ManagedServiceAccount" AccountName="domain\svc-Test$"/>
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a>Affectation d’une stratégie d’accès de sécurité pour des points de terminaison HTTP et HTTPS
Si vous appliquez un service tooa de stratégie d’identification et le manifeste de service hello déclare des ressources de point de terminaison avec le protocole de hello HTTP, vous devez spécifier un **SecurityAccessPolicy** tooensure que les ports affectés les points de terminaison toothese sont correctement contrôle d’accès répertoriés pour hello compte d’utilisateur RunAs hello service s’exécute sous. Dans le cas contraire, **http.sys** ne dispose pas d’accès toohello service, et vous obtenez des échecs lors des appels à partir du client de hello. Hello exemple suivant applique les point de terminaison tooan de compte hello Customer1 appelé **EndpointName**, ce qui lui donne des droits d’accès complets.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

Pour le point de terminaison HTTPS hello, vous avez également tooindicate hello nom d’hello certificat tooreturn toohello client. Vous pouvez pour cela à l’aide de **EndpointBindingPolicy**, avec certificat hello défini dans une section de certificats dans le manifeste de l’application hello.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a>Mise à niveau de plusieurs applications avec des points de terminaison https
Vous devez toobe veiller à ne pas toouse hello **même port** pour différentes instances de hello même application lors de l’utilisation de http**s**. Hello parce que l’infrastructure de Service ne pourra plus être en mesure de tooupgrade des certificats de hello pour l’une des instances de l’application hello. Par exemple, si l’application les 2 1 ou de l’application souhaite tooupgrade leur toocert cert 1 2. En cas de mise à niveau hello, Service Fabric ont pu nettoyées d’inscription de certificat 1 hello auprès de http.sys bien hello autre application est toujours l’utiliser. tooprevent, Service Fabric détecte qu’il existe déjà une autre instance d’application inscrite sur le port avec un certificat de hello hello (échéance toohttp.sys) et échoue hello l’opération.

Par conséquent, l’infrastructure de Service ne gère pas la mise à niveau à l’aide de deux services **hello même port** dans les instances de l’autre application. En d’autres termes, vous ne pouvez pas utiliser hello même certificat sur différents services sur hello le même port. Si vous avez besoin de toohave partagé de certificats sur hello même port, vous devez tooensure que hello services sont placés sur des ordinateurs différents avec des contraintes de placement. Vous pouvez aussi envisager d’utiliser le cas échéant les ports dynamiques Service Fabric pour chaque service de chaque instance d’application. 

Si vous voyez un échec de mise à niveau avec le protocole https, une erreur d’avertissement indiquant que « hello du serveur HTTP Windows ne pas en charge plusieurs certificats pour les applications qui partagent le même port. »

## <a name="a-complete-application-manifest-example"></a>Exemple complet de manifeste d'application
Hello suivant le manifeste de l’application affiche un grand nombre de hello des paramètres différents :

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application3Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="Stateless1_InstanceCount" DefaultValue="-1" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
         <RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup" />
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed hello EndpointName is secured with https -->
        <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
     </Policies>
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="Stateless1">
         <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
   <Principals>
      <Groups>
         <Group Name="LocalAdminGroup">
            <Membership>
               <SystemGroup Name="Administrators" />
            </Membership>
         </Group>
      </Groups>
      <Users>
         <User Name="LocalAdmin">
            <MemberOf>
               <Group NameRef="LocalAdminGroup" />
            </MemberOf>
         </User>
         <!--Customer1 below create a local account that this service runs under -->
         <User Name="Customer1" />
         <User Name="MyDefaultAccount" AccountType="NetworkService" />
      </Users>
   </Principals>
   <Policies>
      <DefaultRunAsPolicy UserRef="LocalAdmin" />
   </Policies>
   <Certificates>
     <EndpointCertificate Name="Cert1" X509FindValue="FF EE E0 TT JJ DD JJ EE EE XX 23 4T 66 "/>
  </Certificates>
</ApplicationManifest>
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes
* [Comprendre le modèle d’application hello](service-fabric-application-model.md)
* [Spécifier des ressources dans un manifeste de service](service-fabric-service-manifest-resources.md)
* [Déployer une application](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
