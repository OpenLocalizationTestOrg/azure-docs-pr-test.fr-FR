---
title: "aaaCommon des tâches de démarrage pour les Services de cloud computing | Documents Microsoft"
description: "Fournit des exemples de tâches courantes de démarrage, vous souhaiterez tooperform dans votre rôle web de services cloud ou le rôle de travail."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: a7095dad-1ee7-4141-bc6a-ef19a6e570f1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: c80fac4079439410dfc3795e4bce0fbc07dbbfab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="common-cloud-service-startup-tasks"></a><span data-ttu-id="d1119-103">Tâches courantes de démarrage dans le service cloud</span><span class="sxs-lookup"><span data-stu-id="d1119-103">Common Cloud Service startup tasks</span></span>
<span data-ttu-id="d1119-104">Cet article fournit des exemples de tâches courantes de démarrage peut souhaité tooperform dans votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="d1119-104">This article provides some examples of common startup tasks you may want tooperform in your cloud service.</span></span> <span data-ttu-id="d1119-105">Vous pouvez utiliser les opérations de tooperform de tâches de démarrage avant le démarrage d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="d1119-105">You can use startup tasks tooperform operations before a role starts.</span></span> <span data-ttu-id="d1119-106">Les opérations que vous pourriez tooperform incluent l’installation d’un composant, l’inscription des composants COM, définition de clés de Registre ou à partir d’un processus à long terme.</span><span class="sxs-lookup"><span data-stu-id="d1119-106">Operations that you might want tooperform include installing a component, registering COM components, setting registry keys, or starting a long running process.</span></span> 

<span data-ttu-id="d1119-107">Consultez [cet article](cloud-services-startup-tasks.md) toounderstand comment fonctionnent les tâches de démarrage et en particulier comment toocreate hello entrées qui définissent une tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d1119-107">See [this article](cloud-services-startup-tasks.md) toounderstand how startup tasks work, and specifically how toocreate hello entries that define a startup task.</span></span>

> [!NOTE]
> <span data-ttu-id="d1119-108">Tâches de démarrage ne sont pas applicables tooVirtual Machines, tooCloud Service Web et les rôles de travail.</span><span class="sxs-lookup"><span data-stu-id="d1119-108">Startup tasks are not applicable tooVirtual Machines, only tooCloud Service Web and Worker roles.</span></span>
> 

## <a name="define-environment-variables-before-a-role-starts"></a><span data-ttu-id="d1119-109">Définir des variables d’environnement avant le démarrage d’un rôle</span><span class="sxs-lookup"><span data-stu-id="d1119-109">Define environment variables before a role starts</span></span>
<span data-ttu-id="d1119-110">Si vous avez besoin de variables d’environnement définies pour une tâche spécifique, utilisez hello [environnement] élément à l’intérieur de hello [tâche] élément.</span><span class="sxs-lookup"><span data-stu-id="d1119-110">If you need environment variables defined for a specific task, use hello [Environment] element inside hello [Task] element.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
                <Environment>
                    <Variable name="MyEnvironmentVariable" value="MyVariableValue" />
                </Environment>
            </Task>
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="d1119-111">Les variables peuvent également utiliser un [valeur Azure XPath valide](cloud-services-role-config-xpath.md) tooreference quelque chose sur le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="d1119-111">Variables can also use a [valid Azure XPath value](cloud-services-role-config-xpath.md) tooreference something about hello deployment.</span></span> <span data-ttu-id="d1119-112">Au lieu d’utiliser hello `value` d’attribut, de définir un [RoleInstanceValue] élément enfant.</span><span class="sxs-lookup"><span data-stu-id="d1119-112">Instead of using hello `value` attribute, define a [RoleInstanceValue] child element.</span></span>

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a><span data-ttu-id="d1119-113">Configurer le démarrage d’IIS avec AppCmd.exe</span><span class="sxs-lookup"><span data-stu-id="d1119-113">Configure IIS startup with AppCmd.exe</span></span>
<span data-ttu-id="d1119-114">Hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) outil de ligne de commande peut être utilisé toomanage les paramètres IIS au démarrage sur Azure.</span><span class="sxs-lookup"><span data-stu-id="d1119-114">hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) command-line tool can be used toomanage IIS settings at startup on Azure.</span></span> <span data-ttu-id="d1119-115">*AppCmd.exe* fournit des paramètres de tooconfiguration d’un accès pratique de ligne de commande pour une utilisation dans les tâches de démarrage sur Azure.</span><span class="sxs-lookup"><span data-stu-id="d1119-115">*AppCmd.exe* provides convenient, command-line access tooconfiguration settings for use in startup tasks on Azure.</span></span> <span data-ttu-id="d1119-116">*AppCmd.exe*permet d’ajouter, de modifier ou de supprimer des paramètres de site web pour les applications et les sites.</span><span class="sxs-lookup"><span data-stu-id="d1119-116">Using *AppCmd.exe*, Website settings can be added, modified, or removed for applications and sites.</span></span>

<span data-ttu-id="d1119-117">Toutefois, il existe quelques toowatch de choses out pour utilisation hello de *AppCmd.exe* comme une tâche de démarrage :</span><span class="sxs-lookup"><span data-stu-id="d1119-117">However, there are a few things toowatch out for in hello use of *AppCmd.exe* as a startup task:</span></span>

* <span data-ttu-id="d1119-118">Les tâches de démarrage peuvent être exécutées plusieurs fois entre les redémarrages.</span><span class="sxs-lookup"><span data-stu-id="d1119-118">Startup tasks can be run more than once between reboots.</span></span> <span data-ttu-id="d1119-119">Par exemple, lorsqu’un rôle est recyclé.</span><span class="sxs-lookup"><span data-stu-id="d1119-119">For instance, when a role recycles.</span></span>
* <span data-ttu-id="d1119-120">Si une action *AppCmd.exe* est exécutée plusieurs fois, cela peut générer une erreur.</span><span class="sxs-lookup"><span data-stu-id="d1119-120">If a *AppCmd.exe* action is performed more than once, it may generate an error.</span></span> <span data-ttu-id="d1119-121">Par exemple, essayer de trop tooadd une section*Web.config* deux fois la peut générer une erreur.</span><span class="sxs-lookup"><span data-stu-id="d1119-121">For example, attempting tooadd a section too*Web.config* twice could generate an error.</span></span>
* <span data-ttu-id="d1119-122">Les tâches de démarrage échouent si elles retournent un code de sortie non nul ou **errorlevel**.</span><span class="sxs-lookup"><span data-stu-id="d1119-122">Startup tasks fail if they return a non-zero exit code or **errorlevel**.</span></span> <span data-ttu-id="d1119-123">Par exemple, lorsque *AppCmd.exe* génère une erreur.</span><span class="sxs-lookup"><span data-stu-id="d1119-123">For example, when *AppCmd.exe* generates an error.</span></span>

