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
# <a name="update-your-previous-java-service-fabric-application-toofetch-java-libraries-from-maven"></a>Mettre à jour de votre précédent Java Service Fabric application toofetch Java les bibliothèques à partir de Maven
Nous avons récemment déplacé des fichiers binaires du Service Fabric Java de hello Service Fabric Java SDK tooMaven hébergement. Vous pouvez désormais utiliser **mavencentral** dépendances de Service Fabric Java toofetch hello plus récente. Cela permet de démarrage rapide vous mettez à jour vos applications Java existantes, que vous avez créés précédemment toobe utilisé avec Service Fabric Java SDK, à l’aide de deux Yeoman modèle ou Eclipse, toobe compatible avec hello build Maven en fonction.

## <a name="prerequisites"></a>Composants requis
1. Vous devez tout d’abord toouninstall hello du Kit de développement Java existant.

  ```bash
  sudo dpkg -r servicefabricsdkjava
  ```
2. Installation hello plus tard Service Fabric CLI après hello étapes mentionnées [ici](service-fabric-cli.md).

3. toobuild et utiliser des applications de Service Fabric Java hello, vous devez tooensure que JDK 1.8 et Gradle sont installés. Si non encore installé, vous pouvez exécuter hello suivant tooinstall JDK 1.8 (openjdk-8-jdk) et Gradle -

 ```bash
 sudo apt-get install openjdk-8-jdk-headless
 sudo apt-get install gradle
 ```
4. Mise à jour hello installer ou désinstaller des scripts de votre application de toouse hello nouvelle CLI de l’infrastructure Service suit hello mentionné [ici](service-fabric-application-lifecycle-sfctl.md). Vous pouvez faire référence tooour mise en route [exemples](https://github.com/Azure-Samples/service-fabric-java-getting-started) pour référence.

>[!TIP]
> Après avoir désinstallé hello Service Fabric Java SDK, Yeoman ne fonctionnera pas. Suivez les conditions préalables de hello mentionnées [ici](service-fabric-create-your-first-linux-application-with-java.md) toohave Service Fabric Yeoman Java Générateur de modèle des et qu’elle fonctionne.

## <a name="service-fabric-java-libraries-on-maven"></a>Bibliothèques Java Service Fabric sur Maven
Les bibliothèques Java Service Fabric ont été hébergées dans Maven. Vous pouvez ajouter des dépendances de hello Bonjour ``pom.xml`` ou ``build.gradle`` de vos bibliothèques de Service Fabric Java toouse projets à partir de **mavenCentral**.

### <a name="actors"></a>Acteurs

Assistance Reliable Actor de Service Fabric pour votre application.

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

### <a name="services"></a>Services

Assistance des services sans état de Service Fabric pour votre application.

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

### <a name="others"></a>Autres
#### <a name="transport"></a>Transport

Assistance de la couche transport pour application Java Service Fabric. Vous n’avez pas besoin tooexplicitly ajouter cette dépendance tooyour Reliable Actor ou les applications de Service, sauf si vous effectuez la programmation au niveau de la couche de transport hello.

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

#### <a name="fabric-support"></a>Assista,ce Fabric

Support de niveau système pour l’infrastructure de Service qui communique avec le runtime du Service Fabric toonative. Vous n’avez pas besoin tooexplicitly ajouter cette dépendance tooyour Reliable Actor ou les applications de Service. Il obtient extraites automatiquement à partir de Maven, lorsque vous incluez hello autres dépendances ci-dessus.

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


## <a name="migrating-service-fabric-stateless-service"></a>Migration des services sans état Service Fabric

toobe toobuild en mesure de votre Service service Fabric existant sans état Java à l’aide des dépendances du Service Fabric extraites à partir de Maven, vous devez tooupdate hello ``build.gradle`` fichier hello Service. Il utilisait toobe comme comme suit :
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
Désormais, les dépendances de hello toofetch à partir de Maven, hello **mise à jour** ``build.gradle`` aurait les parties correspondantes hello comme suit :
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
En règle générale, tooget une idée générale sur la manière de créer des scripts hello ressemble à un service de Java l’infrastructure de Service sans état, reportez-vous tooany exemple à partir de nos exemples de prise en main. Voici hello [build.gradle](https://github.com/Azure-Samples/service-fabric-java-getting-started/blob/master/Services/EchoServer/EchoServer1.0/EchoServerService/build.gradle) pour hello EchoServer exemple.

## <a name="migrating-service-fabric-actor-service"></a>Migration du service d’acteur Service Fabric

toobe toobuild en mesure de votre application Java d’acteur Service Fabric existante, à l’aide des dépendances du Service Fabric extraites à partir de Maven, vous devez tooupdate hello ``build.gradle`` fichier à l’intérieur du package d’interface hello et dans le package de Service hello. Si vous avez un package TestClient, vous devez tooupdate autrement également. C’est le cas, pour votre acteur ``Myactor``, suivants de hello serait emplacements hello où vous avez besoin de tooupdate -
```
./Myactor/build.gradle
./MyactorInterface/build.gradle
./MyactorTestClient/build.gradle
```

#### <a name="updating-build-script-for-hello-interface-project"></a>Mise à jour du script de compilation pour le projet d’interface hello

Il utilisait toobe comme comme suit :
```
dependencies {
    compile fileTree(dir: '/opt/microsoft/sdk/servicefabric/java/packages/lib', include: ['*.jar'])
}
.
.
```
Désormais, les dépendances de hello toofetch à partir de Maven, hello **mise à jour** ``build.gradle`` aurait les parties correspondantes hello comme suit :
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

#### <a name="updating-build-script-for-hello-actor-project"></a>Mise à jour du script de compilation pour le projet d’acteur hello

Il utilisait toobe comme comme suit :
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
Désormais, les dépendances de hello toofetch à partir de Maven, hello **mise à jour** ``build.gradle`` aurait les parties correspondantes hello comme suit :
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

#### <a name="updating-build-script-for-hello-test-client-project"></a>Mise à jour le script de génération de projet de client de test hello

Modifications apportées ici sont des modifications similaires toohello décrites dans la section précédente, autrement dit, le projet d’acteur hello. Précédemment hello Gradle toobe de script utilisé comme comme suit :
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
Désormais, les dépendances de hello toofetch à partir de Maven, hello **mise à jour** ``build.gradle`` aurait les parties correspondantes hello comme suit :
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

## <a name="next-steps"></a>Étapes suivantes

* [Créer et déployer votre première application Java Service Fabric sous Linux à l’aide de Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Créer et déployer votre première application Java Service Fabric sous Linux à l’aide du plug-in Service Fabric pour Eclipse](service-fabric-get-started-eclipse.md)
* [Interagir avec des clusters Service Fabric à l’aide de hello CLI de l’infrastructure de Service](service-fabric-cli.md)
