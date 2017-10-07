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
# <a name="create-an-azure-iot-edge-module-with-cx23"></a><span data-ttu-id="78d8f-104">Créer un module Azure IoT Edge avec C&#x23;</span><span class="sxs-lookup"><span data-stu-id="78d8f-104">Create an Azure IoT Edge Module with C&#x23;</span></span>

<span data-ttu-id="78d8f-105">Ce didacticiel présente comment toocreate un module pour `Azure IoT Edge` à l’aide de `Visual Studio Code` et `C#`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-105">This tutorial showcases how toocreate a module for `Azure IoT Edge` using `Visual Studio Code` and `C#`.</span></span>

<span data-ttu-id="78d8f-106">Dans ce didacticiel, nous suivons la configuration de l’environnement et comment toowrite un [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) module de convertisseur de données à l’aide de hello dernières `Azure IoT Edge NuGet` packages.</span><span class="sxs-lookup"><span data-stu-id="78d8f-106">In this tutorial, we walk through environment set-up and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest `Azure IoT Edge NuGet` packages.</span></span> 

>[!NOTE]
<span data-ttu-id="78d8f-107">Ce didacticiel utilise hello `.NET Core SDK`, qui prend en charge une compatibilité multiplateforme.</span><span class="sxs-lookup"><span data-stu-id="78d8f-107">This tutorial is using hello `.NET Core SDK`, which supports cross-platform compatibility.</span></span> <span data-ttu-id="78d8f-108">Hello didacticiel suivant est écrit à l’aide de hello `Windows 10` système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="78d8f-108">hello following tutorial is written using hello `Windows 10` operating system.</span></span> <span data-ttu-id="78d8f-109">Certaines des commandes hello dans ce didacticiel peuvent être différent selon votre `development environment`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-109">Some of hello commands in this tutorial may be different depending on your `development environment`.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="78d8f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="78d8f-110">Prerequisites</span></span>

<span data-ttu-id="78d8f-111">Dans cette section, vous configurez votre environnement pour le développement du module `Azure IoT Edge`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-111">In this section, we set-up your environment for `Azure IoT Edge` module development.</span></span> <span data-ttu-id="78d8f-112">Il s’applique tooboth **Windows 64 bits** et **64 bits Linux (8 Ubuntu/Debian)** systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="78d8f-112">It applies tooboth **64-bit Windows** and **64-bit Linux (Ubuntu/Debian 8)** operating systems.</span></span>

<span data-ttu-id="78d8f-113">Hello suivant logicielle est requise :</span><span class="sxs-lookup"><span data-stu-id="78d8f-113">hello following software is required:</span></span>