<span data-ttu-id="d1119-124">Il s’agit d’une salutation toocheck de bonnes pratiques **errorlevel** après avoir appelé *AppCmd.exe*, qui est toodo facile si vous encapsulez les appels hello trop*AppCmd.exe* avec un *.cmd*  fichier.</span><span class="sxs-lookup"><span data-stu-id="d1119-124">It is a good practice toocheck hello **errorlevel** after calling *AppCmd.exe*, which is easy toodo if you wrap hello call too*AppCmd.exe* with a *.cmd* file.</span></span> <span data-ttu-id="d1119-125">Si vous détectez une réponse **errorlevel** connue, vous pouvez l’ignorer, ou bien la retransmettre.</span><span class="sxs-lookup"><span data-stu-id="d1119-125">If you detect a known **errorlevel** response, you can ignore it, or pass it back.</span></span>

<span data-ttu-id="d1119-126">Hello errorlevel retournée par *AppCmd.exe* sont répertoriées dans le fichier winerror.h de hello et peuvent également être consultés sur [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1119-126">hello errorlevel returned by *AppCmd.exe* are listed in hello winerror.h file, and can also be seen on [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).</span></span>

### <a name="example-of-managing-hello-error-level"></a><span data-ttu-id="d1119-127">Exemple de gestion de niveau d’erreur hello</span><span class="sxs-lookup"><span data-stu-id="d1119-127">Example of managing hello error level</span></span>
<span data-ttu-id="d1119-128">Cet exemple ajoute une section de compression et une entrée de compression pour JSON toohello *Web.config* fichier, avec la gestion des erreurs et enregistrement.</span><span class="sxs-lookup"><span data-stu-id="d1119-128">This example adds a compression section and a compression entry for JSON toohello *Web.config* file, with error handling and logging.</span></span>

<span data-ttu-id="d1119-129">Hello les sections pertinentes de hello [ServiceDefinition.csdef] fichier sont indiqués ici, qui incluent le paramètre hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) trop d’attributs`elevated` toogive *AppCmd.exe*  suffisamment toochange hello les paramètres d’autorisation Bonjour *Web.config* fichier :</span><span class="sxs-lookup"><span data-stu-id="d1119-129">hello relevant sections of hello [ServiceDefinition.csdef] file are shown here, which include setting hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) attribute too`elevated` toogive *AppCmd.exe* sufficient permissions toochange hello settings in hello *Web.config* file:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="Startup.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="d1119-130">Hello *Startup.cmd* par lots de fichiers utilise *AppCmd.exe* tooadd une section de compression et une entrée de compression pour JSON toohello *Web.config* fichier.</span><span class="sxs-lookup"><span data-stu-id="d1119-130">hello *Startup.cmd* batch file uses *AppCmd.exe* tooadd a compression section and a compression entry for JSON toohello *Web.config* file.</span></span> <span data-ttu-id="d1119-131">Hello attendu **errorlevel** 183 a la valeur toozero à l’aide de hello vérifier. Programme de ligne de commande du fichier EXE.</span><span class="sxs-lookup"><span data-stu-id="d1119-131">hello expected **errorlevel** of 183 is set toozero using hello VERIFY.EXE command-line program.</span></span> <span data-ttu-id="d1119-132">Les errorlevels inattendus sont tooStartupErrorLog.txt connecté.</span><span class="sxs-lookup"><span data-stu-id="d1119-132">Unexpected errorlevels are logged tooStartupErrorLog.txt.</span></span>

```cmd
REM   *** Add a compression section toohello Web.config file. ***
%windir%\system32\inetsrv\appcmd set config /section:urlCompression /doDynamicCompression:True /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1

REM   ERRORLEVEL 183 occurs when trying tooadd a section that already exists. This error is expected if this
REM   batch file were executed twice. This can occur and must be accounted for in a Azure startup
REM   task. toohandle this situation, set hello ERRORLEVEL toozero by using hello Verify command. hello Verify
REM   command will safely set hello ERRORLEVEL toozero.
IF %ERRORLEVEL% EQU 183 DO VERIFY > NUL

REM   If hello ERRORLEVEL is not zero at this point, some other error occurred.
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding a compression section toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Add compression for json. ***
%windir%\system32\inetsrv\appcmd set config  -section:system.webServer/httpCompression /+"dynamicTypes.[mimeType='application/json; charset=utf-8',enabled='True']" /commit:apphost >> "%TEMP%\StartupLog.txt" 2>&1
IF %ERRORLEVEL% EQU 183 VERIFY > NUL
IF %ERRORLEVEL% NEQ 0 (
    ECHO Error adding hello JSON compression type toohello Web.config file. >> "%TEMP%\StartupLog.txt" 2>&1
    GOTO ErrorExit
)

REM   *** Exit batch file. ***
EXIT /b 0

REM   *** Log error and exit ***
:ErrorExit
REM   Report hello date, time, and ERRORLEVEL of hello error.
DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
ECHO An error occurred during startup. ERRORLEVEL = %ERRORLEVEL% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT %ERRORLEVEL%
```

## <a name="add-firewall-rules"></a><span data-ttu-id="d1119-133">Ajouter des règles de pare-feu</span><span class="sxs-lookup"><span data-stu-id="d1119-133">Add firewall rules</span></span>
<span data-ttu-id="d1119-134">Dans Azure, il existe en fait deux pare-feu.</span><span class="sxs-lookup"><span data-stu-id="d1119-134">In Azure, there are effectively two firewalls.</span></span> <span data-ttu-id="d1119-135">Hello premier pare-feu contrôle les connexions entre des VM hello et hello world à l’extérieur.</span><span class="sxs-lookup"><span data-stu-id="d1119-135">hello first firewall controls connections between hello virtual machine and hello outside world.</span></span> <span data-ttu-id="d1119-136">Ce pare-feu est contrôlé par hello [points de terminaison] élément Bonjour [ServiceDefinition.csdef] fichier.</span><span class="sxs-lookup"><span data-stu-id="d1119-136">This firewall is controlled by hello [EndPoints] element in hello [ServiceDefinition.csdef] file.</span></span>

