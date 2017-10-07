---
title: "aaaRun des tâches de démarrage dans les Services de cloud computing Azure | Documents Microsoft"
description: "Les tâches de démarrage facilitent la préparation de votre environnement de service cloud pour votre application. Il vous apprend comment démarrage des tâches et toomake les"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 886939be-4b5b-49cc-9a6e-2172e3c133e9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 3391a5d7434164f59972b8e497e5c34e33409543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-and-run-startup-tasks-for-a-cloud-service"></a>Des tâches de démarrage tooconfigure et exécution d’un service cloud
Vous pouvez utiliser les opérations de tooperform de tâches de démarrage avant le démarrage d’un rôle. Les opérations que vous pourriez tooperform incluent l’installation d’un composant, l’inscription des composants COM, définition de clés de Registre ou à partir d’un processus à long terme.

> [!NOTE]
> Tâches de démarrage ne sont pas applicables tooVirtual Machines, tooCloud Service Web et les rôles de travail.
> 
> 

## <a name="how-startup-tasks-work"></a>Fonctionnement des tâches de démarrage
Tâches de démarrage sont des actions qui sont effectuées avant que vos rôles commencent et sont définis dans hello [ServiceDefinition.csdef] fichier à l’aide de hello [tâche] élément hello [démarrage]élément. Souvent les tâches de démarrage sont des fichiers de commandes, mais elles peuvent également être des applications console ou des fichiers de commandes qui démarrent des scripts PowerShell.

Variables d’environnement passent des informations dans une tâche de démarrage et le stockage local peut être informations toopass utilisé en dehors d’une tâche de démarrage. Par exemple, une variable d’environnement peut spécifier programme de tooa hello chemin d’accès souhaité tooinstall et les fichiers peuvent être écrites de stockage toolocal qui peut être lu ultérieurement par vos rôles.

Votre tâche de démarrage peut enregistrer des informations et répertoire de toohello d’erreurs spécifié par hello **TEMP** variable d’environnement. Au cours de la tâche de démarrage hello, hello **TEMP** variable d’environnement résout toohello *C:\\ressources\\temp\\[guid]. [ rolename]\\RoleTemp* active lors de l’exécution sur le cloud de hello.

Les tâches de démarrage peuvent également être exécutées plusieurs fois entre des redémarrages. Par exemple, tâche de démarrage hello s’exécutera chaque fois hello rôle est recyclé, et les recyclages de rôle n’incluent pas toujours un redémarrage. Tâches de démarrage doivent être écrites d’une manière qui leur permet de toorun plusieurs fois sans problème.

Tâches de démarrage doivent se terminer par un **errorlevel** (ou code de sortie) de zéro pour toocomplete de processus de démarrage hello. Si une tâche de démarrage se termine par un zéro **errorlevel**, rôle de hello ne démarrera pas.

## <a name="role-startup-order"></a>Ordre de démarrage des rôles
Hello suivant la procédure de démarrage de rôle listes hello dans Azure :

1. Hello instance est marquée comme **départ** et ne reçoit pas de trafic.
2. Toutes les tâches de démarrage sont exécutées selon tootheir **taskType** attribut.
   
   * Hello **simple** les tâches sont exécutées de façon synchrone, une à la fois.
   * Hello **arrière-plan** et **premier plan** tâches sont des tâches de démarrage toohello démarré de façon asynchrone et parallèle.  
     
     > [!WARNING]
     > IIS peut être pas complètement configuré pendant l’étape de tâche de démarrage hello dans le processus de démarrage hello, les données spécifiques à un rôle peut ne pas être disponibles. Les tâches de démarrage qui ont besoin de données spécifiques au rôle doivent utiliser [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx).
     > 
     > 
3. processus hôte de rôle Hello est démarré et le site de hello est créé dans IIS.
4. Hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) méthode est appelée.
5. Hello instance est marquée comme **prêt** et le trafic est routé toohello instance.
6. Hello [Microsoft.WindowsAzure.ServiceRuntime.RoleEntryPoint.Run](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) méthode est appelée.