- <span data-ttu-id="78d8f-114">[Client Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="78d8f-114">[Git Client](https://git-scm.com/downloads)</span></span>
- [<span data-ttu-id="78d8f-115">Kit de développement logiciel (SDK) principal NET</span><span class="sxs-lookup"><span data-stu-id="78d8f-115">.NET Core SDK</span></span>](https://www.microsoft.com/net/core#windowscmd)
- [<span data-ttu-id="78d8f-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="78d8f-116">Visual Studio Code</span></span>](https://code.visualstudio.com/)

<span data-ttu-id="78d8f-117">Vous n’avez pas besoin de référentiel de hello tooclone pour cet exemple, toutefois hello tous les exemples de code présenté dans ce didacticiel se trouve dans hello suivant du référentiel :</span><span class="sxs-lookup"><span data-stu-id="78d8f-117">You do not need tooclone hello repo for this sample, however all of hello sample code discussed in this tutorial is located in hello following repository:</span></span>

- <span data-ttu-id="78d8f-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-118">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
- `cd iot-edge-samples/dotnetcore/simulated_ble`

## <a name="getting-started"></a><span data-ttu-id="78d8f-119">Prise en main</span><span class="sxs-lookup"><span data-stu-id="78d8f-119">Getting started</span></span>

1. <span data-ttu-id="78d8f-120">Installez `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-120">Install `.NET Core SDK`.</span></span>
2. <span data-ttu-id="78d8f-121">Installer `Visual Studio Code` et hello `C# extension` à partir de Visual Studio Code Marketplace de hello.</span><span class="sxs-lookup"><span data-stu-id="78d8f-121">Install `Visual Studio Code` and hello `C# extension` from hello Visual Studio Code Marketplace.</span></span>

<span data-ttu-id="78d8f-122">Afficher ce [rapide didacticiel vidéo](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) sur la façon dont tooget route à l’aide de `Visual Studio Code` et hello `.NET Core SDK`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-122">View this [quick video tutorial](https://channel9.msdn.com/Blogs/dotnet/Get-started-VSCode-Csharp-NET-Core-Windows) about how tooget started using `Visual Studio Code` and hello `.NET Core SDK`.</span></span>

## <a name="creating-hello-azure-iot-edge-converter-module"></a><span data-ttu-id="78d8f-123">Création de module de conversion hello Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="78d8f-123">Creating hello Azure IoT Edge converter module</span></span>

1. <span data-ttu-id="78d8f-124">Initialisez un nouveau projet C# de bibliothèque de classes `.NET Core` :</span><span class="sxs-lookup"><span data-stu-id="78d8f-124">Initialize a new `.NET Core` class library C# project:</span></span>
    - <span data-ttu-id="78d8f-125">Ouvrez une invite de commandes (`Windows + R` -> `cmd` -> `enter`).</span><span class="sxs-lookup"><span data-stu-id="78d8f-125">Open a command prompt (`Windows + R` -> `cmd` -> `enter`).</span></span>
    - <span data-ttu-id="78d8f-126">Exploration du dossier toohello où vous aimeriez toocreate hello `C#` projet.</span><span class="sxs-lookup"><span data-stu-id="78d8f-126">Navigate toohello folder where you'd like toocreate hello `C#` project.</span></span>
    - <span data-ttu-id="78d8f-127">Tapez **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="78d8f-127">Type **dotnet new classlib -o IoTEdgeConverterModule -f netstandard1.3**.</span></span> 
    - <span data-ttu-id="78d8f-128">Cette commande crée une classe vide appelée `Class1.cs` dans votre répertoire de projets.</span><span class="sxs-lookup"><span data-stu-id="78d8f-128">This command creates an empty class called `Class1.cs` in your projects directory.</span></span>
2. <span data-ttu-id="78d8f-129">Exploration du dossier toohello où nous venons de créer le projet de bibliothèque de classes hello en tapant **cd IoTEdgeConverterModule**.</span><span class="sxs-lookup"><span data-stu-id="78d8f-129">Navigate toohello folder where we just created hello class library project by typing **cd IoTEdgeConverterModule**.</span></span>
3. <span data-ttu-id="78d8f-130">Projet ouvert hello dans `Visual Studio Code` en tapant **code.**.</span><span class="sxs-lookup"><span data-stu-id="78d8f-130">Open hello project in `Visual Studio Code` by typing **code .**.</span></span>
4. <span data-ttu-id="78d8f-131">Une fois le projet de hello est ouvert dans `Visual Studio Code`, cliquez sur hello **IoTEdgeConverterModule.csproj** fichier de hello tooopen comme indiqué dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="78d8f-131">Once hello project is opened in `Visual Studio Code`, click on hello **IoTEdgeConverterModule.csproj** tooopen hello file as shown in hello following image:</span></span>

    ![Fenêtre de modification - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-edit-csproj.png)

5. <span data-ttu-id="78d8f-133">Insérer hello `XML` blob illustré hello suivant extrait de code entre la fermeture de hello `PropertyGroup` de balise et hello fermeture `Project` balise ; six Bonjour précédant l’image de ligne et enregistrer le fichier de hello en appuyant sur `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-133">Insert hello `XML` blob shown in hello following code snippet between hello closing `PropertyGroup` tag and hello closing `Project` tag; line six in hello preceding image and save hello file by pressing `Ctrl` + `S`.</span></span>

   ```xml
     <ItemGroup>
       <PackageReference Include="Microsoft.Azure.Devices.Gateway.Module.NetStandard" Version="1.0.5" />
       <PackageReference Include="System.Threading.Thread" Version="4.3.0" />
       <PackageReference Include="Newtonsoft.Json" Version="10.0.2" />
     </ItemGroup> 
   ```

6. <span data-ttu-id="78d8f-134">Une fois que vous enregistrez hello `.csproj` fichier `Visual Studio Code` vous invite à entrer avec un `unresolved dependencies` boîte de dialogue comme dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="78d8f-134">Once you save hello `.csproj` file, `Visual Studio Code` should prompt you with an `unresolved dependencies` dialog as seen in hello following image:</span></span> 

    ![Boîte de dialogue pour restaurer des dépendances de restauration - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-restore.png)

    <span data-ttu-id="78d8f-136">un) cliquez sur `Restore` toorestore tous hello fait référence dans les projets hello `.csproj` fichier, y compris hello `PackageReferences` , nous avons ajouté.</span><span class="sxs-lookup"><span data-stu-id="78d8f-136">a) Click `Restore` toorestore all of hello references in hello projects `.csproj` file including hello `PackageReferences` we have added.</span></span> 

    <span data-ttu-id="78d8f-137">(b) `Visual Studio Code` crée automatiquement hello `project.assets.json` fichier dans vos projets `obj` dossier.</span><span class="sxs-lookup"><span data-stu-id="78d8f-137">b) `Visual Studio Code` automatically creates hello `project.assets.json` file in your projects `obj` folder.</span></span> <span data-ttu-id="78d8f-138">Ce fichier contient des informations à propos dépendances toomake les restaurations suivantes de votre projet plus rapides.</span><span class="sxs-lookup"><span data-stu-id="78d8f-138">This file contains information about your project's dependencies toomake subsequent restores quicker.</span></span>
 
    >[!NOTE]
    <span data-ttu-id="78d8f-139">`.NET Core Tools` sont désormais basés sur MSBuild.</span><span class="sxs-lookup"><span data-stu-id="78d8f-139">`.NET Core Tools` are now MSBuild-based.</span></span> <span data-ttu-id="78d8f-140">Ce qui signifie qu’un fichier de projet `.csproj` est créé à la place d’un `project.json`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-140">Which means a `.csproj` project file is created instead of a `project.json`.</span></span>

    - <span data-ttu-id="78d8f-141">Si `Visual Studio Code` n’affiche aucune invite vous indiquant que tout fonctionne normalement, nous pouvons le faire manuellement.</span><span class="sxs-lookup"><span data-stu-id="78d8f-141">If `Visual Studio Code` does not prompt you that is ok, we can do it manually.</span></span> <span data-ttu-id="78d8f-142">Ouvrez hello `Visual Studio Code` intégrée fenêtre de terminal en appuyant sur les hello `Ctrl`  +  `backtick` clés ou à l’aide des menus de hello `View`  ->  `Integrated Terminal`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-142">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal`.</span></span>
    - <span data-ttu-id="78d8f-143">Bonjour `Integrated Terminal` type de fenêtre **dotnet restauration**.</span><span class="sxs-lookup"><span data-stu-id="78d8f-143">In hello `Integrated Terminal` window type **dotnet restore**.</span></span>
    
7. <span data-ttu-id="78d8f-144">Renommer hello `Class1.cs` trop de fichiers`BleConverterModule.cs`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-144">Rename hello `Class1.cs` file too`BleConverterModule.cs`.</span></span> 

    <span data-ttu-id="78d8f-145">a) fichier de hello toorename tout d’abord sur hello fichier appuyez sur hello `F2` clé.</span><span class="sxs-lookup"><span data-stu-id="78d8f-145">a) toorename hello file first click on hello file then press hello `F2` key.</span></span>
    
    <span data-ttu-id="78d8f-146">b) type dans le nouveau nom de hello **BleConverterModule**, comme dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="78d8f-146">b) Type in hello new name **BleConverterModule**, as seen in hello following image:</span></span>

    ![Renommer une classe - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-rename.png)

