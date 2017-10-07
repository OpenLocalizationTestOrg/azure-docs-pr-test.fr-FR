---
title: "aaaMigrate à partir du Kit de développement logiciel Java tooMaven - mettre à jour les anciennes Applications Java de Azure Service Fabric toouse Maven | Documents Microsoft"
description: "Mise à jour hello plus anciennes applications Java utilisé toouse hello du SDK du Service Fabric Java, toofetch les dépendances de Service Fabric Java à partir de Maven. Après avoir terminé cette installation, vos anciennes applications Java serait en mesure de toobuild."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 11b979facd7b3865141a6d3a035a6021dd06ca0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a><span data-ttu-id="ff619-104">Mettre à jour de votre précédent Java Service Fabric application toofetch Java les bibliothèques à partir de Maven</span><span class="sxs-lookup"><span data-stu-id="ff619-104">Update your previous Java Service Fabric application toofetch Java libraries from Maven</span></span>
<span data-ttu-id="ff619-105">Nous avons récemment déplacé des fichiers binaires du Service Fabric Java de hello Service Fabric Java SDK tooMaven hébergement.</span><span class="sxs-lookup"><span data-stu-id="ff619-105">We have recently moved Service Fabric Java binaries from hello Service Fabric Java SDK tooMaven hosting.</span></span> <span data-ttu-id="ff619-106">Vous pouvez désormais utiliser **mavencentral** dépendances de Service Fabric Java toofetch hello plus récente.</span><span class="sxs-lookup"><span data-stu-id="ff619-106">Now you can use **mavencentral** toofetch hello latest Service Fabric Java dependencies.</span></span> <span data-ttu-id="ff619-107">Cela permet de démarrage rapide vous mettez à jour vos applications Java existantes, que vous avez créés précédemment toobe utilisé avec Service Fabric Java SDK, à l’aide de deux Yeoman modèle ou Eclipse, toobe compatible avec hello build Maven en fonction.</span><span class="sxs-lookup"><span data-stu-id="ff619-107">This quick-start helps you update your existing Java applications, which you earlier created toobe used with Service Fabric Java SDK, using either Yeoman template or Eclipse, toobe compatible with hello Maven based build.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff619-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ff619-108">Prerequisites</span></span>
1. <span data-ttu-id="ff619-109">Vous devez tout d’abord toouninstall hello du Kit de développement Java existant.</span><span class="sxs-lookup"><span data-stu-id="ff619-109">First you need toouninstall hello existing Java SDK.</span></span>

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. <span data-ttu-id="ff619-110">Installation hello plus tard Service Fabric CLI après hello étapes mentionnées [ici](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ff619-110">Install hello latest Service Fabric CLI following hello steps mentioned [here](service-fabric-cli.md).</span></span>

3. <span data-ttu-id="ff619-111">toobuild et utiliser des applications de Service Fabric Java hello, vous devez tooensure que JDK 1.8 et Gradle sont installés.</span><span class="sxs-lookup"><span data-stu-id="ff619-111">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK 1.8 and Gradle installed.</span></span> <span data-ttu-id="ff619-112">Si non encore installé, vous pouvez exécuter hello suivant tooinstall JDK 1.8 (openjdk-8-jdk) et Gradle -</span><span class="sxs-lookup"><span data-stu-id="ff619-112">If not yet installed, you can run hello following tooinstall JDK 1.8 (openjdk-8-jdk) and Gradle -</span></span>

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. <span data-ttu-id="ff619-113">Mise à jour hello installer ou désinstaller des scripts de votre application de toouse hello nouvelle CLI de l’infrastructure Service suit hello mentionné [ici](service-fabric-application-lifecycle-sfctl.md).</span><span class="sxs-lookup"><span data-stu-id="ff619-113">Update hello install/uninstall scripts of your application toouse hello new Service Fabric CLI following hello steps mentioned [here](service-fabric-application-lifecycle-sfctl.md).</span></span> <span data-ttu-id="ff619-114">Vous pouvez faire référence tooour mise en route [exemples](https://github.com/Azure-Samples/service-fabric-java-getting-started) pour référence.</span><span class="sxs-lookup"><span data-stu-id="ff619-114">You can refer tooour getting-started [examples](https://github.com/Azure-Samples/service-fabric-java-getting-started) for reference.</span></span>

>[!TIP]
> <span data-ttu-id="ff619-115">Après avoir désinstallé hello Service Fabric Java SDK, Yeoman ne fonctionnera pas.</span><span class="sxs-lookup"><span data-stu-id="ff619-115">After uninstalling hello Service Fabric Java SDK, Yeoman will not work.</span></span> <span data-ttu-id="ff619-116">Suivez les conditions préalables de hello mentionnées [ici](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java Générateur de modèle des et qu’elle fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ff619-116">Follow hello Prerequisites mentioned [here](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java template generator up and working.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="ff619-117">Bibliothèques Java Service Fabric sur Maven</span><span class="sxs-lookup"><span data-stu-id="ff619-117">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="ff619-118">Les bibliothèques Java Service Fabric ont été hébergées dans Maven.</span><span class="sxs-lookup"><span data-stu-id="ff619-118">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="ff619-119">Vous pouvez ajouter des dépendances de hello Bonjour ``pom.xml`` ou ``build.gradle`` de vos bibliothèques de Service Fabric Java toouse projets à partir de **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="ff619-119">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="ff619-120">Acteurs</span><span class="sxs-lookup"><span data-stu-id="ff619-120">Actors</span></span>

<span data-ttu-id="ff619-121">Assistance Reliable Actor de Service Fabric pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ff619-121">Service Fabric Reliable Actor support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a><span data-ttu-id="ff619-122">Services</span><span class="sxs-lookup"><span data-stu-id="ff619-122">Services</span></span>

<span data-ttu-id="ff619-123">Assistance des services sans état de Service Fabric pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ff619-123">Service Fabric Stateless Service support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a><span data-ttu-id="ff619-124">Autres</span><span class="sxs-lookup"><span data-stu-id="ff619-124">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="ff619-125">Transport</span><span class="sxs-lookup"><span data-stu-id="ff619-125">Transport</span></span>

<span data-ttu-id="ff619-126">Assistance de la couche transport pour application Java Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ff619-126">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="ff619-127">Vous n’avez pas besoin tooexplicitly ajouter cette dépendance tooyour Reliable Actor ou les applications de Service, sauf si vous effectuez la programmation au niveau de la couche de transport hello.</span><span class="sxs-lookup"><span data-stu-id="ff619-127">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a><span data-ttu-id="ff619-128">Assista,ce Fabric</span><span class="sxs-lookup"><span data-stu-id="ff619-128">Fabric support</span></span>

<span data-ttu-id="ff619-129">Support de niveau système pour l’infrastructure de Service qui communique avec le runtime du Service Fabric toonative.</span><span class="sxs-lookup"><span data-stu-id="ff619-129">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="ff619-130">Vous n’avez pas besoin tooexplicitly ajouter cette dépendance tooyour Reliable Actor ou les applications de Service.</span><span class="sxs-lookup"><span data-stu-id="ff619-130">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="ff619-131">Il obtient extraites automatiquement à partir de Maven, lorsque vous incluez hello autres dépendances ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="ff619-131">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```


## <a name="migrating-service-fabric-stateless-service"></a><span data-ttu-id="ff619-132">Migration des services sans état Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ff619-132">Migrating Service Fabric Stateless Service</span></span>

<span data-ttu-id="ff619-133">toobe toobuild en mesure de votre Service service Fabric existant sans état Java à l’aide des dépendances du Service Fabric extraites à partir de Maven, vous devez tooupdate hello ``build.gradle`` fichier hello Service.</span><span class="sxs-lookup"><span data-stu-id="ff619-133">toobe able toobuild your existing Service Fabric stateless Java service using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello Service.</span></span> <span data-ttu-id="ff619-134">Il utilisait toobe comme comme suit :</span><span class="sxs-lookup"><span data-stu-id="ff619-134">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':Interface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
}
.
.
.
task copyDeps <<{
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('libj*.so')
    }
}
```
<span data-ttu-id="ff619-135">Désormais, les dépendances de hello toofetch à partir de Maven, hello **mise à jour** ``build.gradle`` aurait les parties correspondantes hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ff619-135">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
        mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':Interface')
    azuresf ('com.microsoft.servicefabric:sf-services-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'statelessservice.MyStatelessServiceHost',
                "Class-Path": mpath)
    baseName "MyStateless"
    destinationDir = file('./../MyStatelessApplication/MyStatelessPkg/Code')
   }
}
.
.
.
task copyDeps <<{
    copy {
        from("lib/")
        into("./../MyStatelessApplication/MyStatelessPkg/Code/lib")
        include('*')
    }
}
```
<span data-ttu-id="ff619-136">En règle générale, tooget une idée générale sur la manière de créer des scripts hello ressemble à un service de Java l’infrastructure de Service sans état, reportez-vous tooany exemple à partir de nos exemples de prise en main.</span><span class="sxs-lookup"><span data-stu-id="ff619-136">In general, tooget an overall idea about how hello build script would look like for a Service Fabric stateless Java service, you can refer tooany sample from our getting-started examples.</span></span> <span data-ttu-id="ff619-137">Voici hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) pour hello EchoServer exemple.</span><span class="sxs-lookup"><span data-stu-id="ff619-137">Here is hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) for hello EchoServer sample.</span></span>

## <a name="migrating-service-fabric-actor-service"></a><span data-ttu-id="ff619-138">Migration du service d’acteur Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ff619-138">Migrating Service Fabric Actor Service</span></span>

<span data-ttu-id="ff619-139">toobe toobuild en mesure de votre application Java d’acteur Service Fabric existante, à l’aide des dépendances du Service Fabric extraites à partir de Maven, vous devez tooupdate hello ``build.gradle`` fichier à l’intérieur du package d’interface hello et dans le package de Service hello.</span><span class="sxs-lookup"><span data-stu-id="ff619-139">toobe able toobuild your existing Service Fabric Actor Java application using Service Fabric dependencies fetched from Maven, you need tooupdate hello ``build.gradle`` file inside hello interface package and in hello Service package.</span></span> <span data-ttu-id="ff619-140">Si vous avez un package TestClient, vous devez tooupdate autrement également.</span><span class="sxs-lookup"><span data-stu-id="ff619-140">If you have a TestClient package, you need tooupdate that as well.</span></span> <span data-ttu-id="ff619-141">C’est le cas, pour votre acteur ``Myactor``, suivants de hello serait emplacements hello où vous avez besoin de tooupdate -</span><span class="sxs-lookup"><span data-stu-id="ff619-141">So, for your actor ``Myactor``, hello following would be hello places where you need tooupdate -</span></span>
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a><span data-ttu-id="ff619-142">Mise à jour du script de compilation pour le projet d’interface hello</span><span class="sxs-lookup"><span data-stu-id="ff619-142">Updating build script for hello interface project</span></span>

<span data-ttu-id="ff619-143">Il utilisait toobe comme comme suit :</span><span class="sxs-lookup"><span data-stu-id="ff619-143">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
<span data-ttu-id="ff619-144">Désormais, les dépendances de hello toofetch à partir de Maven, hello **mise à jour** ``build.gradle`` aurait les parties correspondantes hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ff619-144">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
```

