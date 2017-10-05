---
title: "Créer un module Azure IoT Edge avec C# | Microsoft Docs"
description: "Ce didacticiel explique comment écrire un module de convertisseur de données BLE en utilisant les derniers packages NuGet Azure IoT Edge, Visual Studio Code et C#."
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
ms.openlocfilehash: 7175ffc8de2c043593d61143b402484d33e4a8cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="76028-104">Créer un module Azure IoT Edge avec C&#x23;</span><span class="sxs-lookup"><span data-stu-id="76028-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="76028-105">Ce didacticiel explique comment créer un module pour `Azure IoT Edge` à l’aide de `Visual Studio Code` et `C#`.</span><span class="sxs-lookup"><span data-stu-id="76028-105">This tutorial showcases how to create a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="76028-106">Dans ce didacticiel, nous aborderons la configuration de l’environnement et expliquerons comment écrire un module de convertisseur de données [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) en utilisant les derniers packages `Azure IoT Edge NuGet`.</span><span class="sxs-lookup"><span data-stu-id="76028-106">In this tutorial, we walk through environment set-up and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="76028-107">Ce didacticiel utilise le `.NET Core SDK`, qui prend en charge une compatibilité multiplateforme.</span><span class="sxs-lookup"><span data-stu-id="76028-107">This tutorial is using the `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="76028-108">Le didacticiel suivant est écrit à l’aide du système d’exploitation `Windows 10`.</span><span class="sxs-lookup"><span data-stu-id="76028-108">The following tutorial is written using the `Windows 10` operating system.</span></span> <span data-ttu-id="76028-109">Certaines commandes de ce didacticiel peuvent être différentes selon votre `development environment`.</span><span class="sxs-lookup"><span data-stu-id="76028-109">Some of the commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="76028-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="76028-110">Prerequisites</span></span>

<span data-ttu-id="76028-111">Dans cette section, vous configurez votre environnement pour le développement du module `Azure IoT Edge`.</span><span class="sxs-lookup"><span data-stu-id="76028-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="76028-112">Cela s’applique aux systèmes d’exploitation **Windows 64 bits** et **Linux 64 bits (Ubuntu/Debian 8)**.</span><span class="sxs-lookup"><span data-stu-id="76028-112">It applies to both **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="76028-113">Les logiciels suivants sont requis :</span><span class="sxs-lookup"><span data-stu-id="76028-113">The following software is required:</span></span>