8. <span data-ttu-id="78d8f-148">Remplacer le code existant dans hello hello `BleConverterModule.cs` fichier en copiant et hello collage suivante extrait de code dans votre `BleConverterModule.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="78d8f-148">Replace hello existing code in hello `BleConverterModule.cs` file by copying and pasting hello following code snippet into your `BleConverterModule.cs` file.</span></span>

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

9. <span data-ttu-id="78d8f-149">Enregistrez le fichier de hello en appuyant sur `Ctrl`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-149">Save hello file by pressing `Ctrl` + `S`.</span></span>

10. <span data-ttu-id="78d8f-150">Créer un nouveau fichier appelé `Untitled-1` en appuyant sur les hello `Ctrl`  +  `N` clés comme Bonjour suivant image :</span><span class="sxs-lookup"><span data-stu-id="78d8f-150">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys as seen in hello following image:</span></span>

    ![Nouveau fichier - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-new-file.png)

11. <span data-ttu-id="78d8f-152">toodeserialize hello `JSON` objet que nous recevons de hello simulée `BLE` de périphérique, hello copie suivante de code dans hello `Untitled-1` fenêtre d’éditeur de code de fichier.</span><span class="sxs-lookup"><span data-stu-id="78d8f-152">toodeserialize hello `JSON` object that we receive from hello simulated `BLE` device, copy hello following code into hello `Untitled-1` file code editor window.</span></span> 

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

12. <span data-ttu-id="78d8f-153">Enregistrer le fichier hello sous `BleData.cs` en appuyant sur `Ctrl`  +  `Shift`  +  `S` clés.</span><span class="sxs-lookup"><span data-stu-id="78d8f-153">Save hello file as `BleData.cs` by pressing `Ctrl` + `Shift` + `S` keys.</span></span>
    - <span data-ttu-id="78d8f-154">Sur hello enregistrer en tant que la boîte de dialogue hello `Save as Type` menu déroulant, sélectionnez `C# (*.cs;*.csx)` comme Bonjour suivant image :</span><span class="sxs-lookup"><span data-stu-id="78d8f-154">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)` as seen in hello following image:</span></span>

    ![Boîte de dialogue pour enregistrer sous - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-save-as.png)

