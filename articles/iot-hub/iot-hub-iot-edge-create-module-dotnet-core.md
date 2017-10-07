---
title: aaaCreate un Module de bord Azure IoT avec c# | Documents Microsoft
description: "Ce didacticiel montre comment un ver données convertisseur module à l’aide de toowrite hello derniers packages NuGet de bord Azure IoT, Code de Visual Studio et c#."
services: iot-hub
author: jeffreyCline
manager: timlt
keywords: azure, iot, didacticiel, module, nuget, vscode, csharp, edge
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: jcline
ms.openlocfilehash: b104609c05d1613e21acc7d7bed547f311179151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a>Créer un module Azure IoT Edge avec C&#x23;

Ce didacticiel présente comment toocreate un module pour `Azure IoT Edge` à l’aide de `Visual Studio Code` et `C#`.

Dans ce didacticiel, nous suivons la configuration de l’environnement et comment toowrite un [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) module de convertisseur de données à l’aide de hello dernières `Azure IoT Edge NuGet` packages. 

>[!NOTE]
Ce didacticiel utilise hello `.NET Core SDK`, qui prend en charge une compatibilité multiplateforme. Hello didacticiel suivant est écrit à l’aide de hello `Windows 10` système d’exploitation. Certaines des commandes hello dans ce didacticiel peuvent être différent selon votre `development environment`. 

## <a name="prerequisites"></a>Composants requis

Dans cette section, vous configurez votre environnement pour le développement du module `Azure IoT Edge`. Il s’applique tooboth **Windows 64 bits** et **64 bits Linux (8 Ubuntu/Debian)** systèmes d’exploitation.

Hello suivant logicielle est requise :

