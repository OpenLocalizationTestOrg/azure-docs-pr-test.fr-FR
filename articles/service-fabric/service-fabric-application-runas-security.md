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
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="78427-103">Configurer les stratégies de sécurité de votre application</span><span class="sxs-lookup"><span data-stu-id="78427-103">Configure security policies for your application</span></span>
<span data-ttu-id="78427-104">À l’aide de l’infrastructure de Service Azure, vous pouvez sécuriser les applications qui s’exécutent dans le cluster hello sous différents comptes d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="78427-104">By using Azure Service Fabric, you can secure applications that are running in hello cluster under different user accounts.</span></span> <span data-ttu-id="78427-105">Service Fabric permet également de certificats, les fichiers, les répertoires et les ressources hello sécurisée qui sont utilisés par les applications au moment de hello du déploiement sous des comptes d’utilisateur hello--par exemple.</span><span class="sxs-lookup"><span data-stu-id="78427-105">Service Fabric also helps secure hello resources that are used by applications at hello time of deployment under hello user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="78427-106">Ainsi, les applications en cours d’exécution sont plus sécurisées, même dans un environnement hébergé partagé.</span><span class="sxs-lookup"><span data-stu-id="78427-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="78427-107">Par défaut, les applications de Service Fabric s’exécutent sous le compte de hello hello Fabric.exe processus s’exécute sous.</span><span class="sxs-lookup"><span data-stu-id="78427-107">By default, Service Fabric applications run under hello account that hello Fabric.exe process runs under.</span></span> <span data-ttu-id="78427-108">Service Fabric permet aussi hello toorun des applications sous un compte d’utilisateur local ou le compte système local, qui est spécifié dans le manifeste de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="78427-108">Service Fabric also provides hello capability toorun applications under a local user account or local system account, which is specified within hello application manifest.</span></span> <span data-ttu-id="78427-109">Les types de comptes système locaux pris en charge sont **LocalUser**, **NetworkService**, **LocalService** et **LocalSystem**.</span><span class="sxs-lookup"><span data-stu-id="78427-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="78427-110">Lorsque vous exécutez l’infrastructure de Service sur Windows Server dans votre centre de données à l’aide du programme d’installation autonome de hello, vous pouvez utiliser des comptes de domaine Active Directory, y compris les comptes de service administrés de groupe.</span><span class="sxs-lookup"><span data-stu-id="78427-110">When you're running Service Fabric on Windows Server in your datacenter by using hello standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="78427-111">Vous pouvez définir et créer des groupes d’utilisateurs afin qu’un ou plusieurs utilisateurs peuvent être ajoutés tooeach toobe de groupe géré ensemble.</span><span class="sxs-lookup"><span data-stu-id="78427-111">You can define and create user groups so that one or more users can be added tooeach group toobe managed together.</span></span> <span data-ttu-id="78427-112">Cela est utile quand il existe plusieurs utilisateurs pour les points d’entrée de service différent et doivent toohave certains privilèges courants qui sont disponibles au niveau du groupe hello.</span><span class="sxs-lookup"><span data-stu-id="78427-112">This is useful when there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span>

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="78427-113">Configurer une stratégie de hello pour un point d’entrée de service d’installation</span><span class="sxs-lookup"><span data-stu-id="78427-113">Configure hello policy for a service setup entry point</span></span>
<span data-ttu-id="78427-114">Comme décrit dans hello [modèle d’application](service-fabric-application-model.md), hello point d’entrée, le programme d’installation, **SetupEntryPoint**, est un point d’entrée privilégiés qui s’exécute avec hello même les informations d’identification en tant que Service Fabric (généralement hello *NetworkService* compte) avant de n’importe quel autre point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="78427-114">As described in hello [application model](service-fabric-application-model.md), hello setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="78427-115">fichier exécutable Hello spécifié par **EntryPoint** est habituellement hello longue service hôte.</span><span class="sxs-lookup"><span data-stu-id="78427-115">hello executable that is specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="78427-116">Donc avoir une entrée d’installation distinct point évite hôte de service toorun hello exécutable avec des privilèges élevés pour de longues périodes.</span><span class="sxs-lookup"><span data-stu-id="78427-116">So having a separate setup entry point avoids having toorun hello service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="78427-117">Hello exécutable qui **EntryPoint** Spécifie s’exécute après **SetupEntryPoint** se termine avec succès.</span><span class="sxs-lookup"><span data-stu-id="78427-117">hello executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="78427-118">Hello processus résultant est surveillé et redémarré et recommence avec **SetupEntryPoint** si elle se termine ou se bloque de jamais.</span><span class="sxs-lookup"><span data-stu-id="78427-118">hello resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="78427-119">Hello Voici un exemple de manifeste de service simple qu’affiche hello SetupEntryPoint et hello point d’entrée principal pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="78427-119">hello following is a simple service manifest example that shows hello SetupEntryPoint and hello main EntryPoint for hello service.</span></span>

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

