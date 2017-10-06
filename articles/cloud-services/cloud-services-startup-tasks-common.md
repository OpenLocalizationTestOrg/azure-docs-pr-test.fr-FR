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
# <a name="common-cloud-service-startup-tasks"></a>Tâches courantes de démarrage dans le service cloud
Cet article fournit des exemples de tâches courantes de démarrage peut souhaité tooperform dans votre service cloud. Vous pouvez utiliser les opérations de tooperform de tâches de démarrage avant le démarrage d’un rôle. Les opérations que vous pourriez tooperform incluent l’installation d’un composant, l’inscription des composants COM, définition de clés de Registre ou à partir d’un processus à long terme. 

Consultez [cet article](cloud-services-startup-tasks.md) toounderstand comment fonctionnent les tâches de démarrage et en particulier comment toocreate hello entrées qui définissent une tâche de démarrage.

> [!NOTE]
> Tâches de démarrage ne sont pas applicables tooVirtual Machines, tooCloud Service Web et les rôles de travail.
> 

## <a name="define-environment-variables-before-a-role-starts"></a>Définir des variables d’environnement avant le démarrage d’un rôle
Si vous avez besoin de variables d’environnement définies pour une tâche spécifique, utilisez hello [environnement] élément à l’intérieur de hello [tâche] élément.

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

Les variables peuvent également utiliser un [valeur Azure XPath valide](cloud-services-role-config-xpath.md) tooreference quelque chose sur le déploiement de hello. Au lieu d’utiliser hello `value` d’attribut, de définir un [RoleInstanceValue] élément enfant.

```xml
<Variable name="PathToStartupStorage">
    <RoleInstanceValue xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='StartupLocalStorage']/@path" />
</Variable>
```