<span data-ttu-id="d1119-137">Hello deuxième pare-feu contrôle les connexions entre ordinateur virtuel de hello et processus hello au sein de cet ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="d1119-137">hello second firewall controls connections between hello virtual machine and hello processes within that virtual machine.</span></span> <span data-ttu-id="d1119-138">Ce pare-feu peut être contrôlé par hello `netsh advfirewall firewall` outil de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="d1119-138">This firewall can be controlled by hello `netsh advfirewall firewall` command-line tool.</span></span>

<span data-ttu-id="d1119-139">Azure crée des règles de pare-feu pour les processus de hello démarrés au sein de vos rôles.</span><span class="sxs-lookup"><span data-stu-id="d1119-139">Azure creates firewall rules for hello processes started within your roles.</span></span> <span data-ttu-id="d1119-140">Par exemple, lorsque vous démarrez un service ou un programme, Azure crée automatiquement tooallow de règles de pare-feu nécessaires hello toocommunicate de ce service par hello Internet.</span><span class="sxs-lookup"><span data-stu-id="d1119-140">For example, when you start a service or program, Azure automatically creates hello necessary firewall rules tooallow that service toocommunicate with hello Internet.</span></span> <span data-ttu-id="d1119-141">Toutefois, si vous créez un service qui est démarré par un processus en dehors de votre rôle (comme un service COM + ou une tâche planifiée Windows), vous devez toomanually créer un service de pare-feu règle tooallow accès toothat.</span><span class="sxs-lookup"><span data-stu-id="d1119-141">However, if you create a service that is started by a process outside your role (like a COM+ service or a Windows Scheduled Task), you need toomanually create a firewall rule tooallow access toothat service.</span></span> <span data-ttu-id="d1119-142">Ces règles de pare-feu peuvent être créées à l’aide d’une tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d1119-142">These firewall rules can be created by using a startup task.</span></span>

<span data-ttu-id="d1119-143">Une tâche de démarrage qui crée une règle de pare-feu doit avoir [executionContext][tâche] défini sur **elevated**.</span><span class="sxs-lookup"><span data-stu-id="d1119-143">A startup task that creates a firewall rule must have an [executionContext][Task] of **elevated**.</span></span> <span data-ttu-id="d1119-144">Ajouter hello suivant toohello de tâche de démarrage [ServiceDefinition.csdef] fichier.</span><span class="sxs-lookup"><span data-stu-id="d1119-144">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WorkerRole name="WorkerRole1">
        ...
        <Startup>
            <Task commandLine="AddFirewallRules.cmd" executionContext="elevated" taskType="simple" />
        </Startup>
    </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="d1119-145">règle de pare-feu de hello tooadd, vous devez utiliser hello approprié `netsh advfirewall firewall` commandes dans votre fichier de commandes de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d1119-145">tooadd hello firewall rule, you must use hello appropriate `netsh advfirewall firewall` commands in your startup batch file.</span></span> <span data-ttu-id="d1119-146">Dans cet exemple, la tâche de démarrage de hello nécessite de chiffrement et sécurité pour le port TCP 80.</span><span class="sxs-lookup"><span data-stu-id="d1119-146">In this example, hello startup task requires security and encryption for TCP port 80.</span></span>

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a><span data-ttu-id="d1119-147">Bloquer une adresse IP spécifique</span><span class="sxs-lookup"><span data-stu-id="d1119-147">Block a specific IP address</span></span>
<span data-ttu-id="d1119-148">Vous pouvez limiter un ensemble de tooa d’accès de rôle web Azure d’adresses IP spécifiques en modifiant votre IIS **web.config** fichier.</span><span class="sxs-lookup"><span data-stu-id="d1119-148">You can restrict an Azure web role access tooa set of specified IP addresses by modifying your IIS **web.config** file.</span></span> <span data-ttu-id="d1119-149">Vous devez également toouse un fichier de commandes qui déverrouille hello **IPSec** section Hello **ApplicationHost.config** fichier.</span><span class="sxs-lookup"><span data-stu-id="d1119-149">You also need toouse a command file which unlocks hello **ipSecurity** section of hello **ApplicationHost.config** file.</span></span>

<span data-ttu-id="d1119-150">toodo déverrouiller hello **IPSec** section Hello **ApplicationHost.config** de fichiers, créez un fichier de commandes qui s’exécute au démarrage de rôle.</span><span class="sxs-lookup"><span data-stu-id="d1119-150">toodo unlock hello **ipSecurity** section of hello **ApplicationHost.config** file, create a command file that runs at role start.</span></span> <span data-ttu-id="d1119-151">Créez un dossier au niveau de votre rôle web appelé racine de hello **démarrage** et, dans ce dossier, créez un fichier de commandes appelé **startup.cmd**.</span><span class="sxs-lookup"><span data-stu-id="d1119-151">Create a folder at hello root level of your web role called **startup** and, within this folder, create a batch file called **startup.cmd**.</span></span> <span data-ttu-id="d1119-152">Ajouter ce fichier de projet de Visual Studio tooyour et définir les propriétés de hello trop**toujours copier** tooensure qu’il est inclus dans votre package.</span><span class="sxs-lookup"><span data-stu-id="d1119-152">Add this file tooyour Visual Studio project and set hello properties too**Copy Always** tooensure that it is included in your package.</span></span>

<span data-ttu-id="d1119-153">Ajouter hello suivant toohello de tâche de démarrage [ServiceDefinition.csdef] fichier.</span><span class="sxs-lookup"><span data-stu-id="d1119-153">Add hello following startup task toohello [ServiceDefinition.csdef] file.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
    <WebRole name="WebRole1">
        ...
        <Startup>
            <Task commandLine="startup.cmd" executionContext="elevated" />
        </Startup>
    </WebRole>