- <span data-ttu-id="76028-114">[Client Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="76028-114">[Git Client](https://git-scm.com/downloads)</span></span>
- [<span data-ttu-id="76028-115">Kit de développement logiciel (SDK) principal NET</span><span class="sxs-lookup"><span data-stu-id="76028-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="76028-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="76028-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="76028-117">Vous n’avez pas besoin de cloner le référentiel pour cet exemple. Toutefois, tous les exemples de code présentés dans ce didacticiel se trouvent dans le référentiel suivant :</span><span class="sxs-lookup"><span data-stu-id="76028-117">You do not need to clone the repo for this sample, however all of the sample code discussed in this tutorial is located in the following repository:</span></span>

- <span data-ttu-id="76028-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="76028-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="76028-119">Prise en main</span><span class="sxs-lookup"><span data-stu-id="76028-119">Getting started</span></span>

1. <span data-ttu-id="76028-120">Installez `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="76028-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="76028-121">Installez `Visual Studio Code` et `C# extension` à partir de la Place de marché Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="76028-121">Install `Visual Studio Code` and the `C# extension` from the Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="76028-122">Visionnez ce [bref didacticiel vidéo](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) sur la prise en main de `Visual Studio Code` et `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="76028-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how to get started using `Visual Studio Code` and the `.NET Core SDK`.</span></span>

## <a name="creating-the-azure-iot-edge-converter-module"></a><span data-ttu-id="76028-123">Création du module de convertisseur Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="76028-123">Creating the Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="76028-124">Initialisez un nouveau projet C# de bibliothèque de classes `.NET Core` :</span><span class="sxs-lookup"><span data-stu-id="76028-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="76028-125">Ouvrez une invite de commandes (`Windows + R` -> `cmd` -> `enter`).</span><span class="sxs-lookup"><span data-stu-id="76028-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="76028-126">Accédez au dossier dans lequel vous souhaitez créer le projet `C#`.</span><span class="sxs-lookup"><span data-stu-id="76028-126">Navigate to the folder where you'd like to create the `C#` project.</span></span>
    - <span data-ttu-id="76028-127">Tapez **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="76028-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="76028-128">Cette commande crée une classe vide appelée `Class1.cs` dans votre répertoire de projets.</span><span class="sxs-lookup"><span data-stu-id="76028-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="76028-129">Accédez au dossier dans lequel nous venons de créer le projet de bibliothèque de classes en tapant **cd IoTEdgeConverterModule**.</span><span class="sxs-lookup"><span data-stu-id="76028-129">Navigate to the folder where we just created the class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="76028-130">Ouvrez le projet dans `Visual Studio Code` en tapant **code**.</span><span class="sxs-lookup"><span data-stu-id="76028-130">Open the project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="76028-131">Une fois le projet ouvert dans `Visual Studio Code`, cliquez sur **IoTEdgeConverterModule.csproj** pour ouvrir le fichier, comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="76028-131">Once the project is opened in `Visual Studio Code`, click on the **IoTEdgeConverterModule.csproj** to open the file as shown in the following image:</span></span>

    ![Fenêtre de modification - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="76028-133">Insérez le blob `XML` indiqué dans l’extrait de code suivant entre la balise de fin `PropertyGroup` et la balise de fin `Project` (ligne six dans l’image précédente) et enregistrez le fichier en appuyant sur `Ctrl` + `S`.</span><span class="sxs-lookup"><span data-stu-id="76028-133">Insert the `XML` blob shown in the following code snippet between the closing `PropertyGroup` tag and the closing `Project` tag; line six in the preceding image and save the file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="76028-134">Une fois que vous enregistrez le fichier `.csproj`, `Visual Studio Code` vous invite avec une boîte de dialogue `unresolved dependencies` comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="76028-134">Once you save the `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in the following image:</span></span> 

    ![Boîte de dialogue pour restaurer des dépendances de restauration - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="76028-136">a) Cliquez sur `Restore` pour restaurer toutes les références dans le fichier `.csproj` des projets, y compris l’élément `PackageReferences` que nous avons ajouté.</span><span class="sxs-lookup"><span data-stu-id="76028-136">a) Click `Restore` to restore all of the references in the projects `.csproj` file including the `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="76028-137">(b) `Visual Studio Code` crée automatiquement le fichier `project.assets.json` dans le dossier `obj` de vos projets.</span><span class="sxs-lookup"><span data-stu-id="76028-137">b) `Visual Studio Code` automatically creates the `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="76028-138">Ce fichier contient des informations sur les dépendances de votre projet pour accélérer les restaurations suivantes.</span><span class="sxs-lookup"><span data-stu-id="76028-138">This file contains information about your project's dependencies to make subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="76028-139">`.NET Core Tools` sont désormais basés sur MSBuild.</span><span class="sxs-lookup"><span data-stu-id="76028-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="76028-140">Ce qui signifie qu’un fichier de projet `.csproj` est créé à la place d’un `project.json`.</span><span class="sxs-lookup"><span data-stu-id="76028-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="76028-141">Si `Visual Studio Code` n’affiche aucune invite vous indiquant que tout fonctionne normalement, nous pouvons le faire manuellement.</span><span class="sxs-lookup"><span data-stu-id="76028-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="76028-142">Ouvrez la fenêtre de terminal intégré `Visual Studio Code` en appuyant sur les touches `Ctrl` + `backtick` ou utilisant les menus `View` -> `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="76028-142">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="76028-143">Dans la fenêtre `Integrated Terminal`, tapez **dotnet restore**.</span><span class="sxs-lookup"><span data-stu-id="76028-143">In the `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="76028-144">Renommez le fichier `Class1.cs` par `BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="76028-144">Rename the `Class1.cs` file to `BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="76028-145">a) Pour renommer le fichier, commencez par cliquer dessus, puis appuyez sur la touche `F2`.</span><span class="sxs-lookup"><span data-stu-id="76028-145">a) To rename the file first click on the file then press the `F2` key.</span></span>
    
    <span data-ttu-id="76028-146">b) Tapez le nouveau nom **BleConverterModule** comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="76028-146">b) Type in the new name **BleConverterModule**, as seen in the following image:</span></span>

    ![Renommer une classe - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="76028-148">Remplacez le code existant dans le fichier `BleConverterModule.cs` en copiant-collant l’extrait de code suivant dans votre fichier `BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="76028-148">Replace the existing code in the `BleConverterModule.cs` file by copying and pasting the following code snippet into your `BleConverterModule.cs` file.</span></span>

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

9. <span data-ttu-id="76028-149">Enregistrez le fichier en appuyant sur `Ctrl` + `S`.</span><span class="sxs-lookup"><span data-stu-id="76028-149">Save the file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="76028-150">Créez un fichier appelé `Untitled-1` en appuyant sur les touches `Ctrl` + `N` comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="76028-150">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys as seen in the following image:</span></span>

    ![Nouveau fichier - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="76028-152">Pour désérialiser l’objet `JSON` que nous recevons de l’appareil `BLE` simulé, copiez le code suivant dans la fenêtre d’éditeur de code du fichier `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="76028-152">To deserialize the `JSON` object that we receive from the simulated `BLE` device, copy the following code into the `Untitled-1` file code editor window.</span></span> 

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

12. <span data-ttu-id="76028-153">Enregistrez le fichier sous `BleData.cs` en appuyant sur les touches `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="76028-153">Save the file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="76028-154">Dans la boîte de dialogue Enregistrer sous, dans le menu déroulant `Save as Type`, sélectionnez `C# (*.cs;*.csx)` comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="76028-154">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in the following image:</span></span>

    ![Boîte de dialogue pour enregistrer sous - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="76028-156">Créez un fichier appelé `Untitled-1` en appuyant sur les touches `Ctrl` + `N`.</span><span class="sxs-lookup"><span data-stu-id="76028-156">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="76028-157">Copiez et collez l’extrait de code suivant dans le fichier `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="76028-157">Copy and paste the following code snippet into the `Untitled-1` file.</span></span> <span data-ttu-id="76028-158">Cette classe est un module `Azure IoT Edge`, qui nous permet de générer les données reçues à partir de notre `BleConverterModule`.</span><span class="sxs-lookup"><span data-stu-id="76028-158">This class is a `Azure IoT Edge` module, which we use to output the data received from our `BleConverterModule`.</span></span>

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

15. <span data-ttu-id="76028-159">Enregistrez le fichier sous `DotNetPrinterModule.cs` en appuyant sur `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="76028-159">Save the file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="76028-160">Dans la boîte de dialogue Enregistrer sous, dans le menu déroulant `Save as Type`, sélectionnez `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="76028-160">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="76028-161">Créez un fichier appelé `Untitled-1` en appuyant sur les touches `Ctrl` + `N`.</span><span class="sxs-lookup"><span data-stu-id="76028-161">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="76028-162">Pour désérialiser l’objet `JSON` que nous recevons de `BleConverterModule`, copiez et collez l’extrait de code suivant dans le fichier `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="76028-162">To deserialize the `JSON` object that we receive from the `BleConverterModule`, Copy and paste the following code snippet into the `Untitled-1` file.</span></span> 

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

18. <span data-ttu-id="76028-163">Enregistrez le fichier sous `BleConverterData.cs` en appuyant sur `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="76028-163">Save the file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="76028-164">Dans la boîte de dialogue Enregistrer sous, dans le menu déroulant `Save as Type`, sélectionnez `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="76028-164">On the save as dialog box, in the `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="76028-165">Créez un fichier appelé `Untitled-1` en appuyant sur les touches `Ctrl` + `N`.</span><span class="sxs-lookup"><span data-stu-id="76028-165">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="76028-166">Copiez et collez l’extrait de code suivant dans le fichier `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="76028-166">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

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

21. <span data-ttu-id="76028-167">Enregistrez le fichier sous `gw-config.json` en appuyant sur `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="76028-167">Save the file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="76028-168">Dans la boîte de dialogue Enregistrer sous, dans le menu déroulant `Save as Type`, sélectionnez `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span><span class="sxs-lookup"><span data-stu-id="76028-168">On the save as dialog box, in the `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="76028-169">Pour activer la copie du fichier config dans le répertoire de sortie, mettez à jour `IoTEdgeConverterModule.csproj` avec le blob XML suivant :</span><span class="sxs-lookup"><span data-stu-id="76028-169">To enable copying of the configuration file to the output directory, update the `IoTEdgeConverterModule.csproj` with the following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="76028-170">L’élément `IoTEdgeConverterModule.csproj` mis à jour doit ressembler à l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="76028-170">The updated `IoTEdgeConverterModule.csproj` should look like the following image:</span></span>

    ![Fichier .csproj mis à jour - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="76028-172">Créez un fichier appelé `Untitled-1` en appuyant sur les touches `Ctrl` + `N`.</span><span class="sxs-lookup"><span data-stu-id="76028-172">Create a new file called `Untitled-1` by pressing the `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="76028-173">Copiez et collez l’extrait de code suivant dans le fichier `Untitled-1`.</span><span class="sxs-lookup"><span data-stu-id="76028-173">Copy and paste the following code snippet into the `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="76028-174">Enregistrez le fichier sous `binplace.ps1` en appuyant sur `Ctrl` + `Shift` + `S`.</span><span class="sxs-lookup"><span data-stu-id="76028-174">Save the file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="76028-175">Dans la boîte de dialogue Enregistrer sous, dans le menu déroulant `Save as Type`, sélectionnez `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span><span class="sxs-lookup"><span data-stu-id="76028-175">On the save as dialog box, in the `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="76028-176">Générez le projet en appuyant sur les touches `Ctrl` + `Shift` + `B`.</span><span class="sxs-lookup"><span data-stu-id="76028-176">Build the project by pressing the `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="76028-177">Lorsque vous générez le projet pour la première fois, `Visual Studio Code` vous invite via la boîte de dialogue `No build task defined.` comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="76028-177">When you build the project for the first time, `Visual Studio Code` prompts you with the `No build task defined.` dialog as seen in the following image:</span></span>

    ![Boîte de dialogue de tâche de génération - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="76028-179">a) Cliquez sur le bouton `Configure Build Task`.</span><span class="sxs-lookup"><span data-stu-id="76028-179">a) Click the `Configure Build Task` button.</span></span>

    <span data-ttu-id="76028-180">b) Dans le menu déroulant de la boîte de dialogue `Select a Task Runner`,</span><span class="sxs-lookup"><span data-stu-id="76028-180">b) In the `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="76028-181">sélectionnez `.NET Core` comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="76028-181">Select `.NET Core` as seen in the following image:</span></span> 

    ![Boîte de dialogue pour sélectionner une tâche - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="76028-183">c) Cliquer sur l’élément `.NET Core` crée le fichier `tasks.json` dans votre répertoire `.vscode` et ouvre le fichier dans la fenêtre `code editor`.</span><span class="sxs-lookup"><span data-stu-id="76028-183">c) Clicking the `.NET Core` item creates the `tasks.json` file in your `.vscode` directory and opens the file in the `code editor` window.</span></span> <span data-ttu-id="76028-184">Il n’est pas nécessaire de modifier ce fichier, vous pouvez donc fermer l’onglet.</span><span class="sxs-lookup"><span data-stu-id="76028-184">There is no need to modify this file, close the tab.</span></span>

27.  <span data-ttu-id="76028-185">Ouvrez la fenêtre de terminal intégré `Visual Studio Code` en appuyant sur les touches `Ctrl` + `backtick` ou en utilisant les menus `View` -> `Integrated Terminal`, puis tapez **.\binplace.ps1** dans l’invite de commandes `PowerShell`.</span><span class="sxs-lookup"><span data-stu-id="76028-185">Open the `Visual Studio Code` integrated terminal window by pressing the `Ctrl` + `backtick` keys or using the menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into the `PowerShell` command prompt.</span></span> <span data-ttu-id="76028-186">Cette commande copie toutes nos dépendances dans le répertoire de sortie.</span><span class="sxs-lookup"><span data-stu-id="76028-186">This command copies all our dependencies to the output directory.</span></span>

28. <span data-ttu-id="76028-187">Accédez au répertoire de sortie des projets dans la fenêtre `Integrated Terminal` en tapant **cd .\bin\Debug\netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="76028-187">Navigate to the projects output directory in the `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="76028-188">Exécutez l’exemple de projet en tapant **.\gw.exe gw-config.json** dans l’invite de la fenêtre `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="76028-188">Run the sample project by typing **.\gw.exe gw-config.json** into the `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="76028-189">Si vous avez soigneusement suivi les étapes de ce didacticiel, l’exemple de projet `Azure IoT Edge BLE Data Converter Module` doit être en cours d’exécution comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="76028-189">If you have followed the steps in this tutorial closely, you should now be running the `Azure IoT Edge BLE Data Converter Module` sample project as seen in the following image:</span></span>
    
        ![Exemple d’appareil simulé en cours d’exécution dans Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="76028-191">Si vous souhaitez arrêter l’application, appuyez sur la touche `<Enter>`.</span><span class="sxs-lookup"><span data-stu-id="76028-191">If you want to terminate the application, press the `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="76028-192">Il est déconseillé d’utiliser `Ctrl` + `C` pour arrêter l’application de passerelle `IoT Edge` (c’est-à-dire **gw.exe**).</span><span class="sxs-lookup"><span data-stu-id="76028-192">It is not recommended to use `Ctrl` + `C` to terminate the `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="76028-193">Cela peut entraîner l’arrêt anormal du processus.</span><span class="sxs-lookup"><span data-stu-id="76028-193">As this action may cause the process to terminate abnormally.</span></span>