## <a name="configure-iis-startup-with-appcmdexe"></a>Configurer le démarrage d’IIS avec AppCmd.exe
Hello [AppCmd.exe](https://technet.microsoft.com/library/jj635852.aspx) outil de ligne de commande peut être utilisé toomanage les paramètres IIS au démarrage sur Azure. *AppCmd.exe* fournit des paramètres de tooconfiguration d’un accès pratique de ligne de commande pour une utilisation dans les tâches de démarrage sur Azure. *AppCmd.exe*permet d’ajouter, de modifier ou de supprimer des paramètres de site web pour les applications et les sites.

Toutefois, il existe quelques toowatch de choses out pour utilisation hello de *AppCmd.exe* comme une tâche de démarrage :

* Les tâches de démarrage peuvent être exécutées plusieurs fois entre les redémarrages. Par exemple, lorsqu’un rôle est recyclé.
* Si une action *AppCmd.exe* est exécutée plusieurs fois, cela peut générer une erreur. Par exemple, essayer de trop tooadd une section*Web.config* deux fois la peut générer une erreur.
* Les tâches de démarrage échouent si elles retournent un code de sortie non nul ou **errorlevel**. Par exemple, lorsque *AppCmd.exe* génère une erreur.

Il s’agit d’une salutation toocheck de bonnes pratiques **errorlevel** après avoir appelé *AppCmd.exe*, qui est toodo facile si vous encapsulez les appels hello trop*AppCmd.exe* avec un *.cmd*  fichier. Si vous détectez une réponse **errorlevel** connue, vous pouvez l’ignorer, ou bien la retransmettre.

Hello errorlevel retournée par *AppCmd.exe* sont répertoriées dans le fichier winerror.h de hello et peuvent également être consultés sur [MSDN](https://msdn.microsoft.com/library/windows/desktop/ms681382.aspx).

### <a name="example-of-managing-hello-error-level"></a>Exemple de gestion de niveau d’erreur hello
Cet exemple ajoute une section de compression et une entrée de compression pour JSON toohello *Web.config* fichier, avec la gestion des erreurs et enregistrement.

Hello les sections pertinentes de hello [ServiceDefinition.csdef] fichier sont indiqués ici, qui incluent le paramètre hello [executionContext](https://msdn.microsoft.com/library/azure/gg557552.aspx#Task) trop d’attributs`elevated` toogive *AppCmd.exe*  suffisamment toochange hello les paramètres d’autorisation Bonjour *Web.config* fichier :

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

Hello *Startup.cmd* par lots de fichiers utilise *AppCmd.exe* tooadd une section de compression et une entrée de compression pour JSON toohello *Web.config* fichier. Hello attendu **errorlevel** 183 a la valeur toozero à l’aide de hello vérifier. Programme de ligne de commande du fichier EXE. Les errorlevels inattendus sont tooStartupErrorLog.txt connecté.

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

## <a name="add-firewall-rules"></a>Ajouter des règles de pare-feu
Dans Azure, il existe en fait deux pare-feu. Hello premier pare-feu contrôle les connexions entre des VM hello et hello world à l’extérieur. Ce pare-feu est contrôlé par hello [points de terminaison] élément Bonjour [ServiceDefinition.csdef] fichier.

Hello deuxième pare-feu contrôle les connexions entre ordinateur virtuel de hello et processus hello au sein de cet ordinateur virtuel. Ce pare-feu peut être contrôlé par hello `netsh advfirewall firewall` outil de ligne de commande.

Azure crée des règles de pare-feu pour les processus de hello démarrés au sein de vos rôles. Par exemple, lorsque vous démarrez un service ou un programme, Azure crée automatiquement tooallow de règles de pare-feu nécessaires hello toocommunicate de ce service par hello Internet. Toutefois, si vous créez un service qui est démarré par un processus en dehors de votre rôle (comme un service COM + ou une tâche planifiée Windows), vous devez toomanually créer un service de pare-feu règle tooallow accès toothat. Ces règles de pare-feu peuvent être créées à l’aide d’une tâche de démarrage.

Une tâche de démarrage qui crée une règle de pare-feu doit avoir [executionContext][tâche] défini sur **elevated**. Ajouter hello suivant toohello de tâche de démarrage [ServiceDefinition.csdef] fichier.

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

règle de pare-feu de hello tooadd, vous devez utiliser hello approprié `netsh advfirewall firewall` commandes dans votre fichier de commandes de démarrage. Dans cet exemple, la tâche de démarrage de hello nécessite de chiffrement et sécurité pour le port TCP 80.

```cmd
REM   Add a firewall rule in a startup task.

REM   Add an inbound rule requiring security and encryption for TCP port 80 traffic.
netsh advfirewall firewall add rule name="Require Encryption for Inbound TCP/80" protocol=TCP dir=in localport=80 security=authdynenc action=allow >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

## <a name="block-a-specific-ip-address"></a>Bloquer une adresse IP spécifique
Vous pouvez limiter un ensemble de tooa d’accès de rôle web Azure d’adresses IP spécifiques en modifiant votre IIS **web.config** fichier. Vous devez également toouse un fichier de commandes qui déverrouille hello **IPSec** section Hello **ApplicationHost.config** fichier.

toodo déverrouiller hello **IPSec** section Hello **ApplicationHost.config** de fichiers, créez un fichier de commandes qui s’exécute au démarrage de rôle. Créez un dossier au niveau de votre rôle web appelé racine de hello **démarrage** et, dans ce dossier, créez un fichier de commandes appelé **startup.cmd**. Ajouter ce fichier de projet de Visual Studio tooyour et définir les propriétés de hello trop**toujours copier** tooensure qu’il est inclus dans votre package.

Ajouter hello suivant toohello de tâche de démarrage [ServiceDefinition.csdef] fichier.

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

Ajoutez cette commande toohello **startup.cmd** fichier :

```cmd
@echo off
@echo Installing "IPv4 Address and Domain Restrictions" feature 
powershell -ExecutionPolicy Unrestricted -command "Install-WindowsFeature Web-IP-Security"
@echo Unlocking configuration for "IPv4 Address and Domain Restrictions" feature 
%windir%\system32\inetsrv\AppCmd.exe unlock config -section:system.webServer/security/ipSecurity
```

Cette tâche, Bonjour **startup.cmd** toobe de fichier exécute chaque fois que rôle web de hello est initialisé, garantissant que hello requis du lot **IPSec** section est déverrouillée.

Enfin, modifiez hello [section system.webServer](http://www.iis.net/configreference/system.webserver/security/ipsecurity#005) de votre rôle web **web.config** fichier tooadd une liste d’adresses IP qui ont accès, comme indiqué dans hello l’exemple suivant :

Cet exemple de configuration **permet** toutes les adresses IP tooaccess hello serveur sauf hello deux définies

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

Cet exemple de configuration **refuse** toutes les adresses IP d’accéder au serveur hello à l’exception de hello deux défini.

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

## <a name="create-a-powershell-startup-task"></a>Créer une tâche de démarrage PowerShell
Les scripts Windows PowerShell ne peut pas être appelées directement à partir de hello [ServiceDefinition.csdef] fichier, mais ils peuvent être appelés à partir d’un fichier de commandes de démarrage.

PowerShell (par défaut) n’exécute pas de scripts non signés. Sauf si vous vous connectez à votre script, vous devez tooconfigure PowerShell toorun les scripts non signés. toorun scripts non signés, hello **ExecutionPolicy** doit être défini trop**Unrestricted**. Hello **ExecutionPolicy** paramètre que vous utilisez selon hello version de Windows PowerShell.

```cmd
REM   Run an unsigned PowerShell script and log hello output
PowerShell -ExecutionPolicy Unrestricted .\startup.ps1 >> "%TEMP%\StartupLog.txt" 2>&1

REM   If an error occurred, return hello errorlevel.
EXIT /B %errorlevel%
```

Si vous utilisez un système d’exploitation invité qui s’exécute PowerShell 2.0 ou 1.0, vous pouvez forcer toorun de version 2 et dans le cas contraire, utilisez la version 1.

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

## <a name="create-files-in-local-storage-from-a-startup-task"></a>Créer des fichiers dans le stockage local à partir d’une tâche de démarrage
Vous pouvez utiliser un toostore de ressource de stockage local des fichiers créés par votre tâche de démarrage qui est accessible ultérieurement par votre application.

toocreate hello ressource de stockage local, ajoutez un [LocalResources] section toohello [ServiceDefinition.csdef] de fichier, puis ajoutez hello [LocalStorage] élément enfant. Donnez la ressource de stockage local hello un nom unique et une taille appropriée pour votre tâche de démarrage.

toouse une ressource de stockage local dans votre tâche de démarrage, vous devez toocreate un emplacement de ressources de stockage local environnement tooreference variable hello. Puis hello tâche de démarrage et d’application hello sont en mesure de tooread et écrire les ressources de stockage local des fichiers toohello.

Hello les sections pertinentes de hello **ServiceDefinition.csdef** fichier sont affichés ici :

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

Par exemple, cela **Startup.cmd** fichier de commandes utilise hello **PathToStartupStorage** toocreate variable d’environnement le fichier hello **MyTest.txt** sur le stockage local de hello emplacement.

```cmd
REM   Create a simple text file.

ECHO This text will go into hello MyTest.txt file which will be in hello    >  "%PathToStartupStorage%\MyTest.txt"
ECHO path pointed tooby hello PathToStartupStorage environment variable.  >> "%PathToStartupStorage%\MyTest.txt"
ECHO hello contents of hello PathToStartupStorage environment variable is   >> "%PathToStartupStorage%\MyTest.txt"
ECHO "%PathToStartupStorage%".                                          >> "%PathToStartupStorage%\MyTest.txt"

REM   Exit hello batch file with ERRORLEVEL 0.

EXIT /b 0
```

Vous pouvez accéder à des dossiers de stockage local de hello Azure SDK à l’aide de hello [GetLocalResource](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) (méthode).

```csharp
string localStoragePath = Microsoft.WindowsAzure.ServiceRuntime.RoleEnvironment.GetLocalResource("StartupLocalStorage").RootPath;

string fileContent = System.IO.File.ReadAllText(System.IO.Path.Combine(localStoragePath, "MyTestFile.txt"));
```

## <a name="run-in-hello-emulator-or-cloud"></a>Exécuter dans le cloud ou l’émulateur de Windows hello
Vous pouvez avoir votre tâche de démarrage effectue différentes étapes selon qu’elle s’exécute dans hello toowhen de cloud ou qu'il se trouve dans l’émulateur de calcul hello. Par exemple, vous voudrez toouse une nouvelle copie de vos données SQL uniquement lors de l’exécution dans l’émulateur de hello. Ou vous pouvez toodo certaines optimisations des performances pour le cloud hello que vous n’avez pas besoin toodo lors de l’exécution dans l’émulateur de hello.

Cette possibilité tooperform différente actions sur hello émulateur de calcul et de cloud de hello peut être effectuée en créant une variable d’environnement Bonjour [ServiceDefinition.csdef] fichier. Vous testez ensuite une valeur de cette variable d’environnement dans votre tâche de démarrage.

variable d’environnement toocreate hello, ajouter hello [Variable]/[RoleInstanceValue] élément et créez une valeur XPath de `/RoleEnvironment/Deployment/@emulated`. Hello valeur Hello **ComputeEmulatorRunning %** variable d’environnement est `true` lors de l’exécution sur l’émulateur de calcul hello, et `false` lors de l’exécution sur le cloud de hello.

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

tâche Hello peut désormais vérifier hello **ComputeEmulatorRunning %** différentes actions environnement tooperform variable basées sur l’exécution du rôle de hello Bonjour cloud ou hello émulateur. Voici un script shell .cmd qui vérifie cette variable d’environnement.

```cmd
REM   Check if this task is running on hello compute emulator.

IF "%ComputeEmulatorRunning%" == "true" (
    REM   This task is running on hello compute emulator. Perform tasks that must be run only in hello compute emulator.
) ELSE (
    REM   This task is running on hello cloud. Perform tasks that must be run only in hello cloud.
)
```


## <a name="detect-that-your-task-has-already-run"></a>Détecter que la tâche a déjà été exécutée
rôle de Hello peut recycler sans un redémarrage à l’origine de votre toorun de tâches de démarrage à nouveau. Il n’existe aucun tooindicate indicateur qui une tâche a déjà été exécutée sur hello hébergeant des ordinateurs virtuels. Il est possible que certaines tâches s’exécutent plusieurs fois sans engendrer de problème. Toutefois, vous pouvez exécuter dans une situation où vous devez tooprevent une tâche de s’exécuter plusieurs fois.

Hello la plus simple façon toodetect une tâche a déjà été exécutée est toocreate un fichier Bonjour **%temp%** dossier lors de la tâche hello est réussie et examiner hello pour qu’il le début de la tâche hello. Voici un exemple de script shell cmd qui effectue cette opération.

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

## <a name="task-best-practices"></a>Meilleures pratiques pour les tâches
Voici quelques meilleures pratiques à suivre quand vous configurez la tâche pour votre rôle web ou de travail.

### <a name="always-log-startup-activities"></a>Toujours consigner les activités de démarrage
Visual Studio ne fournit pas un toostep débogueur par le biais des fichiers de commandes, par conséquent, il est bon tooget autant de données sur l’opération hello des fichiers de commandes que possible. Journalisation de sortie hello des fichiers de commandes, les deux **stdout** et **stderr**, peut vous fournir des informations importantes lors de la tentative de toodebug et corriger les fichiers de commandes. toolog les deux **stdout** et **stderr** toohello StartupLog.txt fichier hello de tooby pointu hello active **%temp%** variable d’environnement, ajoutez le texte hello `>>  "%TEMP%\\StartupLog.txt" 2>&1`fin toohello spécifiques lignes que vous souhaitez toolog. Par exemple, tooexecute setup.exe Bonjour **% PathToApp1Install** active :

    "%PathToApp1Install%\setup.exe" >> "%TEMP%\StartupLog.txt" 2>&1

toosimplify votre code xml, vous pouvez créer un wrapper *cmd* fichier qui appelle votre démarrage toutes les tâches en même temps que la journalisation et garantit chaque hello de partages-tâche enfant même variables d’environnement.

Il peut s’avérer agaçantes cependant toouse `>> "%TEMP%\StartupLog.txt" 2>&1` sur fin hello de chaque tâche de démarrage. Vous pouvez appliquer la journalisation des tâches en créant un wrapper qui gère la journalisation pour vous. Ce wrapper appelle hello lot réel fichier toorun. Aucune sortie du fichier de commandes hello cible sera redirigé toohello *Startuplog.txt* fichier.

Bonjour à l’exemple suivant montre comment tooredirect tous de sortie à partir d’un fichier de commandes de démarrage. Dans cet exemple, le fichier ServerDefinition.csdef de hello crée une tâche de démarrage qui appelle *logwrap.cmd*. *logwrap.cmd* appelle *Startup2.cmd*, redirigeant toute la sortie trop**%temp%\\StartupLog.txt**.

ServiceDefinition.cmd :

```xml
<Startup>
    <Task commandLine="logwrap.cmd startup2.cmd" executionContext="limited" taskType="simple" />
</Startup>
```

**logwrap.cmd :**

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

**Startup2.cmd :**

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

Exemple de sortie Bonjour **StartupLog.txt** fichier :

```txt
[Mon 10/17/2016 20:24:46.75] == START logwrap.cmd ============================================== 
[Mon 10/17/2016 20:24:46.75] Running command1.cmd 
[Mon 10/17/2016 20:24:46.77] Some log information about this task
[Mon 10/17/2016 20:24:46.77] Some more log information about this task
[Mon 10/17/2016 20:24:46.77] Done 
[Mon 10/17/2016 20:24:46.77] == END logwrap.cmd ================================================ 
```

> [!TIP]
> Hello **StartupLog.txt** fichier se trouve dans hello *C:\Resources\temp\\{identificateur de rôle} \RoleTemp* dossier.
> 
> 

### <a name="set-executioncontext-appropriately-for-startup-tasks"></a>Définir executionContext convenablement pour les tâches de démarrage
Définissez les privilèges convenablement pour la tâche de démarrage hello. Parfois les tâches de démarrage doivent s’exécuter avec des privilèges élevés même si le rôle de hello s’exécute avec des privilèges normaux.

Hello [executionContext][tâche] attribut définit le niveau de privilège hello de tâche de démarrage hello. À l’aide de `executionContext="limited"` signifie a de la tâche de démarrage hello hello même niveau de privilège en tant que rôle de hello. À l’aide de `executionContext="elevated"` signifie que la tâche de démarrage hello possède des privilèges d’administrateur, ce qui permet à démarrage de hello tâches tâche tooperform de l’administrateur sans donner des rôles de tooyour des privilèges administrateur.

Un exemple d’une tâche de démarrage qui requiert des privilèges élevés est une tâche de démarrage qui utilise **AppCmd.exe** tooconfigure IIS. **AppCmd.exe** nécessite `executionContext="elevated"`.

### <a name="use-hello-appropriate-tasktype"></a>Utiliser le taskType approprié de hello
Hello [taskType][tâche] attribut détermine la tâche de démarrage hello moyen hello est exécutée. Trois valeurs sont possibles : **simple**, **background** et **foreground**. Hello tâches en arrière-plan et de premier plan sont démarrées de façon asynchrone, et ensuite les tâches simples hello sont exécutées de façon synchrone un à la fois.

Avec **simple** des tâches de démarrage, vous pouvez définir commande hello exécution des tâches de hello par ordre hello dans le hello les tâches sont répertoriées dans le fichier ServiceDefinition.csdef de hello. Si un **simple** la fin de tâche avec un zéro non-code de sortie, puis hello s’arrête de procédure de démarrage et hello rôle ne démarre pas.

Hello la différence entre **arrière-plan** tâches de démarrage et **premier plan** est que les tâches de démarrage **premier plan** tâches conserver en permanence hello rôle jusqu'à ce que hello  **premier plan** de tâches se termine. Cela signifie également que si hello **premier plan** tâche se bloque ou se bloque, le rôle de hello recycle pas jusqu'à ce que hello **premier plan** tâche fermé. Pour cette raison, **arrière-plan** tâches sont recommandées pour les tâches de démarrage asynchrones sauf si vous avez besoin de cette fonctionnalité de hello **premier plan** tâche.

### <a name="end-batch-files-with-exit-b-0"></a>Terminer des fichiers de commandes par EXIT /B 0
Hello rôle ne démarrera que si hello **errorlevel** de démarrage simples chaque tâche est égale à zéro. Tous les programmes ne définissent hello **errorlevel** (code de sortie) correctement, par conséquent, un fichier de commandes hello doit se terminer par un `EXIT /B 0` si tous les éléments ont été correctement exécutées.

Absence d’un `EXIT /B 0` hello fin d’un fichier de commandes de démarrage est une cause courante de rôles qui ne démarrent pas.

> [!NOTE]
> J’ai remarqué ce lot imbriqué fichiers se bloquent parfois lors de l’utilisation de hello `/B` paramètre. Vous souhaiterez peut-être toomake assurer que ce problème de blocage ne se produit pas si un autre fichier de commandes appelle votre fichier de commandes en cours, comme si vous utilisez hello [wrapper du journal](#always-log-startup-activities). Vous pouvez omettre hello `/B` paramètre dans ce cas.
> 
> 

### <a name="expect-startup-tasks-toorun-more-than-once"></a>Attendez toorun des tâches de démarrage plusieurs fois
Tous les recyclages de rôle n’incluent pas un redémarrage, mais ils comprennent tous l’exécution de toutes les tâches de démarrage. Cela signifie que les tâches de démarrage doivent être en mesure de toorun plusieurs fois entre les redémarrages sans aucun problème. Ce sujet est abordé dans hello [précédant la section](#detect-that-your-task-has-already-run).

### <a name="use-local-storage-toostore-files-that-must-be-accessed-in-hello-role"></a>Utiliser des fichiers de toostore de stockage local qui doivent être accessibles par le rôle de hello
Si vous souhaitez toocopy ou créez un fichier pendant votre tâche de démarrage qui est ensuite accessible tooyour rôle, ce fichier doit être placé dans le stockage local. Consultez hello [précédant la section](#create-files-in-local-storage-from-a-startup-task).

## <a name="next-steps"></a>Étapes suivantes
Passez en revue les cloud hello [package et le modèle de service](cloud-services-model-and-package.md)

En savoir plus sur le fonctionnement des [tâches](cloud-services-startup-tasks.md) .

[Créez et déployez](cloud-services-how-to-create-deploy-portal.md) votre package de service cloud.

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