- [Client Git](https://git-scm.com/downloads).
- [Kit de développement logiciel (SDK) principal NET](https://www.microsoft.com/net/core#windowscmd)
- [Visual Studio Code](https://code.visualstudio.com/)

Vous n’avez pas besoin de référentiel de hello tooclone pour cet exemple, toutefois hello tous les exemples de code présenté dans ce didacticiel se trouve dans hello suivant du référentiel :

- `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a>Prise en main

1. Installez `.NET Core SDK`.
2. Installer `Visual Studio Code` et hello `C# extension` à partir de Visual Studio Code Marketplace de hello.

Afficher ce [rapide didacticiel vidéo](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) sur la façon dont tooget route à l’aide de `Visual Studio Code` et hello `.NET Core SDK`.

## <a name="creating-hello-azure-iot-edge-converter-module"></a>Création de module de conversion hello Azure IoT Edge

1. Initialisez un nouveau projet C# de bibliothèque de classes `.NET Core` :
    - Ouvrez une invite de commandes (`Windows + R` -> `cmd` -> `enter`).
    - Exploration du dossier toohello où vous aimeriez toocreate hello `C#` projet.
    - Tapez **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**. 
    - Cette commande crée une classe vide appelée `Class1.cs` dans votre répertoire de projets.
2. Exploration du dossier toohello où nous venons de créer le projet de bibliothèque de classes hello en tapant **cd IoTEdgeConverterModule**.
3. Projet ouvert hello dans `Visual Studio Code` en tapant **code.**.
4. Une fois le projet de hello est ouvert dans `Visual Studio Code`, cliquez sur hello **IoTEdgeConverterModule.csproj** fichier de hello tooopen comme indiqué dans hello suivant image :

    ![Fenêtre de modification - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. Insérer hello `XML` blob illustré hello suivant extrait de code entre la fermeture de hello `PropertyGroup` de balise et hello fermeture `Project` balise ; six Bonjour précédant l’image de ligne et enregistrer le fichier de hello en appuyant sur `Ctrl`  +  `S`.

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. Une fois que vous enregistrez hello `.csproj` fichier `Visual Studio Code` vous invite à entrer avec un `unresolved dependencies` boîte de dialogue comme dans hello suivant image : 

    ![Boîte de dialogue pour restaurer des dépendances de restauration - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    un) cliquez sur `Restore` toorestore tous hello fait référence dans les projets hello `.csproj` fichier, y compris hello `PackageReferences` , nous avons ajouté. 

    (b) `Visual Studio Code` crée automatiquement hello `project.assets.json` fichier dans vos projets `obj` dossier. Ce fichier contient des informations à propos dépendances toomake les restaurations suivantes de votre projet plus rapides.
 
    >[!NOTE]
    `.NET Core Tools` sont désormais basés sur MSBuild. Ce qui signifie qu’un fichier de projet `.csproj` est créé à la place d’un `project.json`.

    - Si `Visual Studio Code` n’affiche aucune invite vous indiquant que tout fonctionne normalement, nous pouvons le faire manuellement. Ouvrez hello `Visual Studio Code` intégrée fenêtre de terminal en appuyant sur les hello `Ctrl`  +  `backtick` clés ou à l’aide des menus de hello `View`  ->  `Integrated Terminal`.
    - Bonjour `Integrated Terminal` type de fenêtre **dotnet restauration**.
    
7. Renommer hello `Class1.cs` trop de fichiers`BleConverterModule.cs`. 

    a) fichier de hello toorename tout d’abord sur hello fichier appuyez sur hello `F2` clé.
    
    b) type dans le nouveau nom de hello **BleConverterModule**, comme dans hello suivant image :

    ![Renommer une classe - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. Remplacer le code existant dans hello hello `BleConverterModule.cs` fichier en copiant et hello collage suivante extrait de code dans votre `BleConverterModule.cs` fichier.

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Globalization;
   using System.Linq;
   using System.Text;
   using System.Threading;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace IoTEdgeConverterModule
   {
       public class BleConverterModule : IGatewayModule, IGatewayModuleStart
       {
           private Broker broker;
           private string configuration;
           private int messageCount;

           public void Create(Broker broker, byte[] configuration)
           {
               this.broker = broker;
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Start()
           {
           }

           public void Destroy()
           {
           }

           public void Receive(Message received_message)
           {
               string recMsg = Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               BleData receivedData = JsonConvert.DeserializeObject<BleData>(recMsg);

               float temperature = float.Parse(receivedData.Temperature, CultureInfo.InvariantCulture.NumberFormat); 
               Dictionary<string, string> receivedProperties = received_message.Properties;
            
               Dictionary<string, string> properties = new Dictionary<string, string>();
               properties.Add("source", receivedProperties["source"]);
               properties.Add("macAddress", receivedProperties["macAddress"]);
               properties.Add("temperatureAlert", temperature > 30 ? "true" : "false");
   
               String content = String.Format("{0} \"deviceId\": \"Intel NUC Gateway\", \"messageId\": {1}, \"temperature\": {2} {3}", "{", ++this.messageCount, temperature, "}");
               Message messageToPublish = new Message(content, properties);
   
               this.broker.Publish(messageToPublish);
           }
       }
   }
   ```

9. Enregistrez le fichier de hello en appuyant sur `Ctrl`  +  `S`.

10. Créer un nouveau fichier appelé `Untitled-1` en appuyant sur les hello `Ctrl`  +  `N` clés comme Bonjour suivant image :

    ![Nouveau fichier - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. toodeserialize hello `JSON` objet que nous recevons de hello simulée `BLE` de périphérique, hello copie suivante de code dans hello `Untitled-1` fenêtre d’éditeur de code de fichier. 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace IoTEdgeConverterModule
   {
       public class BleData
       {
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

12. Enregistrer le fichier hello sous `BleData.cs` en appuyant sur `Ctrl`  +  `Shift`  +  `S` clés.
    - Sur hello enregistrer en tant que la boîte de dialogue hello `Save as Type` menu déroulant, sélectionnez `C# (*.cs;*.csx)` comme Bonjour suivant image :

    ![Boîte de dialogue pour enregistrer sous - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. Créer un nouveau fichier appelé `Untitled-1` en appuyant sur les hello `Ctrl`  +  `N` clés.

14. Copiez et collez hello suivant extrait de code dans hello `Untitled-1` fichier. Cette classe est un `Azure IoT Edge` module, que nous utilisons les données de hello toooutput reçues à partir de notre `BleConverterModule`.

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;
   using System.Threading.Tasks;
   using Microsoft.Azure.Devices.Gateway;
   using Newtonsoft.Json;
   
   namespace PrinterModule
   {
       public class DotNetPrinterModule : IGatewayModule
       {
           private string configuration;
           public void Create(Broker broker, byte[] configuration)
           {
               this.configuration = System.Text.Encoding.UTF8.GetString(configuration);
           }
   
           public void Destroy()
           {
           }
   
           public void Receive(Message received_message)
           {
               string recMsg = System.Text.Encoding.UTF8.GetString(received_message.Content, 0, received_message.Content.Length);
               Dictionary<string, string> receivedProperties = received_message.Properties;
               
               BleConverterData receivedData = JsonConvert.DeserializeObject<BleConverterData>(recMsg);
   
               Console.WriteLine();
               Console.WriteLine("Module           : [DotNetPrinterModule]");
               Console.WriteLine("received_message : {0}", recMsg);
   
               if(received_message.Properties["source"] == "bleTelemetry")
               {
                   Console.WriteLine("Source           : {0}", receivedProperties["source"]);
                   Console.WriteLine("MAC address      : {0}", receivedProperties["macAddress"]);
                   Console.WriteLine("Temperature Alert: {0}", receivedProperties["temperatureAlert"]);
                   Console.WriteLine("Deserialized Obj : [BleConverterData]");
                   Console.WriteLine("  DeviceId       : {0}", receivedData.DeviceId);
                   Console.WriteLine("  MessageId      : {0}", receivedData.MessageId);
                   Console.WriteLine("  Temperature    : {0}", receivedData.Temperature);
               }
   
               Console.WriteLine();
           }
       }
   }
   ```

15. Enregistrer le fichier hello sous `DotNetPrinterModule.cs` en appuyant sur `Ctrl`  +  `Shift`  +  `S`.
    - Sur hello enregistrer en tant que la boîte de dialogue hello `Save as Type` menu déroulant, sélectionnez `C# (*.cs;*.csx)`.

16. Créer un nouveau fichier appelé `Untitled-1` en appuyant sur les hello `Ctrl`  +  `N` clés.

17. toodeserialize hello `JSON` objet que nous recevons de hello `BleConverterModule`, copie et suit hello de coller extrait de code hello `Untitled-1` fichier. 

   ```csharp
   using System;
   using Newtonsoft.Json;

   namespace PrinterModule
   {
       public class BleConverterData
       {
           [JsonProperty(PropertyName = "deviceId")]
           public string DeviceId { get; set; }
   
           [JsonProperty(PropertyName = "messageId")]
           public string MessageId { get; set; }
   
           [JsonProperty(PropertyName = "temperature")]
           public string Temperature { get; set; }
       }
   }
   ```

18. Enregistrer le fichier hello sous `BleConverterData.cs` en appuyant sur `Ctrl`  +  `Shift`  +  `S`.
    - Sur hello enregistrer en tant que la boîte de dialogue hello `Save as Type` menu déroulant, sélectionnez `C# (*.cs;*.csx)`.

19. Créer un nouveau fichier appelé `Untitled-1` en appuyant sur les hello `Ctrl`  +  `N` clés.

20. Copiez et collez hello suivant extrait de code dans hello `Untitled-1` fichier.

   ```json
   {
       "loaders": [
           {
               "type": "dotnetcore",
               "name": "dotnetcore",
               "configuration": {
                   "binding.path": "dotnetcore.dll",
                   "binding.coreclrpath": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\coreclr.dll",
                   "binding.trustedplatformassemblieslocation": "C:\\Program Files\\dotnet\\shared\\Microsoft.NETCore.App\\1.1.1\\"
               }
           }
       ],
          "modules": [
           {
               "name": "simulated_device",
               "loader": {
                   "name": "native",
                   "entrypoint": {
                       "module.path": "simulated_device.dll"
                   }
               },
               "args": {
                   "macAddress": "01:02:03:03:02:01",
                   "messagePeriod": 500
               }
           },
           {
               "name": "ble_converter_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "IoTEdgeConverterModule.BleConverterModule"
                   }
               },
               "args": ""
           },
           {
               "name": "printer_module",
               "loader": {
                   "name": "dotnetcore",
                   "entrypoint": {
                       "assembly.name": "IoTEdgeConverterModule",
                       "entry.type": "PrinterModule.DotNetPrinterModule"
                   }
               },
               "args": ""
           }
       ],
       "links": [
           {
               "source": "simulated_device", "sink": "ble_converter_module"
           },
           {
               "source": "ble_converter_module", "sink": "printer_module"
           }
   ]
   }
   ```

21. Enregistrer le fichier hello sous `gw-config.json` en appuyant sur `Ctrl`  +  `Shift`  +  `S`.
    - Sur hello enregistrer en tant que la boîte de dialogue hello `Save as Type` menu déroulant, sélectionnez `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.

22. répertoire, hello de mise à jour de sortie de copie de tooenable de toohello de fichier de configuration hello `IoTEdgeConverterModule.csproj` avec hello suivant l’objet blob XML :

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - mise à jour de Hello `IoTEdgeConverterModule.csproj` doit ressemble hello suivant image :

    ![Fichier .csproj mis à jour - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. Créer un nouveau fichier appelé `Untitled-1` en appuyant sur les hello `Ctrl`  +  `N` clés.

24. Copiez et collez hello suivant extrait de code dans hello `Untitled-1` fichier.

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. Enregistrer le fichier hello sous `binplace.ps1` en appuyant sur `Ctrl`  +  `Shift`  +  `S`.
    - Sur hello enregistrer en tant que la boîte de dialogue hello `Save as Type` menu déroulant, sélectionnez `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.

26. Générer le projet de hello en appuyant sur les hello `Ctrl`  +  `Shift`  +  `B` clés. Lorsque vous générez des projets hello pour hello première fois, `Visual Studio Code` vous invite à hello `No build task defined.` boîte de dialogue comme dans hello suivant image :

    ![Boîte de dialogue de tâche de génération - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    un) cliquez sur hello `Configure Build Task` bouton.

    (b) dans hello `Select a Task Runner` menu déroulant de la boîte de dialogue. Sélectionnez `.NET Core` comme Bonjour suivant image : 

    ![Boîte de dialogue pour sélectionner une tâche - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    c) en cliquant sur hello `.NET Core` élément crée hello `tasks.json` de fichiers dans votre `.vscode` active et ouvre hello fichier Bonjour `code editor` fenêtre. Il est sans toomodify besoin de ce fichier, onglet de fermer hello.

27.  Ouvrez hello `Visual Studio Code` intégrée fenêtre de terminal en appuyant sur les hello `Ctrl`  +  `backtick` clés ou à l’aide des menus de hello `View`  ->  `Integrated Terminal` et le type **.\binplace.ps1**dans hello `PowerShell` invite de commandes. Cette commande copie tous les notre répertoire de sortie toohello dépendances.

28. Parcourir le répertoire de sortie de projets toohello Bonjour `Integrated Terminal` fenêtre en tapant **cd.\bin\Debug\netstandard1.3**.

29. Exécutez l’exemple de projet hello en tapant **. \gw.exe gw-config.json** dans hello `Integrated Terminal` invite de la fenêtre. 
    - Si vous avez suivi des étapes de hello étroitement dans ce didacticiel, vous devez être en cours d’exécution hello `Azure IoT Edge BLE Data Converter Module` exemple de projet comme Bonjour suivant image :
    
        ![Exemple d’appareil simulé en cours d’exécution dans Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - Si vous souhaitez tooterminate hello application, appuyez sur hello `<Enter>` clé.

>[!IMPORTANT]
Il n’est pas recommandé toouse `Ctrl`  +  `C` tooterminate hello `IoT Edge` application passerelle (autrement dit, **gw.exe**). Comme cette opération peut entraîner hello processus tooterminate anormalement.