### <a name="configure-hello-policy-by-using-a-local-account"></a><span data-ttu-id="78427-120">Configurer la stratégie de hello en utilisant un compte local</span><span class="sxs-lookup"><span data-stu-id="78427-120">Configure hello policy by using a local account</span></span>
<span data-ttu-id="78427-121">Après avoir configuré le service de hello toohave un point d’entrée le programme d’installation, vous pouvez modifier les autorisations de sécurité hello il s’exécute sous dans le manifeste de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="78427-121">After you configure hello service toohave a setup entry point, you can change hello security permissions that it runs under in hello application manifest.</span></span> <span data-ttu-id="78427-122">Bonjour à l’exemple suivant montre comment tooconfigure hello toorun service sous des privilèges de compte d’utilisateur administrateur.</span><span class="sxs-lookup"><span data-stu-id="78427-122">hello following example shows how tooconfigure hello service toorun under user administrator account privileges.</span></span>

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

<span data-ttu-id="78427-123">Tout d’abord, créez une section **Principals** avec un nom d’utilisateur, par exemple SetupAdminUser.</span><span class="sxs-lookup"><span data-stu-id="78427-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="78427-124">Cela indique que l’utilisateur hello est un membre du groupe de hello administrateurs système.</span><span class="sxs-lookup"><span data-stu-id="78427-124">This indicates that hello user is a member of hello Administrators system group.</span></span>

<span data-ttu-id="78427-125">Ensuite, sous hello **ServiceManifestImport** section, configurer, une stratégie tooapply ce principal trop**SetupEntryPoint**.</span><span class="sxs-lookup"><span data-stu-id="78427-125">Next, under hello **ServiceManifestImport** section, configure a policy tooapply this principal too**SetupEntryPoint**.</span></span> <span data-ttu-id="78427-126">Cela indique à l’infrastructure de Service qui lorsque hello **MySetup.bat** fichier est exécuté, il doit être `RunAs` avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="78427-126">This tells Service Fabric that when hello **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="78427-127">Étant donné que vous avez *pas* appliqué un point d’entrée principal toohello stratégie, le code hello dans **MyServiceHost.exe** s’exécute sous un système de hello **NetworkService** compte.</span><span class="sxs-lookup"><span data-stu-id="78427-127">Given that you have *not* applied a policy toohello main entry point, hello code in **MyServiceHost.exe** runs under hello system **NetworkService** account.</span></span> <span data-ttu-id="78427-128">Il s’agit de compte par défaut hello exécutés en tant que tous les points d’entrée de service.</span><span class="sxs-lookup"><span data-stu-id="78427-128">This is hello default account that all service entry points are run as.</span></span>

<span data-ttu-id="78427-129">Vous allez maintenant ajouter hello fichier MySetup.bat toohello Visual Studio projet tootest hello des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="78427-129">Let's now add hello file MySetup.bat toohello Visual Studio project tootest hello administrator privileges.</span></span> <span data-ttu-id="78427-130">Dans Visual Studio, cliquez sur le projet de service hello et ajoutez un nouveau fichier appelé MySetup.bat.</span><span class="sxs-lookup"><span data-stu-id="78427-130">In Visual Studio, right-click hello service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="78427-131">Vérifiez ensuite que ce fichier de MySetup.bat hello est inclus dans le package de service hello.</span><span class="sxs-lookup"><span data-stu-id="78427-131">Next, ensure that hello MySetup.bat file is included in hello service package.</span></span> <span data-ttu-id="78427-132">Par défaut, il ne l’est pas.</span><span class="sxs-lookup"><span data-stu-id="78427-132">By default, it is not.</span></span> <span data-ttu-id="78427-133">Sélectionnez le fichier de hello, tooget hello contexte menu contextuel et choisissez **propriétés**.</span><span class="sxs-lookup"><span data-stu-id="78427-133">Select hello file, right-click tooget hello context menu, and choose **Properties**.</span></span> <span data-ttu-id="78427-134">Dans la boîte de dialogue de propriétés hello, vérifiez que **copier tooOutput active** est défini trop**Copier si plus récent**.</span><span class="sxs-lookup"><span data-stu-id="78427-134">In hello Properties dialog box, ensure that **Copy tooOutput Directory** is set too**Copy if newer**.</span></span> <span data-ttu-id="78427-135">Consultez hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="78427-135">See hello following screenshot.</span></span>