13. <span data-ttu-id="78d8f-156">Créer un nouveau fichier appelé `Untitled-1` en appuyant sur les hello `Ctrl`  +  `N` clés.</span><span class="sxs-lookup"><span data-stu-id="78d8f-156">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

14. <span data-ttu-id="78d8f-157">Copiez et collez hello suivant extrait de code dans hello `Untitled-1` fichier.</span><span class="sxs-lookup"><span data-stu-id="78d8f-157">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> <span data-ttu-id="78d8f-158">Cette classe est un `Azure IoT Edge` module, que nous utilisons les données de hello toooutput reçues à partir de notre `BleConverterModule`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-158">This class is a `Azure IoT Edge` module, which we use toooutput hello data received from our `BleConverterModule`.</span></span>

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

15. <span data-ttu-id="78d8f-159">Enregistrer le fichier hello sous `DotNetPrinterModule.cs` en appuyant sur `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-159">Save hello file as `DotNetPrinterModule.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="78d8f-160">Sur hello enregistrer en tant que la boîte de dialogue hello `Save as Type` menu déroulant, sélectionnez `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-160">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

16. <span data-ttu-id="78d8f-161">Créer un nouveau fichier appelé `Untitled-1` en appuyant sur les hello `Ctrl`  +  `N` clés.</span><span class="sxs-lookup"><span data-stu-id="78d8f-161">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

17. <span data-ttu-id="78d8f-162">toodeserialize hello `JSON` objet que nous recevons de hello `BleConverterModule`, copie et suit hello de coller extrait de code hello `Untitled-1` fichier.</span><span class="sxs-lookup"><span data-stu-id="78d8f-162">toodeserialize hello `JSON` object that we receive from hello `BleConverterModule`, Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span> 

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

18. <span data-ttu-id="78d8f-163">Enregistrer le fichier hello sous `BleConverterData.cs` en appuyant sur `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-163">Save hello file as `BleConverterData.cs` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="78d8f-164">Sur hello enregistrer en tant que la boîte de dialogue hello `Save as Type` menu déroulant, sélectionnez `C# (*.cs;*.csx)`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-164">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `C# (*.cs;*.csx)`.</span></span>

19. <span data-ttu-id="78d8f-165">Créer un nouveau fichier appelé `Untitled-1` en appuyant sur les hello `Ctrl`  +  `N` clés.</span><span class="sxs-lookup"><span data-stu-id="78d8f-165">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

20. <span data-ttu-id="78d8f-166">Copiez et collez hello suivant extrait de code dans hello `Untitled-1` fichier.</span><span class="sxs-lookup"><span data-stu-id="78d8f-166">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

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