</ServiceDefinition>
```

<span data-ttu-id="d1119-154">Ajoutez cette commande toohello **startup.cmd** fichier :</span><span class="sxs-lookup"><span data-stu-id="d1119-154">Add this command toohello **startup.cmd** file:</span></span>

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

<span data-ttu-id="d1119-155">Cette tâche, Bonjour **startup.cmd** toobe de fichier exécute chaque fois que rôle web de hello est initialisé, garantissant que hello requis du lot **IPSec** section est déverrouillée.</span><span class="sxs-lookup"><span data-stu-id="d1119-155">This task causes hello **startup.cmd** batch file toobe run every time hello web role is initialized, ensuring that hello required **ipSecurity** section is unlocked.</span></span>

<span data-ttu-id="d1119-156">Enfin, modifiez hello [section system.webServer](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) de votre rôle web **web.config** fichier tooadd une liste d’adresses IP qui ont accès, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d1119-156">Finally, modify hello [system.webServer section](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) your web role’s **web.config** file tooadd a list of IP addresses that are granted access, as shown in hello following example:</span></span>

<span data-ttu-id="d1119-157">Cet exemple de configuration **permet** toutes les adresses IP tooaccess hello serveur sauf hello deux définies</span><span class="sxs-lookup"><span data-stu-id="d1119-157">This sample config **allows** all IPs tooaccess hello server except hello two defined</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are granted access-->
    <ipSecurity>
        <!--hello following IP addresses are denied access-->
        <add allowed="false" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="false" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

<span data-ttu-id="d1119-158">Cet exemple de configuration **refuse** toutes les adresses IP d’accéder au serveur hello à l’exception de hello deux défini.</span><span class="sxs-lookup"><span data-stu-id="d1119-158">This sample config **denies** all IPs from accessing hello server except for hello two defined.</span></span>

```xml
<system.webServer>
    <security>
    <!--Unlisted IP addresses are denied access-->
    <ipSecurity allowUnlisted="false">
        <!--hello following IP addresses are granted access-->
        <add allowed="true" ipAddress="192.168.100.1" subnetMask="255.255.0.0" />
        <add allowed="true" ipAddress="192.168.100.2" subnetMask="255.255.0.0" />
    </ipSecurity>
    </security>
</system.webServer>
```

## <a name="create-a-powershell-startup-task"></a><span data-ttu-id="d1119-159">Créer une tâche de démarrage PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1119-159">Create a PowerShell startup task</span></span>
<span data-ttu-id="d1119-160">Les scripts Windows PowerShell ne peut pas être appelées directement à partir de hello [ServiceDefinition.csdef] fichier, mais ils peuvent être appelés à partir d’un fichier de commandes de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d1119-160">Windows PowerShell scripts cannot be called directly from hello [ServiceDefinition.csdef] file, but they can be invoked from within a startup batch file.</span></span>

<span data-ttu-id="d1119-161">PowerShell (par défaut) n’exécute pas de scripts non signés.</span><span class="sxs-lookup"><span data-stu-id="d1119-161">PowerShell (by default) does not run unsigned scripts.</span></span> <span data-ttu-id="d1119-162">Sauf si vous vous connectez à votre script, vous devez tooconfigure PowerShell toorun les scripts non signés.</span><span class="sxs-lookup"><span data-stu-id="d1119-162">Unless you sign your script, you need tooconfigure PowerShell toorun unsigned scripts.</span></span> <span data-ttu-id="d1119-163">toorun scripts non signés, hello **ExecutionPolicy** doit être défini trop**Unrestricted**.</span><span class="sxs-lookup"><span data-stu-id="d1119-163">toorun unsigned scripts, hello **ExecutionPolicy** must be set too**Unrestricted**.</span></span> <span data-ttu-id="d1119-164">Hello **ExecutionPolicy** paramètre que vous utilisez selon hello version de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1119-164">hello **ExecutionPolicy** setting that you use is based on hello version of Windows PowerShell.</span></span>

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

<span data-ttu-id="d1119-165">Si vous utilisez un système d’exploitation invité qui s’exécute PowerShell 2.0 ou 1.0, vous pouvez forcer toorun de version 2 et dans le cas contraire, utilisez la version 1.</span><span class="sxs-lookup"><span data-stu-id="d1119-165">If you're using a Guest OS that is runs PowerShell 2.0 or 1.0 you can force version 2 toorun, and if unavailable, use version 1.</span></span>

```cmd
REM   Attempt tooset hello execution policy by using PowerShell version 2.0 syntax.
PowerShell -Version 2.0 -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If PowerShell version 2.0 isn't available. Set hello execution policy by using hello PowerShell
IF %ERRORLEVEL% EQU -393216 (
   PowerShell -Command "Set-ExecutionPolicy Unrestricted" >> "%TEMP%\StartupLog.txt" 2>&1
   PowerShell .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1
)

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="create-files-in-local-storage-from-a-startup-task"></a><span data-ttu-id="d1119-166">Créer des fichiers dans le stockage local à partir d’une tâche de démarrage</span><span class="sxs-lookup"><span data-stu-id="d1119-166">Create files in local storage from a startup task</span></span>
<span data-ttu-id="d1119-167">Vous pouvez utiliser un toostore de ressource de stockage local des fichiers créés par votre tâche de démarrage qui est accessible ultérieurement par votre application.</span><span class="sxs-lookup"><span data-stu-id="d1119-167">You can use a local storage resource toostore files created by your startup task that is accessed later by your application.</span></span>

<span data-ttu-id="d1119-168">toocreate hello ressource de stockage local, ajoutez un [LocalResources] section toohello [ServiceDefinition.csdef] de fichier, puis ajoutez hello [LocalStorage] élément enfant.</span><span class="sxs-lookup"><span data-stu-id="d1119-168">toocreate hello local storage resource, add a [LocalResources] section toohello [ServiceDefinition.csdef] file and then add hello [LocalStorage] child element.</span></span> <span data-ttu-id="d1119-169">Donnez la ressource de stockage local hello un nom unique et une taille appropriée pour votre tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d1119-169">Give hello local storage resource a unique name and an appropriate size for your startup task.</span></span>

<span data-ttu-id="d1119-170">toouse une ressource de stockage local dans votre tâche de démarrage, vous devez toocreate un emplacement de ressources de stockage local environnement tooreference variable hello.</span><span class="sxs-lookup"><span data-stu-id="d1119-170">toouse a local storage resource in your startup task, you need toocreate an environment variable tooreference hello local storage resource location.</span></span> <span data-ttu-id="d1119-171">Puis hello tâche de démarrage et d’application hello sont en mesure de tooread et écrire les ressources de stockage local des fichiers toohello.</span><span class="sxs-lookup"><span data-stu-id="d1119-171">Then hello startup task and hello application are able tooread and write files toohello local storage resource.</span></span>

<span data-ttu-id="d1119-172">Hello les sections pertinentes de hello **ServiceDefinition.csdef** fichier sont affichés ici :</span><span class="sxs-lookup"><span data-stu-id="d1119-172">hello relevant sections of hello **ServiceDefinition.csdef** file are shown here:</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">
    ...

    <LocalResources>
      <LocalStorage name="StartupLocalStorage" sizeInMB="5"/>
    </LocalResources>

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="PathToStartupStorage">
            <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
          </Variable>
        </Environment>
      </Task>
    </Startup>
  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="d1119-173">Par exemple, cela **Startup.cmd** fichier de commandes utilise hello **PathToStartupStorage** toocreate variable d’environnement le fichier hello **MyTest.txt** sur le stockage local de hello emplacement.</span><span class="sxs-lookup"><span data-stu-id="d1119-173">As an example, this **Startup.cmd** batch file uses hello **PathToStartupStorage** environment variable toocreate hello file **MyTest.txt** on hello local storage location.</span></span>

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