#### <a name="updating-build-script-for-hello-actor-project"></a><span data-ttu-id="ff619-145">Mise à jour du script de compilation pour le projet d’acteur hello</span><span class="sxs-lookup"><span data-stu-id="ff619-145">Updating build script for hello actor project</span></span>

<span data-ttu-id="ff619-146">Il utilisait toobe comme comme suit :</span><span class="sxs-lookup"><span data-stu-id="ff619-146">Previously it used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
    compile project(':MyactorInterface')
}
.
.
.
jar {
    manifest {
    attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
      baseName "myactor"
    destinationDir = file('./../myjavaapp/MyactorPkg/Code')
    }
}
.
.
.
task copyDeps<< {
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
    copy {
        from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('libj*.so')
    }
    copy {
        from("../MyactorInterface/out/lib")
        into("./../myjavaapp/MyactorPkg/Code/lib")
        include('*.jar')
    }
}
```
<span data-ttu-id="ff619-147">Désormais, les dépendances de hello toofetch à partir de Maven, hello **mise à jour** ``build.gradle`` aurait les parties correspondantes hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ff619-147">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar {
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
        attributes(
                'Main-Class': 'reliableactor.MyactorHost',
                "Class-Path": mpath)
    baseName "myactor"
    destinationDir = file('../myjavaapp/MyactorPkg/Code')}
 }
.
.
.
task copyDeps<< {
      copy {
              from("lib/")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*')
      }
      copy {
              from("../MyactorInterface/out/lib")
              into("../myjavaapp/MyactorPkg/Code/lib")
              include('*.jar')
      }
}
```