21. <span data-ttu-id="78d8f-167">Enregistrer le fichier hello sous `gw-config.json` en appuyant sur `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-167">Save hello file as `gw-config.json` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="78d8f-168">Sur hello enregistrer en tant que la boîte de dialogue hello `Save as Type` menu déroulant, sélectionnez `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-168">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `JSON (*.json;*.bowerrc;*.jshintrc;*.jscsrc;*.eslintrc;*.babelrc;*webmanifest)`.</span></span>

22. <span data-ttu-id="78d8f-169">répertoire, hello de mise à jour de sortie de copie de tooenable de toohello de fichier de configuration hello `IoTEdgeConverterModule.csproj` avec hello suivant l’objet blob XML :</span><span class="sxs-lookup"><span data-stu-id="78d8f-169">tooenable copying of hello configuration file toohello output directory, update hello `IoTEdgeConverterModule.csproj` with hello following XML blob:</span></span>

   ```xml
     <ItemGroup>
       <None Update="gw-config.json" CopyToOutputDirectory="PreserveNewest" />
     </ItemGroup>
   ```
    
   - <span data-ttu-id="78d8f-170">mise à jour de Hello `IoTEdgeConverterModule.csproj` doit ressemble hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="78d8f-170">hello updated `IoTEdgeConverterModule.csproj` should look like hello following image:</span></span>

    ![Fichier .csproj mis à jour - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-update-csproj.png)

23. <span data-ttu-id="78d8f-172">Créer un nouveau fichier appelé `Untitled-1` en appuyant sur les hello `Ctrl`  +  `N` clés.</span><span class="sxs-lookup"><span data-stu-id="78d8f-172">Create a new file called `Untitled-1` by pressing hello `Ctrl` + `N` keys.</span></span>

24. <span data-ttu-id="78d8f-173">Copiez et collez hello suivant extrait de code dans hello `Untitled-1` fichier.</span><span class="sxs-lookup"><span data-stu-id="78d8f-173">Copy and paste hello following code snippet into hello `Untitled-1` file.</span></span>

   ```powershell
   Copy-Item -Path $env:userprofile\.nuget\packages\microsoft.azure.devices.gateway.native.windows.x64\1.1.3\runtimes\win-x64\native\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.formatters\4.3.0\lib\netstandard1.4\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.runtime.serialization.primitives\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\newtonsoft.json\10.0.2\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.componentmodel.typeconverter\4.3.0\lib\netstandard1.5\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.nongeneric\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   Copy-Item -Path $env:userprofile\.nuget\packages\system.collections.specialized\4.3.0\lib\netstandard1.3\* -Destination .\bin\Debug\netstandard1.3
   ```