<span data-ttu-id="d1119-174">Vous pouvez accéder à des dossiers de stockage local de hello Azure SDK à l’aide de hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) (méthode).</span><span class="sxs-lookup"><span data-stu-id="d1119-174">You can access local storage folder from hello Azure SDK by using hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a><span data-ttu-id="d1119-175">Exécuter dans le cloud ou l’émulateur de Windows hello</span><span class="sxs-lookup"><span data-stu-id="d1119-175">Run in hello emulator or cloud</span></span>
<span data-ttu-id="d1119-176">Vous pouvez avoir votre tâche de démarrage effectue différentes étapes selon qu’elle s’exécute dans hello toowhen de cloud ou qu'il se trouve dans l’émulateur de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="d1119-176">You can have your startup task perform different steps when it is operating in hello cloud compared toowhen it is in hello compute emulator.</span></span> <span data-ttu-id="d1119-177">Par exemple, vous voudrez toouse une nouvelle copie de vos données SQL uniquement lors de l’exécution dans l’émulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="d1119-177">For example, you may want toouse a fresh copy of your SQL data only when running in hello emulator.</span></span> <span data-ttu-id="d1119-178">Ou vous pouvez toodo certaines optimisations des performances pour le cloud hello que vous n’avez pas besoin toodo lors de l’exécution dans l’émulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="d1119-178">Or you may want toodo some performance optimizations for hello cloud that you don't need toodo when running in hello emulator.</span></span>

<span data-ttu-id="d1119-179">Cette possibilité tooperform différente actions sur hello émulateur de calcul et de cloud de hello peut être effectuée en créant une variable d’environnement Bonjour [ServiceDefinition.csdef] fichier.</span><span class="sxs-lookup"><span data-stu-id="d1119-179">This ability tooperform different actions on hello compute emulator and hello cloud can be accomplished by creating an environment variable in hello [ServiceDefinition.csdef] file.</span></span> <span data-ttu-id="d1119-180">Vous testez ensuite une valeur de cette variable d’environnement dans votre tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d1119-180">You then test that environment variable for a value in your startup task.</span></span>

<span data-ttu-id="d1119-181">variable d’environnement toocreate hello, ajouter hello [Variable]/[RoleInstanceValue] élément et créez une valeur XPath de `/RoleEnvironment/Deployment/@emulated`.</span><span class="sxs-lookup"><span data-stu-id="d1119-181">toocreate hello environment variable, add hello [Variable]/[RoleInstanceValue] element and create an XPath value of `/RoleEnvironment/Deployment/@emulated`.</span></span> <span data-ttu-id="d1119-182">Hello valeur Hello **ComputeEmulatorRunning %** variable d’environnement est `true` lors de l’exécution sur l’émulateur de calcul hello, et `false` lors de l’exécution sur le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="d1119-182">hello value of hello **%ComputeEmulatorRunning%** environment variable is `true` when running on hello compute emulator, and `false` when running on hello cloud.</span></span>

```xml
<ServiceDefinition name="MyService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WorkerRole name="WorkerRole1">

    ...

    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>
          <Variable name="ComputeEmulatorRunning">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
          </Variable>
        </Environment>
      </Task>
    </Startup>

  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="d1119-183">tâche Hello peut désormais vérifier hello **ComputeEmulatorRunning %** différentes actions environnement tooperform variable basées sur l’exécution du rôle de hello Bonjour cloud ou hello émulateur.</span><span class="sxs-lookup"><span data-stu-id="d1119-183">hello task can now check hello **%ComputeEmulatorRunning%** environment variable tooperform different actions based on whether hello role is running in hello cloud or hello emulator.</span></span> <span data-ttu-id="d1119-184">Voici un script shell .cmd qui vérifie cette variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="d1119-184">Here is a .cmd shell script that checks for that environment variable.</span></span>

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a><span data-ttu-id="d1119-185">Détecter que la tâche a déjà été exécutée</span><span class="sxs-lookup"><span data-stu-id="d1119-185">Detect that your task has already run</span></span>
<span data-ttu-id="d1119-186">rôle de Hello peut recycler sans un redémarrage à l’origine de votre toorun de tâches de démarrage à nouveau.</span><span class="sxs-lookup"><span data-stu-id="d1119-186">hello role may recycle without a reboot causing your startup tasks toorun again.</span></span> <span data-ttu-id="d1119-187">Il n’existe aucun tooindicate indicateur qui une tâche a déjà été exécutée sur hello hébergeant des ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="d1119-187">There is no flag tooindicate that a task has already run on hello hosting VM.</span></span> <span data-ttu-id="d1119-188">Il est possible que certaines tâches s’exécutent plusieurs fois sans engendrer de problème.</span><span class="sxs-lookup"><span data-stu-id="d1119-188">You may have some tasks where it doesn't matter that they run multiple times.</span></span> <span data-ttu-id="d1119-189">Toutefois, vous pouvez exécuter dans une situation où vous devez tooprevent une tâche de s’exécuter plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="d1119-189">However, you may run into a situation where you need tooprevent a task from running more than once.</span></span>

<span data-ttu-id="d1119-190">Hello la plus simple façon toodetect une tâche a déjà été exécutée est toocreate un fichier Bonjour **%temp%** dossier lors de la tâche hello est réussie et examiner hello pour qu’il le début de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="d1119-190">hello simplest way toodetect that a task has already run is toocreate a file in hello **%TEMP%** folder when hello task is successful and look for it at hello start of hello task.</span></span> <span data-ttu-id="d1119-191">Voici un exemple de script shell cmd qui effectue cette opération.</span><span class="sxs-lookup"><span data-stu-id="d1119-191">Here is a sample cmd shell script that does that for you.</span></span>

```cmd
REM   If Task1_Success.txt exists, then Application 1 is already installed.
IF EXIST "%RoleRoot%\Task1_Success.txt" (
  ECHO Application 1 is already installed. Exiting. >> "%TEMP%\StartupLog.txt" 2>&1
  GOTO Finish
)