![Visual Studio CopyToOutput pour fichier batch SetupEntryPoint][image1]

<span data-ttu-id="78427-137">Maintenant ouvrir le fichier de MySetup.bat hello et ajouter hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="78427-137">Now open hello MySetup.bat file and add hello following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="78427-138">Ensuite, générer et déployer le cluster de développement local tooa hello solution.</span><span class="sxs-lookup"><span data-stu-id="78427-138">Next, build and deploy hello solution tooa local development cluster.</span></span> <span data-ttu-id="78427-139">Après hello a démarrage du service, comme indiqué dans l’Explorateur de l’infrastructure de Service, vous pouvez voir le que fichier MySetup.bat hello réussie de deux manières.</span><span class="sxs-lookup"><span data-stu-id="78427-139">After hello service has started, as shown in Service Fabric Explorer, you can see that hello MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="78427-140">Ouvrez une invite de commandes PowerShell et entrez :</span><span class="sxs-lookup"><span data-stu-id="78427-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="78427-141">Ensuite, notez hello nom du nœud hello où le service de hello a été déployé et lancé dans le Service Fabric Explorer--par exemple, nœud 2.</span><span class="sxs-lookup"><span data-stu-id="78427-141">Then, note hello name of hello node where hello service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="78427-142">Ensuite, accédez toohello application instance travail toofind hello out.txt fichiers du dossier qui affiche la valeur hello **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="78427-142">Next, navigate toohello application instance work folder toofind hello out.txt file that shows hello value of **TestVariable**.</span></span> <span data-ttu-id="78427-143">Par exemple, si ce service a été déployé tooNode 2, vous pouvez passer toothis chemin hello **MyApplicationType**:</span><span class="sxs-lookup"><span data-stu-id="78427-143">For example, if this service was deployed tooNode 2, then you can go toothis path for hello **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a><span data-ttu-id="78427-144">Configurer la stratégie de hello en utilisant des comptes système local</span><span class="sxs-lookup"><span data-stu-id="78427-144">Configure hello policy by using local system accounts</span></span>
<span data-ttu-id="78427-145">Souvent, c’est le script de démarrage hello toorun préférable à l’aide d’un compte système local plutôt que d’un compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="78427-145">Often, it's preferable toorun hello startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="78427-146">Exécution de la stratégie de RunAs hello en tant que membre du groupe Administrateurs généralement ne fonctionne pas correctement, car les ordinateurs ont accès contrôle utilisateur (UAC) activé par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="78427-146">Running hello RunAs policy as a member of hello Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="78427-147">Dans ce cas, **recommandation de hello est toorun hello SetupEntryPoint en tant que LocalSystem, au lieu d’en tant qu’un groupe d’utilisateurs local ajouté tooAdministrators**.</span><span class="sxs-lookup"><span data-stu-id="78427-147">In such cases, **hello recommendation is toorun hello SetupEntryPoint as LocalSystem, instead of as a local user added tooAdministrators group**.</span></span> <span data-ttu-id="78427-148">Hello suivant montre paramètre hello SetupEntryPoint toorun en tant que LocalSystem :</span><span class="sxs-lookup"><span data-stu-id="78427-148">hello following example shows setting hello SetupEntryPoint toorun as LocalSystem:</span></span>

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

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="78427-149">Lancer des commandes PowerShell à partir d’un point d’entrée de configuration</span><span class="sxs-lookup"><span data-stu-id="78427-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="78427-150">toorun PowerShell à partir de hello **SetupEntryPoint** point, vous pouvez exécuter **PowerShell.exe** dans un fichier de commandes qui pointe tooa PowerShell de fichiers.</span><span class="sxs-lookup"><span data-stu-id="78427-150">toorun PowerShell from hello **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points tooa PowerShell file.</span></span> <span data-ttu-id="78427-151">Tout d’abord, ajoutez un projet de service PowerShell fichier toohello--par exemple, **MySetup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="78427-151">First, add a PowerShell file toohello service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="78427-152">N’oubliez pas de tooset hello *Copier si plus récent* propriété pour ce fichier hello est également inclus dans le package de service hello.</span><span class="sxs-lookup"><span data-stu-id="78427-152">Remember tooset hello *Copy if newer* property so that hello file is also included in hello service package.</span></span> <span data-ttu-id="78427-153">Hello suivant montre un exemple de fichier de traitement par lots qui démarre un fichier PowerShell appelé MySetup.ps1, qui définit une variable d’environnement système appelée **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="78427-153">hello following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="78427-154">MySetup.bat toostart un fichier de PowerShell :</span><span class="sxs-lookup"><span data-stu-id="78427-154">MySetup.bat toostart a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="78427-155">Dans le fichier de PowerShell hello, ajoutez hello suivant tooset une variable d’environnement système :</span><span class="sxs-lookup"><span data-stu-id="78427-155">In hello PowerShell file, add hello following tooset a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="78427-156">Par défaut, lorsque le fichier de commandes hello s’exécute, il examine appelé dossier de l’application hello **fonctionne** pour les fichiers.</span><span class="sxs-lookup"><span data-stu-id="78427-156">By default, when hello batch file runs, it looks at hello application folder called **work** for files.</span></span> <span data-ttu-id="78427-157">Dans ce cas, MySetup.bat s’exécute, nous souhaitons cette hello toofind MySetup.ps1 fichier Bonjour même dossier, qui est l’application hello **package de code** dossier.</span><span class="sxs-lookup"><span data-stu-id="78427-157">In this case, when MySetup.bat runs, we want this toofind hello MySetup.ps1 file in hello same folder, which is hello application **code package** folder.</span></span> <span data-ttu-id="78427-158">toochange ce dossier, le dossier de travail ensemble hello :</span><span class="sxs-lookup"><span data-stu-id="78427-158">toochange this folder, set hello working folder:</span></span>
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

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="78427-159">Utiliser la console de redirection pour le débogage local</span><span class="sxs-lookup"><span data-stu-id="78427-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="78427-160">Il est parfois utile toosee sortie de console hello à partir d’un script pour le débogage en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="78427-160">Occasionally, it's useful toosee hello console output from running a script for debugging purposes.</span></span> <span data-ttu-id="78427-161">toodo, vous pouvez définir une stratégie de redirection de console, qui écrit le fichier de sortie de tooa hello.</span><span class="sxs-lookup"><span data-stu-id="78427-161">toodo this, you can set a console redirection policy, which writes hello output tooa file.</span></span> <span data-ttu-id="78427-162">Hello fichier de sortie est appelée de dossier de l’application écrit toohello **journal** sur le nœud hello où l’application hello est déployée et exécutée.</span><span class="sxs-lookup"><span data-stu-id="78427-162">hello file output is written toohello application folder called **log** on hello node where hello application is deployed and run.</span></span> <span data-ttu-id="78427-163">(Consultez la rubrique toofind cela Bonjour précédent exemple.)</span><span class="sxs-lookup"><span data-stu-id="78427-163">(See where toofind this in hello preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="78427-164">N’utilisez jamais de stratégie de redirection de console hello dans une application est déployée en production, car cela peut affecter le basculement d’application hello.</span><span class="sxs-lookup"><span data-stu-id="78427-164">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="78427-165">N’utilisez cette stratégie *que* pour le développement local et à des fins de débogage.</span><span class="sxs-lookup"><span data-stu-id="78427-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="78427-166">Hello exemple suivant illustre la redirection de la console hello de paramètre avec la valeur FileRetentionCount :</span><span class="sxs-lookup"><span data-stu-id="78427-166">hello following example shows setting hello console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="78427-167">Si vous modifiez maintenant hello MySetup.ps1 fichier toowrite une **Echo** commande, il écrit le fichier de sortie toohello à des fins de débogage :</span><span class="sxs-lookup"><span data-stu-id="78427-167">If you now change hello MySetup.ps1 file toowrite an **Echo** command, this will write toohello output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