25. <span data-ttu-id="78d8f-174">Enregistrer le fichier hello sous `binplace.ps1` en appuyant sur `Ctrl`  +  `Shift`  +  `S`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-174">Save hello file as `binplace.ps1` by pressing `Ctrl` + `Shift` + `S`.</span></span>
    - <span data-ttu-id="78d8f-175">Sur hello enregistrer en tant que la boîte de dialogue hello `Save as Type` menu déroulant, sélectionnez `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span><span class="sxs-lookup"><span data-stu-id="78d8f-175">On hello save as dialog box, in hello `Save as Type` dropdown menu, select `PowerShell (*.ps1;*.psm1;*.psd1;*.pssc;*.psrc)`.</span></span>

26. <span data-ttu-id="78d8f-176">Générer le projet de hello en appuyant sur les hello `Ctrl`  +  `Shift`  +  `B` clés.</span><span class="sxs-lookup"><span data-stu-id="78d8f-176">Build hello project by pressing hello `Ctrl` + `Shift` + `B` keys.</span></span> <span data-ttu-id="78d8f-177">Lorsque vous générez des projets hello pour hello première fois, `Visual Studio Code` vous invite à hello `No build task defined.` boîte de dialogue comme dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="78d8f-177">When you build hello project for hello first time, `Visual Studio Code` prompts you with hello `No build task defined.` dialog as seen in hello following image:</span></span>

    ![Boîte de dialogue de tâche de génération - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task.png)

    <span data-ttu-id="78d8f-179">un) cliquez sur hello `Configure Build Task` bouton.</span><span class="sxs-lookup"><span data-stu-id="78d8f-179">a) Click hello `Configure Build Task` button.</span></span>

    <span data-ttu-id="78d8f-180">(b) dans hello `Select a Task Runner` menu déroulant de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="78d8f-180">b) In hello `Select a Task Runner` dialog dropdown menu.</span></span> <span data-ttu-id="78d8f-181">Sélectionnez `.NET Core` comme Bonjour suivant image :</span><span class="sxs-lookup"><span data-stu-id="78d8f-181">Select `.NET Core` as seen in hello following image:</span></span> 

    ![Boîte de dialogue pour sélectionner une tâche - Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-build-task-runner.png)

    <span data-ttu-id="78d8f-183">c) en cliquant sur hello `.NET Core` élément crée hello `tasks.json` de fichiers dans votre `.vscode` active et ouvre hello fichier Bonjour `code editor` fenêtre.</span><span class="sxs-lookup"><span data-stu-id="78d8f-183">c) Clicking hello `.NET Core` item creates hello `tasks.json` file in your `.vscode` directory and opens hello file in hello `code editor` window.</span></span> <span data-ttu-id="78d8f-184">Il est sans toomodify besoin de ce fichier, onglet de fermer hello.</span><span class="sxs-lookup"><span data-stu-id="78d8f-184">There is no need toomodify this file, close hello tab.</span></span>

27.  <span data-ttu-id="78d8f-185">Ouvrez hello `Visual Studio Code` intégrée fenêtre de terminal en appuyant sur les hello `Ctrl`  +  `backtick` clés ou à l’aide des menus de hello `View`  ->  `Integrated Terminal` et le type **.\binplace.ps1**dans hello `PowerShell` invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="78d8f-185">Open hello `Visual Studio Code` integrated terminal window by pressing hello `Ctrl` + `backtick` keys or using hello menus `View` -> `Integrated Terminal` and type **.\binplace.ps1** into hello `PowerShell` command prompt.</span></span> <span data-ttu-id="78d8f-186">Cette commande copie tous les notre répertoire de sortie toohello dépendances.</span><span class="sxs-lookup"><span data-stu-id="78d8f-186">This command copies all our dependencies toohello output directory.</span></span>

28. <span data-ttu-id="78d8f-187">Parcourir le répertoire de sortie de projets toohello Bonjour `Integrated Terminal` fenêtre en tapant **cd.\bin\Debug\netstandard1.3**.</span><span class="sxs-lookup"><span data-stu-id="78d8f-187">Navigate toohello projects output directory in hello `Integrated Terminal` window by typing **cd .\bin\Debug\netstandard1.3**.</span></span>

29. <span data-ttu-id="78d8f-188">Exécutez l’exemple de projet hello en tapant **. \gw.exe gw-config.json** dans hello `Integrated Terminal` invite de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="78d8f-188">Run hello sample project by typing **.\gw.exe gw-config.json** into hello `Integrated Terminal` window prompt.</span></span> 
    - <span data-ttu-id="78d8f-189">Si vous avez suivi des étapes de hello étroitement dans ce didacticiel, vous devez être en cours d’exécution hello `Azure IoT Edge BLE Data Converter Module` exemple de projet comme Bonjour suivant image :</span><span class="sxs-lookup"><span data-stu-id="78d8f-189">If you have followed hello steps in this tutorial closely, you should now be running hello `Azure IoT Edge BLE Data Converter Module` sample project as seen in hello following image:</span></span>
    
        ![Exemple d’appareil simulé en cours d’exécution dans Visual Studio Code](media/iot-hub-iot-edge-create-module/vscode-run.png)
    
    - <span data-ttu-id="78d8f-191">Si vous souhaitez tooterminate hello application, appuyez sur hello `<Enter>` clé.</span><span class="sxs-lookup"><span data-stu-id="78d8f-191">If you want tooterminate hello application, press hello `<Enter>` key.</span></span>

>[!IMPORTANT]
<span data-ttu-id="78d8f-192">Il n’est pas recommandé toouse `Ctrl`  +  `C` tooterminate hello `IoT Edge` application passerelle (autrement dit, **gw.exe**).</span><span class="sxs-lookup"><span data-stu-id="78d8f-192">It is not recommended toouse `Ctrl` + `C` tooterminate hello `IoT Edge` gateway application (that is, **gw.exe**).</span></span> <span data-ttu-id="78d8f-193">Comme cette opération peut entraîner hello processus tooterminate anormalement.</span><span class="sxs-lookup"><span data-stu-id="78d8f-193">As this action may cause hello process tooterminate abnormally.</span></span>