REM   Run your real exe task
ECHO Running XYZ >> "%TEMP%\StartupLog.txt" 2>&1
"%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (
  REM   hello application installed without error. Create a file tooindicate that hello task
  REM   does not need toobe run again.

  ECHO This line will create a file tooindicate that Application 1 installed correctly. > "%RoleRoot%\Task1_Success.txt"

) ELSE (
  REM   An error occurred. Log hello error and exit with hello error code.

  DATE /T >> "%TEMP%\StartupLog.txt" 2>&1
  TIME /T >> "%TEMP%\StartupLog.txt" 2>&1
  ECHO  An error occurred running task 1. Errorlevel = %ERRORLEVEL%. >> "%TEMP%\StartupLog.txt" 2>&1

  EXIT %ERRORLEVEL%
)

:Finish

REM   Exit normally.
EXIT /B 0
```

## <a name="task-best-practices"></a><span data-ttu-id="d1119-192">Meilleures pratiques pour les tâches</span><span class="sxs-lookup"><span data-stu-id="d1119-192">Task best practices</span></span>
<span data-ttu-id="d1119-193">Voici quelques meilleures pratiques à suivre quand vous configurez la tâche pour votre rôle web ou de travail.</span><span class="sxs-lookup"><span data-stu-id="d1119-193">Here are some best practices you should follow when configuring task for your web or worker role.</span></span>

### <a name="always-log-startup-activities"></a><span data-ttu-id="d1119-194">Toujours consigner les activités de démarrage</span><span class="sxs-lookup"><span data-stu-id="d1119-194">Always log startup activities</span></span>
<span data-ttu-id="d1119-195">Visual Studio ne fournit pas un toostep débogueur par le biais des fichiers de commandes, par conséquent, il est bon tooget autant de données sur l’opération hello des fichiers de commandes que possible.</span><span class="sxs-lookup"><span data-stu-id="d1119-195">Visual Studio does not provide a debugger toostep through batch files, so it's good tooget as much data on hello operation of batch files as possible.</span></span> <span data-ttu-id="d1119-196">Journalisation de sortie hello des fichiers de commandes, les deux **stdout** et **stderr**, peut vous fournir des informations importantes lors de la tentative de toodebug et corriger les fichiers de commandes.</span><span class="sxs-lookup"><span data-stu-id="d1119-196">Logging hello output of batch files, both **stdout** and **stderr**, can give you important information when trying toodebug and fix batch files.</span></span> <span data-ttu-id="d1119-197">toolog les deux **stdout** et **stderr** toohello StartupLog.txt fichier hello de tooby pointu hello active **%temp%** variable d’environnement, ajoutez le texte hello `>>  "%TEMP%\\StartupLog.txt" 2>&1`fin toohello spécifiques lignes que vous souhaitez toolog.</span><span class="sxs-lookup"><span data-stu-id="d1119-197">toolog both **stdout** and **stderr** toohello StartupLog.txt file in hello directory pointed tooby hello **%TEMP%** environment variable, add hello text `>>  "%TEMP%\\StartupLog.txt" 2>&1` toohello end of specific lines you want toolog.</span></span> <span data-ttu-id="d1119-198">Par exemple, tooexecute setup.exe Bonjour **% PathToApp1Install** active :</span><span class="sxs-lookup"><span data-stu-id="d1119-198">For example, tooexecute setup.exe in hello **%PathToApp1Install%** directory:</span></span>

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

<span data-ttu-id="d1119-199">toosimplify votre code xml, vous pouvez créer un wrapper *cmd* fichier qui appelle votre démarrage toutes les tâches en même temps que la journalisation et garantit chaque hello de partages-tâche enfant même variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="d1119-199">toosimplify your xml, you can create a wrapper *cmd* file that calls all of your startup tasks along with logging and ensures each child-task shares hello same environment variables.</span></span>

<span data-ttu-id="d1119-200">Il peut s’avérer agaçantes cependant toouse `>> "%TEMP%\StartupLog.txt" 2>&1` sur fin hello de chaque tâche de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d1119-200">You may find it annoying though toouse `>> "%TEMP%\StartupLog.txt" 2>&1` on hello end of each startup task.</span></span> <span data-ttu-id="d1119-201">Vous pouvez appliquer la journalisation des tâches en créant un wrapper qui gère la journalisation pour vous.</span><span class="sxs-lookup"><span data-stu-id="d1119-201">You can enforce task logging by creating a wrapper that handles logging for you.</span></span> <span data-ttu-id="d1119-202">Ce wrapper appelle hello lot réel fichier toorun.</span><span class="sxs-lookup"><span data-stu-id="d1119-202">This wrapper calls hello real batch file you want toorun.</span></span> <span data-ttu-id="d1119-203">Aucune sortie du fichier de commandes hello cible sera redirigé toohello *Startuplog.txt* fichier.</span><span class="sxs-lookup"><span data-stu-id="d1119-203">Any output from hello target batch file will be redirected toohello *Startuplog.txt* file.</span></span>

<span data-ttu-id="d1119-204">Bonjour à l’exemple suivant montre comment tooredirect tous de sortie à partir d’un fichier de commandes de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d1119-204">hello following example shows how tooredirect all output from a startup batch file.</span></span> <span data-ttu-id="d1119-205">Dans cet exemple, le fichier ServerDefinition.csdef de hello crée une tâche de démarrage qui appelle *logwrap.cmd*.</span><span class="sxs-lookup"><span data-stu-id="d1119-205">In this example, hello ServerDefinition.csdef file creates a startup task that calls *logwrap.cmd*.</span></span> <span data-ttu-id="d1119-206">*logwrap.cmd* appelle *Startup2.cmd*, redirigeant toute la sortie trop**%temp%\\StartupLog.txt**.</span><span class="sxs-lookup"><span data-stu-id="d1119-206">*logwrap.cmd* calls *Startup2.cmd*, redirecting all output too**%TEMP%\\StartupLog.txt**.</span></span>

<span data-ttu-id="d1119-207">ServiceDefinition.cmd :</span><span class="sxs-lookup"><span data-stu-id="d1119-207">ServiceDefinition.cmd:</span></span>

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

<span data-ttu-id="d1119-208">**logwrap.cmd :**</span><span class="sxs-lookup"><span data-stu-id="d1119-208">**logwrap.cmd:**</span></span>

```cmd
@ECHO OFF

REM   logwrap.cmd calls passed in batch file, redirecting all output toohello StartupLog.txt log file.

ECHO [%date% %time%] == START logwrap.cmd ============================================== >> "%TEMP%\StartupLog.txt" 2>&1
ECHO [%date% %time%] Running %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Call hello child command batch file, redirecting all output toohello StartupLog.txt log file.
START /B /WAIT %1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   Log hello completion of child command.
ECHO [%date% %time%] Done >> "%TEMP%\StartupLog.txt" 2>&1