## <a name="example-of-a-startup-task"></a>Exemple d’une tâche de démarrage
Tâches de démarrage sont définies dans hello [ServiceDefinition.csdef] fichier, Bonjour **tâche** élément. Hello **commandLine** attribut spécifie le nom de hello et paramètres des commandes de démarrage hello de fichiers ou de la console de commande, hello **executionContext** attribut spécifie le niveau de privilège hello du démarrage de hello tâche et hello **taskType** attribut spécifie comment hello tâche sera exécutée.

Dans cet exemple, une variable d’environnement **MyVersionNumber**, est créé pour la tâche de démarrage hello et toohello la valeur «**1.0.0.0**».

**ServiceDefinition.csdef**:

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
        <Environment>
            <Variable name="MyVersionNumber" value="1.0.0.0" />
        </Environment>
    </Task>
</Startup>
```

Dans l’exemple suivant de hello, hello **Startup.cmd** fichier de commandes écrit, « la version actuelle de hello est 1.0.0.0 » de fichier de StartupLog.txt toohello, ligne de hello dans le répertoire hello spécifié par la variable d’environnement TEMP hello. Hello `EXIT /B 0` ligne garantit que cette tâche de démarrage hello se termine par un **errorlevel** égale à zéro.

```cmd
ECHO hello current version is %MyVersionNumber% >> "%TEMP%\StartupLog.txt" 2>&1
EXIT /B 0
```

> [!NOTE]
> Dans Visual Studio, hello **copier tooOutput active** propriété pour votre fichier de commandes de démarrage doit être définie trop**toujours copier** toobe assurer que votre fichier de commandes de démarrage est correctement déployé le projet tooyour sur Azure (**approot\\bin** pour les rôles Web, et **approot** pour les rôles de travail).
> 
> 

## <a name="description-of-task-attributes"></a>Description des attributs de tâche
Hello suivante décrit les attributs hello Hello **tâche** élément Bonjour [ServiceDefinition.csdef] fichier :

**ligne de commande** -spécifie la ligne de commande hello pour la tâche de démarrage hello :

* Hello commande avec des paramètres de ligne de commande facultatifs, qui commence la tâche de démarrage hello.
* Il s’agit souvent hello de nom de fichier d’un fichier de commandes .cmd ou .bat.
* tâche Hello est relatif toohello AppRoot\\dossier Bin pour le déploiement de hello. Variables d’environnement ne sont pas développées dans la détermination hello chemin d’accès et de la tâche hello. Si ce développement est nécessaire, vous pouvez créer un petit script .cmd qui appelle votre tâche de démarrage.
* Il peut s’agir d’une application console ou d’un fichier de commande qui démarre un [script PowerShell](cloud-services-startup-tasks-common.md#create-a-powershell-startup-task).

**executionContext** -Spécifie le niveau de privilège hello pour la tâche de démarrage hello. niveau de privilège Hello peut être limité ou élevé :

* **limited**  
  tâche de démarrage Hello s’exécute avec hello mêmes privilèges en tant que rôle de hello. Hello lorsque **executionContext** attribut pour hello [Runtime] élément est également **limité**, puis les privilèges utilisateur sont utilisés.
* **elevated**  
  tâche de démarrage Hello s’exécute avec des privilèges d’administrateur. Ainsi, les tâches de démarrage tooinstall programmes, apporter des modifications de configuration IIS, effectuer des modifications du Registre et autres tâches d’administration, sans augmenter le niveau de privilège hello du rôle hello lui-même.  

> [!NOTE]
> Hello niveau de privilège d’une tâche de démarrage n’a pas besoin toobe même hello en tant que rôle hello lui-même.
> 
> 

**taskType** -spécifie hello façon une tâche de démarrage est exécutée.

* **simple**  
  Les tâches sont exécutées de façon synchrone, une à la fois, dans l’ordre de hello spécifié dans hello [ServiceDefinition.csdef] fichier. Lorsqu’un **simple** tâche de démarrage se termine par un **errorlevel** de zéro, hello ensuite **simple** tâche de démarrage est exécutée. S’il n’y a plus aucun **simple** tooexecute, les tâches de démarrage puis démarrera rôle hello lui-même.   
  
  > [!NOTE]
  > Si hello **simple** tâche se termine par un zéro **errorlevel**, hello instance sera bloquée. Ultérieures **simple** tâches de démarrage et rôle hello lui-même, ne démarrent pas.
  > 
  > 
  
    tooensure votre fichier de commandes se termine par un **errorlevel** égal à zéro, exécutez la commande hello `EXIT /B 0` à fin hello de votre processus de fichier de traitement par lots.
* **background**  
  Tâches sont exécutées de façon asynchrone, en parallèle avec démarrage hello du rôle de hello.
* **foreground**  
  Tâches sont exécutées de façon asynchrone, en parallèle avec démarrage hello du rôle de hello. Hello la principale différence entre un **premier plan** et un **arrière-plan** est que la tâche un **premier plan** tâche empêche le rôle hello de recyclage ou l’arrêt jusqu'à ce que la tâche hello a s’est terminée. Hello **arrière-plan** tâches ne disposent pas de cette restriction.

## <a name="environment-variables"></a>Variables d’environnement
Variables d’environnement sont une tâche de démarrage de façon toopass informations tooa. Par exemple, vous pouvez placer hello chemin d’accès tooa blob qui contient un programme tooinstall, ou les numéros de port qui utilise votre rôle ou toocontrol les fonctionnalités des paramètres de votre tâche de démarrage.

Il existe deux types de variables d’environnement pour les tâches de démarrage ; variables d’environnement statiques et les variables d’environnement basée sur les membres de hello [ RoleEnvironment] classe. Les deux sont Bonjour [environnement] section Hello [ServiceDefinition.csdef] de fichiers et les deux hello utilisation [ Variable] élément et **nom** attribut.

Hello d’utilise les variables statiques environnement **valeur** attribut Hello [ Variable] élément. exemple Hello ci-dessus crée la variable d’environnement hello **MyVersionNumber** avec une valeur statique de «**1.0.0.0**». Un autre exemple consisterait à toocreate un **StagingOrProduction** variable d’environnement que vous pouvez définir manuellement toovalues de «**intermédiaire**« ou »**production**» tooperform les actions de démarrage différentes en fonction de la valeur hello hello **StagingOrProduction** variable d’environnement.

Variables d’environnement basées sur les membres de hello classe RoleEnvironment n’utilisent pas hello **valeur** attribut Hello [ Variable] élément. Au lieu de cela, hello [RoleInstanceValue] élément enfant, avec hello approprié **XPath** valeur d’attribut, est toocreate utilisé une variable d’environnement basée sur un membre spécifique de hello [ RoleEnvironment] classe. Valeurs pour hello **XPath** tooaccess d’attributs différentes [ RoleEnvironment] les valeurs se trouvent [ici](cloud-services-role-config-xpath.md).

Par exemple, toocreate une variable d’environnement qui est «**true**» lors de l’instance de hello est en cours d’exécution dans l’émulateur de calcul hello, et «**false**» lors de l’exécution dans le cloud de hello, utilisez des éléments suivants de hello [ Variable] et [RoleInstanceValue] éléments :

```xml
<Startup>
    <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple">
        <Environment>

            <!-- Create hello environment variable that informs hello startup task whether it is running
                in hello Compute Emulator or in hello cloud. "%ComputeEmulatorRunning%"=="true" when
                running in hello Compute Emulator, "%ComputeEmulatorRunning%"=="false" when running
                in hello cloud. -->

            <Variable name="ComputeEmulatorRunning">
                <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated" />
            </Variable>

        </Environment>
    </Task>
</Startup>
```

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment tooperform certains [tâches courantes de démarrage](cloud-services-startup-tasks-common.md) avec votre Service Cloud.

[Créez un package](cloud-services-model-and-package.md) de votre service cloud.  

[ServiceDefinition.csdef]: cloud-services-model-and-package.md#csdef
[tâche]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Task
[démarrage]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Startup
[Runtime]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Runtime
[environnement]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Environment
[ Variable]: https://msdn.microsoft.com/library/azure/gg557552.aspx#Variable
[RoleInstanceValue]: https://msdn.microsoft.com/library/azure/gg557552.aspx#RoleInstanceValue
[ RoleEnvironment]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx
