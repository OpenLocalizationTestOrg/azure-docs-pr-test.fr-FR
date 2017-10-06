---
title: "aaaConnect un appareil à l’aide de C sur Windows | Documents Microsoft"
description: "Décrit comment tooconnect un toohello appareil Azure IoT Suite préconfiguré solution d’analyse à distance à l’aide d’une application écrite en C s’exécutant sous Windows."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a>Se connecter à votre solution préconfigurée (Windows) de surveillance à distance de toohello périphérique
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a>Création d’un exemple de solution C sur Windows
Hello suit vous montre comment toocreate une application cliente qui communique avec le contrôle à distance hello solution préconfigurée. Cette application est écrite en C, générée et exécutée sur Windows.

Créer un projet de démarrage dans Visual Studio 2015 ou Visual Studio 2017 et ajouter les packages NuGet hello IoT Hub périphérique client :

1. Dans Visual Studio, créez une application de console C à l’aide de Visual C++ de hello **Application Console Win32** modèle. Projet de hello nom **RMDevice**.
2. Sur hello **paramètres de l’Application** page Bonjour **Assistant Application Win32**, vérifiez que **application Console** est sélectionné, puis décochez la case **précompilé en-tête** et **du cycle de vie de développement de sécurité (SDL) vérifie**.
3. Dans **l’Explorateur de solutions**, supprimer hello fichiers stdafx.h, targetver.h et stdafx.cpp.
4. Dans **l’Explorateur de solutions**, renommez hello fichier RMDevice.cpp tooRMDevice.c.
5. Dans **l’Explorateur de solutions**, avec le bouton droit sur hello **RMDevice** de projet, puis cliquez sur **gérer les packages NuGet**. Cliquez sur **Parcourir**, puis recherchez et installez hello suivant les packages NuGet :
   
   * Microsoft.Azure.IoTHub.Serializer
   * Microsoft.Azure.IoTHub.IoTHubClient
   * Microsoft.Azure.IoTHub.MqttTransport
6. Dans **l’Explorateur de solutions**, avec le bouton droit sur hello **RMDevice** de projet, puis cliquez sur **propriétés** du projet tooopen hello **Pages de propriétés**boîte de dialogue. Pour plus d’informations, consultez [Setting Visual C++ Project Properties (Définition des propriétés de projet Visual C++)][lnk-c-project-properties]. 
7. Cliquez sur hello **l’éditeur de liens** dossier, puis cliquez sur hello **entrée** page de propriétés.
8. Ajouter **crypt32.lib** toohello **dépendances supplémentaires** propriété. Cliquez sur **OK** , puis **OK** à nouveau les valeurs de propriété du projet toosave hello.

Ajouter hello Parson JSON bibliothèque toohello **RMDevice** de projet et ajouter hello requis `#include` instructions :

1. Dans un dossier approprié sur votre ordinateur, cloner le référentiel de Parson GitHub hello à l’aide de hello de commande suivante :

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. Copiez les fichiers parson.h et parson.c hello copie locale hello hello Parson référentiel tooyour **RMDevice** dossier du projet.

1. Dans Visual Studio, avec le bouton droit hello **RMDevice** de projet, cliquez sur **ajouter**, puis cliquez sur **élément existant**.

1. Bonjour **ajouter un élément existant** boîte de dialogue, sélectionnez hello parson.h et parson.c les fichiers de hello **RMDevice** dossier du projet. Puis cliquez sur **ajouter** tooadd ces projets tooyour de deux fichiers.

1. Dans Visual Studio, ouvrez le fichier de RMDevice.c hello. Remplacer hello `#include` instructions avec hello suivant de code :
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > Vous pouvez maintenant vérifier que votre projet comporte les dépendances appropriées hello en créer.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Générer et exécuter l’exemple hello

Ajouter hello tooinvoke de code **distant\_analyse\_exécuter** fonction puis générer et exécuter l’application d’appareil hello.

1. Remplacez hello **principal** fonction avec hello de tooinvoke de code suivant **distant\_analyse\_exécuter** fonction :
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Cliquez sur **générer** , puis **générer la Solution** application d’appareil toobuild hello.

1. Dans **l’Explorateur de solutions**, avec le bouton hello **RMDevice** de projet, cliquez sur **déboguer**, puis cliquez sur **démarrer une nouvelle instance** toorun hello exemple. console de Hello affiche les messages hello application envoie exemple télémétrie toohello solution préconfigurée, reçoit les valeurs de propriétés souhaitées définies dans le tableau de bord de solution hello et répond toomethods appelée à partir du tableau de bord de solution hello.

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