IF %ERRORLEVEL% EQU 0 (

   REM   No errors occurred. Exit logwrap.cmd normally.
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B 0

) ELSE (

   REM   Log hello error.
   ECHO [%date% %time%] An error occurred. hello ERRORLEVEL = %ERRORLEVEL%.  >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO [%date% %time%] == END logwrap.cmd ================================================ >> "%TEMP%\StartupLog.txt" 2>&1
   ECHO.  >> "%TEMP%\StartupLog.txt" 2>&1
   EXIT /B %ERRORLEVEL%

)
```

<span data-ttu-id="d1119-209">**Startup2.cmd :**</span><span class="sxs-lookup"><span data-stu-id="d1119-209">**Startup2.cmd:**</span></span>

```cmd
@ECHO OFF

REM   This is hello batch file where hello startup steps should be performed. Because of the
REM   way Startup2.cmd was called, all commands and their outputs will be stored in the
REM   StartupLog.txt file in hello directory pointed tooby hello TEMP environment variable.

REM   If an error occurs, hello following command will pass hello ERRORLEVEL back toothe
REM   calling batch file.

ECHO [%date% %time%] Some log information about this task
ECHO [%date% %time%] Some more log information about this task

EXIT %ERRORLEVEL%
```

<span data-ttu-id="d1119-210">Exemple de sortie Bonjour **StartupLog.txt** fichier :</span><span class="sxs-lookup"><span data-stu-id="d1119-210">Sample output in hello **StartupLog.txt** file:</span></span>

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> <span data-ttu-id="d1119-211">Hello **StartupLog.txt** fichier se trouve dans hello *C:\Resources\temp\\{identificateur de rôle} \RoleTemp* dossier.</span><span class="sxs-lookup"><span data-stu-id="d1119-211">hello **StartupLog.txt** file is located in hello *C:\Resources\temp\\{role identifier}\RoleTemp* folder.</span></span>
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a><span data-ttu-id="d1119-212">Définir executionContext convenablement pour les tâches de démarrage</span><span class="sxs-lookup"><span data-stu-id="d1119-212">Set executionContext appropriately for startup tasks</span></span>
<span data-ttu-id="d1119-213">Définissez les privilèges convenablement pour la tâche de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="d1119-213">Set privileges appropriately for hello startup task.</span></span> <span data-ttu-id="d1119-214">Parfois les tâches de démarrage doivent s’exécuter avec des privilèges élevés même si le rôle de hello s’exécute avec des privilèges normaux.</span><span class="sxs-lookup"><span data-stu-id="d1119-214">Sometimes startup tasks must run with elevated privileges even though hello role runs with normal privileges.</span></span>

<span data-ttu-id="d1119-215">Hello [executionContext][tâche] attribut définit le niveau de privilège hello de tâche de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="d1119-215">hello [executionContext][Task] attribute sets hello privilege level of hello startup task.</span></span> <span data-ttu-id="d1119-216">À l’aide de `executionContext="limited"` signifie a de la tâche de démarrage hello hello même niveau de privilège en tant que rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="d1119-216">Using `executionContext="limited"` means hello startup task has hello same privilege level as hello role.</span></span> <span data-ttu-id="d1119-217">À l’aide de `executionContext="elevated"` signifie que la tâche de démarrage hello possède des privilèges d’administrateur, ce qui permet à démarrage de hello tâches tâche tooperform de l’administrateur sans donner des rôles de tooyour des privilèges administrateur.</span><span class="sxs-lookup"><span data-stu-id="d1119-217">Using `executionContext="elevated"` means hello startup task has administrator privileges, which allows hello startup task tooperform administrator tasks without giving administrator privileges tooyour role.</span></span>

<span data-ttu-id="d1119-218">Un exemple d’une tâche de démarrage qui requiert des privilèges élevés est une tâche de démarrage qui utilise **AppCmd.exe** tooconfigure IIS.</span><span class="sxs-lookup"><span data-stu-id="d1119-218">An example of a startup task that requires elevated privileges is a startup task that uses **AppCmd.exe** tooconfigure IIS.</span></span> <span data-ttu-id="d1119-219">**AppCmd.exe** nécessite `executionContext="elevated"`.</span><span class="sxs-lookup"><span data-stu-id="d1119-219">**AppCmd.exe** requires `executionContext="elevated"`.</span></span>

### <a name="use-hello-appropriate-tasktype"></a><span data-ttu-id="d1119-220">Utiliser le taskType approprié de hello</span><span class="sxs-lookup"><span data-stu-id="d1119-220">Use hello appropriate taskType</span></span>
<span data-ttu-id="d1119-221">Hello [taskType][tâche] attribut détermine la tâche de démarrage hello moyen hello est exécutée.</span><span class="sxs-lookup"><span data-stu-id="d1119-221">hello [taskType][Task] attribute determines hello way hello startup task is executed.</span></span> <span data-ttu-id="d1119-222">Trois valeurs sont possibles : **simple**, **background** et **foreground**.</span><span class="sxs-lookup"><span data-stu-id="d1119-222">There are three values: **simple**, **background**, and **foreground**.</span></span> <span data-ttu-id="d1119-223">Hello tâches en arrière-plan et de premier plan sont démarrées de façon asynchrone, et ensuite les tâches simples hello sont exécutées de façon synchrone un à la fois.</span><span class="sxs-lookup"><span data-stu-id="d1119-223">hello background and foreground tasks are started asynchronously, and then hello simple tasks are executed synchronously one at a time.</span></span>

<span data-ttu-id="d1119-224">Avec **simple** des tâches de démarrage, vous pouvez définir commande hello exécution des tâches de hello par ordre hello dans le hello les tâches sont répertoriées dans le fichier ServiceDefinition.csdef de hello.</span><span class="sxs-lookup"><span data-stu-id="d1119-224">With **simple** startup tasks, you can set hello order in which hello tasks run by hello order in which hello tasks are listed in hello ServiceDefinition.csdef file.</span></span> <span data-ttu-id="d1119-225">Si un **simple** la fin de tâche avec un zéro non-code de sortie, puis hello s’arrête de procédure de démarrage et hello rôle ne démarre pas.</span><span class="sxs-lookup"><span data-stu-id="d1119-225">If a **simple** task ends with a non-zero exit code, then hello startup procedure stops and hello role does not start.</span></span>

<span data-ttu-id="d1119-226">Hello la différence entre **arrière-plan** tâches de démarrage et **premier plan** est que les tâches de démarrage **premier plan** tâches conserver en permanence hello rôle jusqu'à ce que hello  **premier plan** de tâches se termine.</span><span class="sxs-lookup"><span data-stu-id="d1119-226">hello difference between **background** startup tasks and **foreground** startup tasks is that **foreground** tasks keep hello role running until hello **foreground** task ends.</span></span> <span data-ttu-id="d1119-227">Cela signifie également que si hello **premier plan** tâche se bloque ou se bloque, le rôle de hello recycle pas jusqu'à ce que hello **premier plan** tâche fermé.</span><span class="sxs-lookup"><span data-stu-id="d1119-227">This also means that if hello **foreground** task hangs or crashes, hello role will not recycle until hello **foreground** task is forced closed.</span></span> <span data-ttu-id="d1119-228">Pour cette raison, **arrière-plan** tâches sont recommandées pour les tâches de démarrage asynchrones sauf si vous avez besoin de cette fonctionnalité de hello **premier plan** tâche.</span><span class="sxs-lookup"><span data-stu-id="d1119-228">For this reason, **background** tasks are recommended for asynchronous startup tasks unless you need that feature of hello **foreground** task.</span></span>

### <a name="end-batch-files-with-exit-b-0"></a><span data-ttu-id="d1119-229">Terminer des fichiers de commandes par EXIT /B 0</span><span class="sxs-lookup"><span data-stu-id="d1119-229">End batch files with EXIT /B 0</span></span>
<span data-ttu-id="d1119-230">Hello rôle ne démarrera que si hello **errorlevel** de démarrage simples chaque tâche est égale à zéro.</span><span class="sxs-lookup"><span data-stu-id="d1119-230">hello role will only start if hello **errorlevel** from each of your simple startup task is zero.</span></span> <span data-ttu-id="d1119-231">Tous les programmes ne définissent hello **errorlevel** (code de sortie) correctement, par conséquent, un fichier de commandes hello doit se terminer par un `EXIT /B 0` si tous les éléments ont été correctement exécutées.</span><span class="sxs-lookup"><span data-stu-id="d1119-231">Not all programs set hello **errorlevel** (exit code) correctly, so hello batch file should end with an `EXIT /B 0` if everything ran correctly.</span></span>

<span data-ttu-id="d1119-232">Absence d’un `EXIT /B 0` hello fin d’un fichier de commandes de démarrage est une cause courante de rôles qui ne démarrent pas.</span><span class="sxs-lookup"><span data-stu-id="d1119-232">A missing `EXIT /B 0` at hello end of a startup batch file is a common cause of roles that do not start.</span></span>

> [!NOTE]
> <span data-ttu-id="d1119-233">J’ai remarqué ce lot imbriqué fichiers se bloquent parfois lors de l’utilisation de hello `/B` paramètre.</span><span class="sxs-lookup"><span data-stu-id="d1119-233">I've noticed that nested batch files sometimes hang when using hello `/B` parameter.</span></span> <span data-ttu-id="d1119-234">Vous souhaiterez peut-être toomake assurer que ce problème de blocage ne se produit pas si un autre fichier de commandes appelle votre fichier de commandes en cours, comme si vous utilisez hello [wrapper du journal](#always-log-startup-activities).</span><span class="sxs-lookup"><span data-stu-id="d1119-234">You may want toomake sure that this hang problem does not happen if another batch file calls your current batch file, like if you use hello [log wrapper](#always-log-startup-activities).</span></span> <span data-ttu-id="d1119-235">Vous pouvez omettre hello `/B` paramètre dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="d1119-235">You can omit hello `/B` parameter in this case.</span></span>
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a><span data-ttu-id="d1119-236">Attendez toorun des tâches de démarrage plusieurs fois</span><span class="sxs-lookup"><span data-stu-id="d1119-236">Expect startup tasks toorun more than once</span></span>
<span data-ttu-id="d1119-237">Tous les recyclages de rôle n’incluent pas un redémarrage, mais ils comprennent tous l’exécution de toutes les tâches de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d1119-237">Not all role recycles include a reboot, but all role recycles include running all startup tasks.</span></span> <span data-ttu-id="d1119-238">Cela signifie que les tâches de démarrage doivent être en mesure de toorun plusieurs fois entre les redémarrages sans aucun problème.</span><span class="sxs-lookup"><span data-stu-id="d1119-238">This means that startup tasks must be able toorun multiple times between reboots without any problems.</span></span> <span data-ttu-id="d1119-239">Ce sujet est abordé dans hello [précédant la section](#detect-that-your-task-has-already-run).</span><span class="sxs-lookup"><span data-stu-id="d1119-239">This is discussed in hello [preceding section](#detect-that-your-task-has-already-run).</span></span>

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a><span data-ttu-id="d1119-240">Utiliser des fichiers de toostore de stockage local qui doivent être accessibles par le rôle de hello</span><span class="sxs-lookup"><span data-stu-id="d1119-240">Use local storage toostore files that must be accessed in hello role</span></span>
<span data-ttu-id="d1119-241">Si vous souhaitez toocopy ou créez un fichier pendant votre tâche de démarrage qui est ensuite accessible tooyour rôle, ce fichier doit être placé dans le stockage local.</span><span class="sxs-lookup"><span data-stu-id="d1119-241">If you want toocopy or create a file during your startup task that is then accessible tooyour role, then that file must be placed in local storage.</span></span> <span data-ttu-id="d1119-242">Consultez hello [précédant la section](#create-files-in-local-storage-from-a-startup-task).</span><span class="sxs-lookup"><span data-stu-id="d1119-242">See hello [preceding section](#create-files-in-local-storage-from-a-startup-task).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1119-243">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d1119-243">Next steps</span></span>
<span data-ttu-id="d1119-244">Passez en revue les cloud hello [package et le modèle de service](cloud-services-model-and-package.md)</span><span class="sxs-lookup"><span data-stu-id="d1119-244">Review hello cloud [service model and package](cloud-services-model-and-package.md)</span></span>

<span data-ttu-id="d1119-245">En savoir plus sur le fonctionnement des [tâches](cloud-services-startup-tasks.md) .</span><span class="sxs-lookup"><span data-stu-id="d1119-245">Learn more about how [Tasks](cloud-services-startup-tasks.md) work.</span></span>

<span data-ttu-id="d1119-246">[Créez et déployez](cloud-services-how-to-create-deploy-portal.md) votre package de service cloud.</span><span class="sxs-lookup"><span data-stu-id="d1119-246">[Create and deploy](cloud-services-how-to-create-deploy-portal.md) your cloud service package.</span></span>

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[tâche]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[Startup]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[environnement]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
[Endpoints]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Endpoints
[LocalStorage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalStorage
[LocalResources]: https://msdn.microsoft.com/library/azure/gg557552.aspx#LocalResources
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