<span data-ttu-id="78427-168">**Une fois que vous avez débogué votre script, supprimez immédiatement cette stratégie de redirection de console**.</span><span class="sxs-lookup"><span data-stu-id="78427-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="78427-169">Configurer une stratégie pour les packages de code de service</span><span class="sxs-lookup"><span data-stu-id="78427-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="78427-170">Bonjour étapes précédentes, vous avez vu comment tooapply un tooSetupEntryPoint de stratégie d’identification.</span><span class="sxs-lookup"><span data-stu-id="78427-170">In hello preceding steps, you saw how tooapply a RunAs policy tooSetupEntryPoint.</span></span> <span data-ttu-id="78427-171">Examinons un peu plus loin comment toocreate principaux différents qui peut être appliquées en tant que stratégies de service.</span><span class="sxs-lookup"><span data-stu-id="78427-171">Let's look a little deeper into how toocreate different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="78427-172">Création de groupes d'utilisateurs locaux</span><span class="sxs-lookup"><span data-stu-id="78427-172">Create local user groups</span></span>
<span data-ttu-id="78427-173">Vous pouvez définir et créer des groupes d’utilisateurs qui permet d’utiliser un ou plusieurs utilisateurs toobe tooa ajouté.</span><span class="sxs-lookup"><span data-stu-id="78427-173">You can define and create user groups that allow one or more users toobe added tooa group.</span></span> <span data-ttu-id="78427-174">Cela est utile s’il existe plusieurs utilisateurs pour les points d’entrée de service différent et ils doivent toohave certains privilèges courants qui sont disponibles au niveau du groupe hello.</span><span class="sxs-lookup"><span data-stu-id="78427-174">This is useful if there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span> <span data-ttu-id="78427-175">Hello suivant montre un groupe local appelé **LocalAdminGroup** disposant des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="78427-175">hello following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="78427-176">Deux utilisateurs, Customer1 et Customer2, deviennent membres de ce groupe local.</span><span class="sxs-lookup"><span data-stu-id="78427-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

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

### <a name="create-local-users"></a><span data-ttu-id="78427-177">Création d'utilisateurs locaux</span><span class="sxs-lookup"><span data-stu-id="78427-177">Create local users</span></span>
<span data-ttu-id="78427-178">Vous pouvez créer un utilisateur local qui peut être utilisé toohelp sécurisée un service au sein de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="78427-178">You can create a local user that can be used toohelp secure a service within hello application.</span></span> <span data-ttu-id="78427-179">Lorsqu’un **UtilisateurLocal** type de compte est spécifié dans la section de principaux de hello de manifeste de l’application hello, Service Fabric crée des comptes d’utilisateurs locaux sur les ordinateurs où l’application hello est déployée.</span><span class="sxs-lookup"><span data-stu-id="78427-179">When a **LocalUser** account type is specified in hello principals section of hello application manifest, Service Fabric creates local user accounts on machines where hello application is deployed.</span></span> <span data-ttu-id="78427-180">Par défaut, ces comptes n’ont pas de hello mêmes noms que ceux spécifiés dans l’application hello manifeste (par exemple, Customer3 Bonjour suivant l’exemple).</span><span class="sxs-lookup"><span data-stu-id="78427-180">By default, these accounts do not have hello same names as those specified in hello application manifest (for example, Customer3 in hello following sample).</span></span> <span data-ttu-id="78427-181">Ils sont générés dynamiquement et sont associés à des mots de passe aléatoires.</span><span class="sxs-lookup"><span data-stu-id="78427-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="78427-182">Si une application nécessite que le mot de passe et le compte d’utilisateur hello être même sur tous les ordinateurs (par exemple, l’authentification NTLM tooenable), le manifeste du cluster hello doit définir NTLMAuthenticationEnabled tootrue.</span><span class="sxs-lookup"><span data-stu-id="78427-182">If an application requires that hello user account and password be same on all machines (for example, tooenable NTLM authentication), hello cluster manifest must set NTLMAuthenticationEnabled tootrue.</span></span> <span data-ttu-id="78427-183">Hello manifeste du cluster doit également spécifier un NTLMAuthenticationPasswordSecret utilisé toogenerate hello même mot de passe sur tous les ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="78427-183">hello cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used toogenerate hello same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a><span data-ttu-id="78427-184">Affecter des stratégies toohello packages de code de service</span><span class="sxs-lookup"><span data-stu-id="78427-184">Assign policies toohello service code packages</span></span>
<span data-ttu-id="78427-185">Hello **RunAsPolicy** section pour un **ServiceManifestImport** Spécifie le compte hello à partir de la section principaux hello qui doit être toorun utilisé un package de code.</span><span class="sxs-lookup"><span data-stu-id="78427-185">hello **RunAsPolicy** section for a **ServiceManifestImport** specifies hello account from hello principals section that should be used toorun a code package.</span></span> <span data-ttu-id="78427-186">Il associe également code packages à partir du service de hello manifeste avec des comptes d’utilisateur dans la section des principaux hello.</span><span class="sxs-lookup"><span data-stu-id="78427-186">It also associates code packages from hello service manifest with user accounts in hello principals section.</span></span> <span data-ttu-id="78427-187">Vous pouvez le spécifier pour le programme d’installation hello ou des points d’entrée principal, ou vous pouvez spécifier `All` tooapply il tooboth.</span><span class="sxs-lookup"><span data-stu-id="78427-187">You can specify this for hello setup or main entry points, or you can specify `All` tooapply it tooboth.</span></span> <span data-ttu-id="78427-188">Hello suivant montre différentes stratégies appliquées :</span><span class="sxs-lookup"><span data-stu-id="78427-188">hello following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="78427-189">Si **EntryPointType** n’est pas spécifié, a la valeur par défaut de hello tooEntryPointType = « Main ».</span><span class="sxs-lookup"><span data-stu-id="78427-189">If **EntryPointType** is not specified, hello default is set tooEntryPointType=”Main”.</span></span> <span data-ttu-id="78427-190">Spécification de **SetupEntryPoint** s’avère particulièrement utile lorsque vous souhaitez toorun certaines opérations à privilèges élevés le programme d’installation sous un compte système.</span><span class="sxs-lookup"><span data-stu-id="78427-190">Specifying **SetupEntryPoint** is especially useful when you want toorun certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="78427-191">code de service réel Hello peut exécuter sous un compte de plus faible privilège.</span><span class="sxs-lookup"><span data-stu-id="78427-191">hello actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-tooall-service-code-packages"></a><span data-ttu-id="78427-192">Appliquer un packages de code de service par défaut stratégie tooall</span><span class="sxs-lookup"><span data-stu-id="78427-192">Apply a default policy tooall service code packages</span></span>
<span data-ttu-id="78427-193">Vous utilisez hello **DefaultRunAsPolicy** section toospecify un compte d’utilisateur par défaut pour tous les packages de code qui n’ont pas un spécifique **RunAsPolicy** défini.</span><span class="sxs-lookup"><span data-stu-id="78427-193">You use hello **DefaultRunAsPolicy** section toospecify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="78427-194">Si la plupart des packages de code hello qui sont spécifiés dans le manifeste du service utilisé par une application hello devez toorun sous hello même utilisateur, hello application peut définir simplement une stratégie de d’identification par défaut avec ce compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="78427-194">If most of hello code packages that are specified in hello service manifest used by an application need toorun under hello same user, hello application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="78427-195">Hello exemple suivant spécifie que si un package de code n’a pas un **RunAsPolicy** spécifié, le package de code hello doit s’exécuter sous hello **MyDefaultAccount** spécifié dans la section des principaux hello.</span><span class="sxs-lookup"><span data-stu-id="78427-195">hello following example specifies that if a code package does not have a **RunAsPolicy** specified, hello code package should run under hello **MyDefaultAccount** specified in hello principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="78427-196">Utiliser un utilisateur ou groupe de domaine Active Directory</span><span class="sxs-lookup"><span data-stu-id="78427-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="78427-197">Pour une instance de l’infrastructure de Service qui a été installé sur Windows Server à l’aide du programme d’installation autonome de hello, vous pouvez exécuter le service hello sous les informations d’identification hello pour un compte d’utilisateur ou un groupe Active Directory.</span><span class="sxs-lookup"><span data-stu-id="78427-197">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service under hello credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="78427-198">Il s’agit d’Active Directory en local au sein de votre domaine et non avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="78427-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="78427-199">À l’aide un utilisateur de domaine ou un groupe, vous pouvez ensuite accéder autres ressources dans le domaine hello (par exemple, les partages de fichiers) qui dispose d’autorisations.</span><span class="sxs-lookup"><span data-stu-id="78427-199">By using a domain user or group, you can then access other resources in hello domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="78427-200">Hello suivant montre un utilisateur Active Directory appelé *TestUser* avec leur domaine mot de passe chiffré à l’aide d’un certificat appelé *MonCert*.</span><span class="sxs-lookup"><span data-stu-id="78427-200">hello following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="78427-201">Vous pouvez utiliser hello `Invoke-ServiceFabricEncryptText` texte de chiffrement secrètes PowerShell commande toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="78427-201">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text.</span></span> <span data-ttu-id="78427-202">Consultez [Gestion des secrets dans des applications Service Fabric](service-fabric-application-secret-management.md) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="78427-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="78427-203">Vous devez déployer la clé privée hello hello certificat toodecrypt hello mot de passe toohello ordinateur local à l’aide d’une méthode hors-bande (dans Azure, il s’agit de via Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="78427-203">You must deploy hello private key of hello certificate toodecrypt hello password toohello local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="78427-204">Ensuite, lorsque le Service Fabric déploie le package toohello ordinateur hello service, il est en mesure de toodecrypt hello secret et (ainsi que le nom d’utilisateur hello) auprès de toorun d’Active Directory avec les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="78427-204">Then, when Service Fabric deploys hello service package toohello machine, it is able toodecrypt hello secret and (along with hello user name) authenticate with Active Directory toorun under those credentials.</span></span>

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
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="78427-205">Utilisez un compte de service géré de groupe.</span><span class="sxs-lookup"><span data-stu-id="78427-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="78427-206">Pour une instance de l’infrastructure de Service qui a été installé sur Windows Server à l’aide du programme d’installation autonome de hello, vous pouvez exécuter le service de hello en tant que groupe (gMSA) du compte de Service administré.</span><span class="sxs-lookup"><span data-stu-id="78427-206">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="78427-207">Remarque : il s’agit d’Active Directory en local au sein de votre domaine et non avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="78427-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="78427-208">À l’aide d’un compte gMSA il n’existe aucun mot de passe ou le mot de passe chiffré stocké dans hello `Application Manifest`.</span><span class="sxs-lookup"><span data-stu-id="78427-208">By using a gMSA there is no password or encrypted password stored in hello `Application Manifest`.</span></span>