#### <a name="updating-build-script-for-hello-test-client-project"></a><span data-ttu-id="ff619-148">Mise à jour le script de génération de projet de client de test hello</span><span class="sxs-lookup"><span data-stu-id="ff619-148">Updating build script for hello test client project</span></span>

<span data-ttu-id="ff619-149">Modifications apportées ici sont des modifications similaires toohello décrites dans la section précédente, autrement dit, le projet d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="ff619-149">Changes here are similar toohello changes discussed in previous section, that is, hello actor project.</span></span> <span data-ttu-id="ff619-150">Précédemment hello Gradle toobe de script utilisé comme comme suit :</span><span class="sxs-lookup"><span data-stu-id="ff619-150">Previously hello Gradle script used toobe like as follows -</span></span>
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
      compile project(':MyactorInterface')
}
.
.
.
jar
{
    manifest {
    attributes(
        'Main-Class': 'reliableactor.test.MyactorTestClient',
        "Class-Path": configurations.compile.collect { 'lib/' + it.getName() }.join(' '))
    }
    baseName "myactor-test"
  destinationDir = file('out/lib')
}
.
.
.
task copyDeps<< {
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
        copy {
                from("/opt/microsoft/sdk/servicefabric/java/packages/lib")
                into("./out/lib/lib")
                include('libj*.so')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```
<span data-ttu-id="ff619-151">Désormais, les dépendances de hello toofetch à partir de Maven, hello **mise à jour** ``build.gradle`` aurait les parties correspondantes hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ff619-151">Now, toofetch hello dependencies from Maven, hello **updated** ``build.gradle`` would have hello corresponding parts as follows -</span></span>
```
repositories {
    mavenCentral()
}

configurations {
    azuresf
}

dependencies {
    compile project(':MyactorInterface')
    azuresf ('com.microsoft.servicefabric:sf-actors-preview:0.10.0')
    compile fileTree(dir: 'lib', include: '*.jar')
}

task explodeDeps(type: Copy, dependsOn:configurations.azuresf) { task ->
    configurations.azuresf.filter { it.toString().contains("native-preview") }.each{
        from zipTree(it)
    }
    configurations.azuresf.filter { !it.toString().contains("native-preview") }.each {
        from it
    }
    into "lib"
    include "libj*.so", "*.jar"
}

compileJava.dependsOn(explodeDeps)
.
.
.
jar
{
    manifest {
        def mpath = configurations.compile.collect {'lib/'+it.getName()}.join (' ')
        mpath = mpath + ' ' + configurations.azuresf.collect {'lib/'+it.getName()}.join (' ')
    attributes(
                'Main-Class': 'reliableactor.test.MyactorTestClient',
                "Class-Path": mpath)
    baseName "myactor-test"
    destinationDir = file('./out/lib')
        }
}
.
.
.
task copyDeps<< {
        copy {
                from("lib/")
                into("./out/lib/lib")
                include('*')
        }
        copy {
                from("../MyactorInterface/out/lib")
                into("./out/lib/lib")
                include('*.jar')
        }
}
```

## <a name="next-steps"></a><span data-ttu-id="ff619-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ff619-152">Next steps</span></span>

* [<span data-ttu-id="ff619-153">Créer et déployer votre première application Java Service Fabric sous Linux à l’aide de Yeoman</span><span class="sxs-lookup"><span data-stu-id="ff619-153">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="ff619-154">Créer et déployer votre première application Java Service Fabric sous Linux à l’aide du plug-in Service Fabric pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="ff619-154">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="ff619-155">Interagir avec des clusters Service Fabric à l’aide de hello CLI de l’infrastructure de Service</span><span class="sxs-lookup"><span data-stu-id="ff619-155">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