<span data-ttu-id="78427-209">Hello exemple suivant montre comment toocreate un compte de service administré de groupe appelée *Test-svc$*; la méthode de gestion de toodeploy que nœuds de cluster de toohello de compte de service, et comment tooconfigure hello principal de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="78427-209">hello following example shows how toocreate a gMSA account called *svc-Test$*; how toodeploy that managed service account toohello cluster nodes; and how tooconfigure hello user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="78427-210">Composants requis.</span><span class="sxs-lookup"><span data-stu-id="78427-210">Prerequisites.</span></span>
- <span data-ttu-id="78427-211">domaine de Hello a besoin d’une clé racine KDS.</span><span class="sxs-lookup"><span data-stu-id="78427-211">hello domain needs a KDS root key.</span></span>
- <span data-ttu-id="78427-212">domaine de Hello doit toobe au plus tard le niveau fonctionnel de Windows Server 2012 ou.</span><span class="sxs-lookup"><span data-stu-id="78427-212">hello domain needs toobe at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="78427-213">Exemple</span><span class="sxs-lookup"><span data-stu-id="78427-213">Example</span></span>
1. <span data-ttu-id="78427-214">Avoir un administrateur de domaine active directory de créer un compte de service administrés de groupe à l’aide de hello `New-ADServiceAccount` applet de commande et assurez-vous que hello `PrincipalsAllowedToRetrieveManagedPassword` inclut tous les nœuds de cluster de l’infrastructure de service hello.</span><span class="sxs-lookup"><span data-stu-id="78427-214">Have an active directory domain administrator create a group managed service account using hello `New-ADServiceAccount` commandlet and ensure that hello `PrincipalsAllowedToRetrieveManagedPassword` includes all of hello service fabric cluster nodes.</span></span> <span data-ttu-id="78427-215">Notez que `AccountName`, `DnsHostName` et `ServicePrincipalName` doivent être uniques.</span><span class="sxs-lookup"><span data-stu-id="78427-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="78427-216">Sur chaque nœud de cluster hello service fabric (par exemple, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), installer et de test de service administré de groupe hello.</span><span class="sxs-lookup"><span data-stu-id="78427-216">On each of hello service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test hello gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="78427-217">Configurez l’UPN hello et configurer hello RunAsPolicy tooreference hello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="78427-217">Configure hello User principal, and configure hello RunAsPolicy tooreference hello user.</span></span>
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

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="78427-218">Affectation d’une stratégie d’accès de sécurité pour des points de terminaison HTTP et HTTPS</span><span class="sxs-lookup"><span data-stu-id="78427-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="78427-219">Si vous appliquez un service tooa de stratégie d’identification et le manifeste de service hello déclare des ressources de point de terminaison avec le protocole de hello HTTP, vous devez spécifier un **SecurityAccessPolicy** tooensure que les ports affectés les points de terminaison toothese sont correctement contrôle d’accès répertoriés pour hello compte d’utilisateur RunAs hello service s’exécute sous.</span><span class="sxs-lookup"><span data-stu-id="78427-219">If you apply a RunAs policy tooa service and hello service manifest declares endpoint resources with hello HTTP protocol, you must specify a **SecurityAccessPolicy** tooensure that ports allocated toothese endpoints are correctly access-control listed for hello RunAs user account that hello service runs under.</span></span> <span data-ttu-id="78427-220">Dans le cas contraire, **http.sys** ne dispose pas d’accès toohello service, et vous obtenez des échecs lors des appels à partir du client de hello.</span><span class="sxs-lookup"><span data-stu-id="78427-220">Otherwise, **http.sys** does not have access toohello service, and you get failures with calls from hello client.</span></span> <span data-ttu-id="78427-221">Hello exemple suivant applique les point de terminaison tooan de compte hello Customer1 appelé **EndpointName**, ce qui lui donne des droits d’accès complets.</span><span class="sxs-lookup"><span data-stu-id="78427-221">hello following example applies hello Customer1 account tooan endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="78427-222">Pour le point de terminaison HTTPS hello, vous avez également tooindicate hello nom d’hello certificat tooreturn toohello client.</span><span class="sxs-lookup"><span data-stu-id="78427-222">For hello HTTPS endpoint, you also have tooindicate hello name of hello certificate tooreturn toohello client.</span></span> <span data-ttu-id="78427-223">Vous pouvez pour cela à l’aide de **EndpointBindingPolicy**, avec certificat hello défini dans une section de certificats dans le manifeste de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="78427-223">You can do this by using **EndpointBindingPolicy**, with hello certificate defined in a certificates section in hello application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="78427-224">Mise à niveau de plusieurs applications avec des points de terminaison https</span><span class="sxs-lookup"><span data-stu-id="78427-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="78427-225">Vous devez toobe veiller à ne pas toouse hello **même port** pour différentes instances de hello même application lors de l’utilisation de http**s**.</span><span class="sxs-lookup"><span data-stu-id="78427-225">You need toobe careful not toouse hello **same port** for different instances of hello same application when using http**s**.</span></span> <span data-ttu-id="78427-226">Hello parce que l’infrastructure de Service ne pourra plus être en mesure de tooupgrade des certificats de hello pour l’une des instances de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="78427-226">hello reason is that Service Fabric won't be able tooupgrade hello cert for one of hello application instances.</span></span> <span data-ttu-id="78427-227">Par exemple, si l’application les 2 1 ou de l’application souhaite tooupgrade leur toocert cert 1 2.</span><span class="sxs-lookup"><span data-stu-id="78427-227">For example, if application 1 or application 2 both want tooupgrade their cert 1 toocert 2.</span></span> <span data-ttu-id="78427-228">En cas de mise à niveau hello, Service Fabric ont pu nettoyées d’inscription de certificat 1 hello auprès de http.sys bien hello autre application est toujours l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="78427-228">When hello upgrade happens, Service Fabric might have cleaned up hello cert 1 registration with http.sys even though hello other application is still using it.</span></span> <span data-ttu-id="78427-229">tooprevent, Service Fabric détecte qu’il existe déjà une autre instance d’application inscrite sur le port avec un certificat de hello hello (échéance toohttp.sys) et échoue hello l’opération.</span><span class="sxs-lookup"><span data-stu-id="78427-229">tooprevent this, Service Fabric detects that there is already another application instance registered on hello port with hello certificate (due toohttp.sys) and fails hello operation.</span></span>

<span data-ttu-id="78427-230">Par conséquent, l’infrastructure de Service ne gère pas la mise à niveau à l’aide de deux services **hello même port** dans les instances de l’autre application.</span><span class="sxs-lookup"><span data-stu-id="78427-230">Hence Service Fabric does not support upgrading two different services using **hello same port** in different application instances.</span></span> <span data-ttu-id="78427-231">En d’autres termes, vous ne pouvez pas utiliser hello même certificat sur différents services sur hello le même port.</span><span class="sxs-lookup"><span data-stu-id="78427-231">In other words, you cannot use hello same certificate on different services on hello same port.</span></span> <span data-ttu-id="78427-232">Si vous avez besoin de toohave partagé de certificats sur hello même port, vous devez tooensure que hello services sont placés sur des ordinateurs différents avec des contraintes de placement.</span><span class="sxs-lookup"><span data-stu-id="78427-232">If you need toohave a shared certificate on hello same port, you need tooensure that hello services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="78427-233">Vous pouvez aussi envisager d’utiliser le cas échéant les ports dynamiques Service Fabric pour chaque service de chaque instance d’application.</span><span class="sxs-lookup"><span data-stu-id="78427-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="78427-234">Si vous voyez un échec de mise à niveau avec le protocole https, une erreur d’avertissement indiquant que « hello du serveur HTTP Windows ne pas en charge plusieurs certificats pour les applications qui partagent le même port. »</span><span class="sxs-lookup"><span data-stu-id="78427-234">If you see an upgrade fail with https, an error warning saying "hello Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="78427-235">Exemple complet de manifeste d'application</span><span class="sxs-lookup"><span data-stu-id="78427-235">A complete application manifest example</span></span>
<span data-ttu-id="78427-236">Hello suivant le manifeste de l’application affiche un grand nombre de hello des paramètres différents :</span><span class="sxs-lookup"><span data-stu-id="78427-236">hello following application manifest shows many of hello different settings:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="78427-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="78427-237">Next steps</span></span>
* [<span data-ttu-id="78427-238">Comprendre le modèle d’application hello</span><span class="sxs-lookup"><span data-stu-id="78427-238">Understand hello application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="78427-239">Spécifier des ressources dans un manifeste de service</span><span class="sxs-lookup"><span data-stu-id="78427-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="78427-240">Déployer une application</span><span class="sxs-lookup"><span data-stu-id="78427-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
