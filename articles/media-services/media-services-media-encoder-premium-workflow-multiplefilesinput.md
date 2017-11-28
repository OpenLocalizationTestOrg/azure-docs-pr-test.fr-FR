---
title: "Plusieurs fichiers d’entrée et propriétés du composant avec Premium Encoder - Azure | Microsoft Docs"
description: "Cette rubrique explique comment utiliser setRuntimeProperties pour plusieurs fichiers d’entrée et transmettre des données personnalisées au processeur multimédia de flux de travail Media Encoder Premium."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: 7fb35bdd-9891-4401-a65b-ef3cc8190e8a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: xpouyat;anilmur;juliako
ms.openlocfilehash: df1ee5089a0af6ffce1431b658843fcb34a66ce5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="9343a-103">Utilisation de plusieurs fichiers d’entrée et propriétés du composant avec Premium Encoder</span><span class="sxs-lookup"><span data-stu-id="9343a-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="9343a-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9343a-104">Overview</span></span>
<span data-ttu-id="9343a-105">Il existe des scénarios dans lesquels vous devrez peut-être personnaliser les propriétés du composant, spécifier le contenu du fichier XML de liste de séquences ou envoyer plusieurs fichiers d’entrée lorsque vous soumettez une tâche avec le processeur multimédia **Media Encoder Premium Workflow** .</span><span class="sxs-lookup"><span data-stu-id="9343a-105">There are scenarios in which you might need to customize component properties, specify Clip List XML content, or send multiple input files when you submit a task with the **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="9343a-106">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="9343a-106">Some examples are:</span></span>

* <span data-ttu-id="9343a-107">Superposition de texte sur la vidéo et définition de la valeur du texte (par exemple, la date actuelle) au moment de l’exécution pour chaque vidéo d’entrée.</span><span class="sxs-lookup"><span data-stu-id="9343a-107">Overlaying text on video and setting the text value (for example, the current date) at runtime for each input video.</span></span>
* <span data-ttu-id="9343a-108">Personnalisation du fichier XML de liste de séquences (pour spécifier un ou plusieurs fichiers source, avec ou sans découpage, etc.).</span><span class="sxs-lookup"><span data-stu-id="9343a-108">Customizing the Clip List XML (to specify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="9343a-109">Superposition d’une image de logo sur l’entrée vidéo pendant l’encodage de la vidéo.</span><span class="sxs-lookup"><span data-stu-id="9343a-109">Overlaying a logo image on the input video while the video is encoded.</span></span>
* <span data-ttu-id="9343a-110">Encodage de plusieurs langues audio.</span><span class="sxs-lookup"><span data-stu-id="9343a-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="9343a-111">Pour faire savoir à **Media Encoder Premium Workflow** que vous modifiez certaines propriétés dans le flux de travail quand vous créez la tâche ou envoyez plusieurs fichiers d’entrée, vous devez utiliser une chaîne de configuration qui contient **setRuntimeProperties** et/ou **transcodeSource**.</span><span class="sxs-lookup"><span data-stu-id="9343a-111">To let the **Media Encoder Premium Workflow** know that you are changing some properties in the workflow when you create the task or send multiple input files, you have to use a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="9343a-112">Cette rubrique explique comment les utiliser.</span><span class="sxs-lookup"><span data-stu-id="9343a-112">This topic explains how to use them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="9343a-113">Syntaxe de chaîne de configuration</span><span class="sxs-lookup"><span data-stu-id="9343a-113">Configuration string syntax</span></span>
<span data-ttu-id="9343a-114">La chaîne de configuration à définir dans la tâche d’encodage utilise un document XML qui ressemble au document suivant :</span><span class="sxs-lookup"><span data-stu-id="9343a-114">The configuration string to set in the encoding task uses an XML document that looks like this:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<transcodeRequest>
  <transcodeSource>
  </transcodeSource>
  <setRuntimeProperties>
    <property propertyPath="Media File Input/filename" value="VideoFileName.mp4" />
  </setRuntimeProperties>
</transcodeRequest>
```

<span data-ttu-id="9343a-115">Voici le code C# qui lit la configuration XML d’un fichier, la met à jour avec le nom de fichier vidéo approprié et la transmet à la tâche d’un travail :</span><span class="sxs-lookup"><span data-stu-id="9343a-115">The following is the C# code that reads the XML configuration from a file, update it with the right video filename and passes it to the task in a job:</span></span>

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass to it the name of the 
// processor to use for the specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with the encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify the input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset to contain the results of the job. 
// This output is specified as AssetCreationOptions.None, which 
// means the output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a><span data-ttu-id="9343a-116">Personnalisation des propriétés du composant</span><span class="sxs-lookup"><span data-stu-id="9343a-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="9343a-117">Propriété avec une valeur simple</span><span class="sxs-lookup"><span data-stu-id="9343a-117">Property with a simple value</span></span>
<span data-ttu-id="9343a-118">Dans certains cas, il peut être utile de personnaliser une propriété du composant avec le fichier de flux de travail qui doit être exécuté par Media Encoder Premium Workflow.</span><span class="sxs-lookup"><span data-stu-id="9343a-118">In some cases, it is useful to customize a component property together with the workflow file that is going to be executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="9343a-119">Supposons que vous ayez conçu un flux de travail qui superpose du texte sur vos vidéos et que ce texte (par exemple, la date actuelle) doive être défini au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="9343a-119">Suppose you designed a workflow that overlays text on your videos, and the text (for example, the current date) is supposed to be set at runtime.</span></span> <span data-ttu-id="9343a-120">Pour cela, vous pouvez envoyer le texte à définir comme nouvelle valeur de la propriété de texte du composant Overlay à partir de la tâche d’encodage.</span><span class="sxs-lookup"><span data-stu-id="9343a-120">You can do this by sending the text to be set as the new value for the text property of the overlay component from the encoding task.</span></span> <span data-ttu-id="9343a-121">Vous pouvez utiliser ce mécanisme pour modifier d’autres propriétés d’un composant du flux de travail (par exemple, la position ou la couleur de la superposition, la vitesse de transmission de l’encodeur AVC, etc.).</span><span class="sxs-lookup"><span data-stu-id="9343a-121">You can use this mechanism to change other properties of a component in the workflow (such as the position or color of the overlay, the bitrate of the AVC encoder, etc.).</span></span>

<span data-ttu-id="9343a-122">**setRuntimeProperties** est utilisé pour remplacer une propriété dans les composants du flux de travail.</span><span class="sxs-lookup"><span data-stu-id="9343a-122">**setRuntimeProperties** is used to override a property in the components of the workflow.</span></span>

<span data-ttu-id="9343a-123">Exemple :</span><span class="sxs-lookup"><span data-stu-id="9343a-123">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text To Image Converter/text" value="Today is Friday the 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a><span data-ttu-id="9343a-124">Propriété avec une valeur XML</span><span class="sxs-lookup"><span data-stu-id="9343a-124">Property with an XML value</span></span>
<span data-ttu-id="9343a-125">Pour définir une propriété qui attend une valeur XML, encapsulez à l’aide de `<![CDATA[ and ]]>`.</span><span class="sxs-lookup"><span data-stu-id="9343a-125">To set a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="9343a-126">Exemple :</span><span class="sxs-lookup"><span data-stu-id="9343a-126">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

> [!NOTE]
> <span data-ttu-id="9343a-127">Assurez-vous de ne pas mettre de retour chariot juste après `<![CDATA[`.</span><span class="sxs-lookup"><span data-stu-id="9343a-127">Make sure not to put a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="9343a-128">Valeur propertyPath</span><span class="sxs-lookup"><span data-stu-id="9343a-128">propertyPath value</span></span>
<span data-ttu-id="9343a-129">Dans les exemples précédents, la valeur propertyPath était « /Media File Input/filename », « /inactiveTimeout » ou « clipListXml ».</span><span class="sxs-lookup"><span data-stu-id="9343a-129">In the previous examples, the propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="9343a-130">Il s’agit en général du nom du composant, puis du nom de la propriété.</span><span class="sxs-lookup"><span data-stu-id="9343a-130">This is, in general, the name of the component, then the name of the property.</span></span> <span data-ttu-id="9343a-131">Le chemin d’accès peut avoir un nombre de niveaux différent, comme « / primarySourceFile » (étant donné que la propriété est à la racine du flux de travail) ou « /Video Processing/Graphic Overlay/Opacity » (car la propriété Overlay est dans un groupe).</span><span class="sxs-lookup"><span data-stu-id="9343a-131">The path can have more or fewer levels, like "/primarySourceFile" (because the property is at the root of the workflow) or "/Video Processing/Graphic Overlay/Opacity" (because the Overlay is in a group).</span></span>    

<span data-ttu-id="9343a-132">Pour vérifier le nom du chemin et de la propriété, utilisez le bouton d’action en regard de chaque propriété.</span><span class="sxs-lookup"><span data-stu-id="9343a-132">To check the path and property name, use the action button that is immediately beside each property.</span></span> <span data-ttu-id="9343a-133">Vous pouvez cliquer sur ce bouton d’action et sélectionner **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="9343a-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="9343a-134">Cette commande affiche le nom réel de la propriété et, juste au-dessus, l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="9343a-134">This will show you the actual name of the property, and immediately above it, the namespace.</span></span>

![Action/Modifier](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Propriété](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="9343a-137">Fichiers d’entrée multiples</span><span class="sxs-lookup"><span data-stu-id="9343a-137">Multiple input files</span></span>
<span data-ttu-id="9343a-138">Chaque tâche que vous envoyez au **Media Encoder Premium Workflow** nécessite deux éléments :</span><span class="sxs-lookup"><span data-stu-id="9343a-138">Each task that you submit to the **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="9343a-139">Une *Ressource de flux de travail* qui contient un fichier de flux de travail.</span><span class="sxs-lookup"><span data-stu-id="9343a-139">The first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="9343a-140">pouvant être créé à l’aide du [Concepteur de flux de travail](media-services-workflow-designer.md).</span><span class="sxs-lookup"><span data-stu-id="9343a-140">You can design workflow files by using the [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="9343a-141">Un *Élément multimédia* qui contient le(s) fichier(s) multimédia(s) que vous souhaitez encoder.</span><span class="sxs-lookup"><span data-stu-id="9343a-141">The second one is a *Media Asset* that contains the media file(s) that you want to encode.</span></span>

<span data-ttu-id="9343a-142">Lorsque vous envoyez plusieurs fichiers multimédias à l’encodeur **Media Encoder Premium Workflow** , les contraintes suivantes s’appliquent :</span><span class="sxs-lookup"><span data-stu-id="9343a-142">When you're sending multiple media files to the **Media Encoder Premium Workflow** encoder, the following constraints apply:</span></span>

* <span data-ttu-id="9343a-143">Tous les fichiers multimédias doivent être dans le même *Élément multimédia*.</span><span class="sxs-lookup"><span data-stu-id="9343a-143">All the media files must be in the same *Media Asset*.</span></span> <span data-ttu-id="9343a-144">L’utilisation de plusieurs éléments multimédias n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="9343a-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="9343a-145">Vous devez définir le fichier principal dans cet élément multimédia (dans l’idéal, il s’agit du fichier vidéo principal que l’encodeur doit traiter).</span><span class="sxs-lookup"><span data-stu-id="9343a-145">You must set the primary file in this Media Asset (ideally, this is the main video file that the encoder is asked to process).</span></span>
* <span data-ttu-id="9343a-146">Il est nécessaire de passer les données de configuration qui incluent l’élément **setRuntimeProperties** et/ou **transcodeSource** au processeur.</span><span class="sxs-lookup"><span data-stu-id="9343a-146">It is necessary to pass configuration data that includes the **setRuntimeProperties** and/or **transcodeSource** element to the processor.</span></span>
  * <span data-ttu-id="9343a-147">**setRuntimeProperties** est utilisé pour remplacer la propriété Nom de fichier ou une autre propriété dans les composants du flux de travail.</span><span class="sxs-lookup"><span data-stu-id="9343a-147">**setRuntimeProperties** is used to override the filename property or another property in the components of the workflow.</span></span>
  * <span data-ttu-id="9343a-148">**transcodeSource** est utilisé pour spécifier le contenu du fichier XML de liste de séquences.</span><span class="sxs-lookup"><span data-stu-id="9343a-148">**transcodeSource** is used to specify the Clip List XML content.</span></span>

<span data-ttu-id="9343a-149">Connexions dans le flux de travail :</span><span class="sxs-lookup"><span data-stu-id="9343a-149">Connections in the workflow:</span></span>

* <span data-ttu-id="9343a-150">Si vous utilisez un ou plusieurs composants Media File Input et que vous envisagez d’utiliser **setRuntimeProperties** pour spécifier le nom de fichier, ne leur connectez pas la broche du composant de fichier principal.</span><span class="sxs-lookup"><span data-stu-id="9343a-150">If you use one or several Media File Input components and plan to use **setRuntimeProperties** to specify the file name, then do not connect the primary file component pin to them.</span></span> <span data-ttu-id="9343a-151">Vérifiez qu’il n’y a aucune connexion entre l’objet de fichier principal et le(s) composant(s) Media File Input.</span><span class="sxs-lookup"><span data-stu-id="9343a-151">Make sure that there is no connection between the primary file object and the Media File Input(s).</span></span>
* <span data-ttu-id="9343a-152">Si vous préférez utiliser le fichier XML de liste de séquences et un composant Media Source, vous pouvez les connecter entre eux.</span><span class="sxs-lookup"><span data-stu-id="9343a-152">If you prefer to use Clip List XML and one Media Source component, then you can connect both together.</span></span>

![Aucune connexion entre la propriété Primary Source File et le composant Media File Input](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="9343a-154">*Il n’y a aucune connexion entre le fichier principal et le(s) composant(s) Media File Input si vous utilisez setRuntimeProperties pour définir la propriété Nom de fichier.*</span><span class="sxs-lookup"><span data-stu-id="9343a-154">*There is no connection from the primary file to Media File Input component(s) if you use setRuntimeProperties to set the filename property.*</span></span>

![Connexion depuis le fichier XML de liste de séquences au composant Clip List Source](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="9343a-156">*Vous pouvez connecter le fichier XML de liste de séquences à Media Source et utiliser transcodeSource.*</span><span class="sxs-lookup"><span data-stu-id="9343a-156">*You can connect Clip List XML to Media Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="9343a-157">Personnalisation du fichier XML de liste de séquences</span><span class="sxs-lookup"><span data-stu-id="9343a-157">Clip List XML customization</span></span>
<span data-ttu-id="9343a-158">Vous pouvez spécifier le fichier XML de liste de séquences dans le flux de travail, lors de l’exécution, à l’aide de **transcodeSource** dans la chaîne de configuration XML.</span><span class="sxs-lookup"><span data-stu-id="9343a-158">You can specify the Clip List XML in the workflow at runtime by using **transcodeSource** in the configuration string XML.</span></span> <span data-ttu-id="9343a-159">Cela nécessite que la broche du fichier XML de liste de séquences soit connectée au composant Media Source dans le flux de travail.</span><span class="sxs-lookup"><span data-stu-id="9343a-159">This requires the Clip List XML pin to be connected to the Media Source component in the workflow.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <transcodeSource>
      <clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
      </clipList>
    </transcodeSource>
    <setRuntimeProperties>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="9343a-160">Si vous souhaitez spécifier /primarySourceFile pour utiliser cette propriété afin de nommer les fichiers de sortie à l’aide de « Expressions », nous vous recommandons de transmettre le fichier XML de liste de séquences en tant que propriété *après* la propriété /primarySourceFile, afin d’éviter que la liste de séquences ne soit remplacée par le paramètre /primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="9343a-160">If you want to specify /primarySourceFile to use this property to name the output files by using 'Expressions', then we recommend passing the Clip List XML as a property *after* the /primarySourceFile property, to avoid having the Clip List be overridden by the /primarySourceFile setting.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="c:\temp\start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="9343a-161">Avec découpage précis de la trame supplémentaire :</span><span class="sxs-lookup"><span data-stu-id="9343a-161">With additional frame-accurate trimming:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

## <a name="example-1--overlay-an-image-on-top-of-the-video"></a><span data-ttu-id="9343a-162">Exemple 1 : Superposition d’une image sur la vidéo</span><span class="sxs-lookup"><span data-stu-id="9343a-162">Example 1 : Overlay an image on top of the video</span></span>

### <a name="presentation"></a><span data-ttu-id="9343a-163">Présentation</span><span class="sxs-lookup"><span data-stu-id="9343a-163">Presentation</span></span>
<span data-ttu-id="9343a-164">Prenons un exemple dans lequel vous voulez superposer une image de logo sur la vidéo d’entrée pendant l’encodage de la vidéo.</span><span class="sxs-lookup"><span data-stu-id="9343a-164">Consider an example in which you want to overlay a logo image on the input video while the video is encoded.</span></span> <span data-ttu-id="9343a-165">Dans cet exemple, la vidéo d’entrée est nommée « Microsoft_HoloLens_Possibilities_816p24.mp4 » et le logo est nommé « logo.png ».</span><span class="sxs-lookup"><span data-stu-id="9343a-165">In this example, the input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and the logo is named "logo.png".</span></span> <span data-ttu-id="9343a-166">Vous devez effectuer les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9343a-166">You should perform the following steps:</span></span>

* <span data-ttu-id="9343a-167">Créez une ressource de flux de travail avec le fichier de flux de travail (voir l’exemple suivant).</span><span class="sxs-lookup"><span data-stu-id="9343a-167">Create a Workflow Asset with the workflow file (see the following example).</span></span>
* <span data-ttu-id="9343a-168">Créez un élément multimédia contenant deux fichiers : MyInputVideo.mp4 en tant que fichier principal et MyLogo.png.</span><span class="sxs-lookup"><span data-stu-id="9343a-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as the primary file and MyLogo.png.</span></span>
* <span data-ttu-id="9343a-169">Envoyez une tâche au processeur multimédia Media Encoder Premium Workflow avec les ressources d’entrée ci-dessus et spécifiez la chaîne de configuration suivante.</span><span class="sxs-lookup"><span data-stu-id="9343a-169">Send a task to the Media Encoder Premium Workflow media processor with the above input assets and specify the following configuration string.</span></span>

<span data-ttu-id="9343a-170">Configuration :</span><span class="sxs-lookup"><span data-stu-id="9343a-170">Configuration:</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="9343a-171">Dans l’exemple ci-dessus, le nom du fichier vidéo est envoyé au composant Media File Input et à la propriété primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="9343a-171">In the example above, the name of the video file is sent to the Media File Input component and the primarySourceFile property.</span></span> <span data-ttu-id="9343a-172">Le nom du fichier logo est envoyé à un autre Media File Input connecté au composant de superposition graphique.</span><span class="sxs-lookup"><span data-stu-id="9343a-172">The name of the logo file is sent to another Media File Input that is connected to the graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="9343a-173">Le nom du fichier vidéo est envoyé à la propriété primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="9343a-173">The video file name is sent to the primarySourceFile property.</span></span> <span data-ttu-id="9343a-174">L’objectif est d’utiliser cette propriété dans le flux de travail pour générer le nom de fichier de sortie correct à l’aide d’Expressions, par exemple.</span><span class="sxs-lookup"><span data-stu-id="9343a-174">The reason for this is to use this property in the workflow for building the correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="9343a-175">Procédure de création de workflow pas à pas</span><span class="sxs-lookup"><span data-stu-id="9343a-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="9343a-176">Voici les étapes pour créer un flux de travail prenant deux fichiers en entrée : une vidéo et une image.</span><span class="sxs-lookup"><span data-stu-id="9343a-176">Here are the steps to create a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="9343a-177">Ce flux de travail superpose l’image sur la vidéo.</span><span class="sxs-lookup"><span data-stu-id="9343a-177">It will overlay the image on top of the video.</span></span>

<span data-ttu-id="9343a-178">Ouvrez **Concepteur de flux de travail** et sélectionnez **Fichier** > **Nouvel espace de travail** > **Plan de transcodage**.</span><span class="sxs-lookup"><span data-stu-id="9343a-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="9343a-179">Le nouveau flux de travail affiche trois éléments :</span><span class="sxs-lookup"><span data-stu-id="9343a-179">The new workflow shows three elements:</span></span>

* <span data-ttu-id="9343a-180">Fichier source principal</span><span class="sxs-lookup"><span data-stu-id="9343a-180">Primary Source File</span></span>
* <span data-ttu-id="9343a-181">Fichier XML de liste de séquences</span><span class="sxs-lookup"><span data-stu-id="9343a-181">Clip List XML</span></span>
* <span data-ttu-id="9343a-182">Fichier/élément multimédia de sortie</span><span class="sxs-lookup"><span data-stu-id="9343a-182">Output File/Asset</span></span>  

![Nouveau workflow d’encodage](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="9343a-184">*Nouveau workflow d’encodage*</span><span class="sxs-lookup"><span data-stu-id="9343a-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="9343a-185">Pour accepter le fichier multimédia d’entrée, commencez par ajouter un composant Media File Input.</span><span class="sxs-lookup"><span data-stu-id="9343a-185">In order to accept the input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="9343a-186">Pour ajouter un composant au workflow, recherchez-le dans la zone de recherche du référentiel et faites glisser l’entrée souhaitée dans le volet du concepteur.</span><span class="sxs-lookup"><span data-stu-id="9343a-186">To add a component to the workflow, look for it in the Repository search box and drag the desired entry onto the designer pane.</span></span>

<span data-ttu-id="9343a-187">Ensuite, ajoutez le fichier vidéo à utiliser pour la conception de votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="9343a-187">Next, add the video file to be used for designing your workflow.</span></span> <span data-ttu-id="9343a-188">Pour ce faire, cliquez sur l’arrière-plan du volet du Concepteur de flux de travail et recherchez la propriété Primary Source File dans le volet des propriétés à droite.</span><span class="sxs-lookup"><span data-stu-id="9343a-188">To do so, click the background pane in Workflow Designer and look for the Primary Source File property on the right-hand property pane.</span></span> <span data-ttu-id="9343a-189">Cliquez sur l’icône de dossier et sélectionnez le fichier vidéo approprié.</span><span class="sxs-lookup"><span data-stu-id="9343a-189">Click the folder icon and select the appropriate video file.</span></span>

![Primary Source File](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="9343a-191">*Primary Source File*</span><span class="sxs-lookup"><span data-stu-id="9343a-191">*Primary File Source*</span></span>

<span data-ttu-id="9343a-192">Ensuite, spécifiez le fichier vidéo dans le composant Media File Input.</span><span class="sxs-lookup"><span data-stu-id="9343a-192">Next, specify the video file in the Media File Input component.</span></span>   

![Source Media File Input](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="9343a-194">*Source Media File Input*</span><span class="sxs-lookup"><span data-stu-id="9343a-194">*Media File Input Source*</span></span>

<span data-ttu-id="9343a-195">Une fois cette opération effectuée, le composant Media File Input inspectera le fichier et remplira ses broches de sortie afin de refléter le fichier inspecté.</span><span class="sxs-lookup"><span data-stu-id="9343a-195">As soon as this is done, the Media File Input component will inspect the file and populate its output pins to reflect the file that it inspected.</span></span>

<span data-ttu-id="9343a-196">L’étape suivante consiste à ajouter un composant «Video Data Type Updater » pour spécifier l’espace colorimétrique sur Rec.709.</span><span class="sxs-lookup"><span data-stu-id="9343a-196">The next step is to add a "Video Data Type Updater" to specify the color space to Rec.709.</span></span> <span data-ttu-id="9343a-197">Ajoutez un composant « Video Format Converter » défini sur Disposition des données/Type de disposition = Planaire configurable.</span><span class="sxs-lookup"><span data-stu-id="9343a-197">Add a "Video Format Converter" that is set to Data Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="9343a-198">Cela convertit le flux vidéo en un format pouvant être considéré comme une source du composant de superposition.</span><span class="sxs-lookup"><span data-stu-id="9343a-198">This will convert the video stream to a format that can be taken as a source of the overlay component.</span></span>

![Video Data Type Updater et Format Converter](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="9343a-200">*Video Data Type Updater et Format Converter*</span><span class="sxs-lookup"><span data-stu-id="9343a-200">*Video Data Type Updater and Format Converter*</span></span>

![Type de disposition = Planaire configurable](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<span data-ttu-id="9343a-202">*Le type de disposition est Planaire configurable*</span><span class="sxs-lookup"><span data-stu-id="9343a-202">*Layout type is Configurable Planar*</span></span>

<span data-ttu-id="9343a-203">Ensuite, ajoutez un composant Video Overlay et connectez la broche de la vidéo (Uncompressed) à la broche de la vidéo (Uncompressed) du composant Media File Input.</span><span class="sxs-lookup"><span data-stu-id="9343a-203">Next, add a Video Overlay component and connect the (uncompressed) video pin to the (uncompressed) video pin of the media file input.</span></span>

<span data-ttu-id="9343a-204">Ajoutez un autre composant Media File Input (pour charger le fichier du logo), cliquez sur ce composant et renommez-le « Logo Media File Input », puis sélectionnez une image (un fichier .png par exemple) dans la propriété de fichier.</span><span class="sxs-lookup"><span data-stu-id="9343a-204">Add another Media File Input (to load the logo file), click on this component and rename it to "Media File Input Logo", and select an image (a .png file for example) in the file property.</span></span> <span data-ttu-id="9343a-205">Connectez la broche de l’image Uncompressed à la broche de l’image Uncompressed de la superposition.</span><span class="sxs-lookup"><span data-stu-id="9343a-205">Connect the Uncompressed image pin to the Uncompressed image pin of the overlay.</span></span>

![Composant Overlay et source du fichier d’image](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="9343a-207">*Composant Overlay et source du fichier d’image*</span><span class="sxs-lookup"><span data-stu-id="9343a-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="9343a-208">Si vous souhaitez modifier la position du logo sur la vidéo (vous voulez par exemple le positionner 10 % en retrait de l’angle supérieur gauche), décochez la case « Entrée manuelle ».</span><span class="sxs-lookup"><span data-stu-id="9343a-208">If you want to modify the position of the logo on the video (for example, you might want to position it at 10 percent off of the top left corner of the video), clear the "Manual Input" check box.</span></span> <span data-ttu-id="9343a-209">Vous pouvez le faire car vous utilisez un composant Media File Input pour fournir le fichier de logo au composant de superposition.</span><span class="sxs-lookup"><span data-stu-id="9343a-209">You can do this because you are using a Media File Input to provide the logo file to the overlay component.</span></span>

![Position de superposition](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="9343a-211">*Position de superposition*</span><span class="sxs-lookup"><span data-stu-id="9343a-211">*Overlay position*</span></span>

<span data-ttu-id="9343a-212">Pour encoder le flux vidéo en H.264, ajoutez les composants AVC Video Encoder et AAC encoder à l’aire du concepteur.</span><span class="sxs-lookup"><span data-stu-id="9343a-212">To encode the video stream to H.264, add the AVC Video Encoder and AAC encoder components to the designer surface.</span></span> <span data-ttu-id="9343a-213">Connectez les broches.</span><span class="sxs-lookup"><span data-stu-id="9343a-213">Connect the pins.</span></span>
<span data-ttu-id="9343a-214">Configurez le composant AAC encoder et sélectionnez Conversion du format audio/Présélection : 2.0 (G, D).</span><span class="sxs-lookup"><span data-stu-id="9343a-214">Set up the AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![Encodeurs audio et vidéo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="9343a-216">*Encodeurs audio et vidéo*</span><span class="sxs-lookup"><span data-stu-id="9343a-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="9343a-217">Ajoutez maintenant les composants **ISO Mpeg-4 Multiplexer** et **File Output**, et connectez les broches, comme illustré.</span><span class="sxs-lookup"><span data-stu-id="9343a-217">Now add the **ISO Mpeg-4 Multiplexer** and **File Output** components and connect the pins as shown.</span></span>

![MP4 Multiplexer et File Output](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="9343a-219">*MP4 Multiplexer et File Output*</span><span class="sxs-lookup"><span data-stu-id="9343a-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="9343a-220">Vous devez définir le nom du fichier de sortie.</span><span class="sxs-lookup"><span data-stu-id="9343a-220">You need to set the name for the output file.</span></span> <span data-ttu-id="9343a-221">Cliquez sur le composant **File Output** et modifiez l’expression du fichier :</span><span class="sxs-lookup"><span data-stu-id="9343a-221">Click the **File Output** component and edit the expression for the file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Nom de sortie du fichier](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="9343a-223">*Nom de sortie du fichier*</span><span class="sxs-lookup"><span data-stu-id="9343a-223">*File output name*</span></span>

<span data-ttu-id="9343a-224">Vous pouvez exécuter le flux de travail localement pour vérifier qu’il fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="9343a-224">You can run the workflow locally to check that it is running correctly.</span></span>

<span data-ttu-id="9343a-225">Une fois terminé, vous pouvez l’exécuter dans Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="9343a-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="9343a-226">Préparez tout d’abord un élément multimédia dans Azure Media Services avec deux fichiers : le fichier vidéo et le logo.</span><span class="sxs-lookup"><span data-stu-id="9343a-226">First, prepare an asset in Azure Media Services with two files in it: the video file and the logo.</span></span> <span data-ttu-id="9343a-227">Vous pouvez pour cela utiliser l’API REST ou .NET.</span><span class="sxs-lookup"><span data-stu-id="9343a-227">You can do this by using the .NET or REST API.</span></span> <span data-ttu-id="9343a-228">Vous pouvez également le faire avec le portail Azure ou [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span><span class="sxs-lookup"><span data-stu-id="9343a-228">You can also do this by using the Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="9343a-229">Ce didacticiel vous montre comment gérer des éléments multimédias avec AMSE.</span><span class="sxs-lookup"><span data-stu-id="9343a-229">This tutorial shows you how to manage assets with AMSE.</span></span> <span data-ttu-id="9343a-230">Il existe deux façons d’ajouter des fichiers à un élément multimédia :</span><span class="sxs-lookup"><span data-stu-id="9343a-230">There are two ways to add files to an asset:</span></span>

* <span data-ttu-id="9343a-231">Créez un dossier local, copiez-y les deux fichiers et glissez-déplacez le dossier vers l’onglet **Élément multimédia** .</span><span class="sxs-lookup"><span data-stu-id="9343a-231">Create a local folder, copy the two files in it, and drag and drop the folder to the **Asset** tab.</span></span>
* <span data-ttu-id="9343a-232">Téléchargez le fichier vidéo en tant qu’élément multimédia, affichez les informations de l’élément, accédez à l’onglet Fichier, puis téléchargez un fichier supplémentaire (logo).</span><span class="sxs-lookup"><span data-stu-id="9343a-232">Upload the video file as an asset, display the asset information, go to the files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="9343a-233">Veillez à définir un fichier principal dans l’élément multimédia (le fichier vidéo principal).</span><span class="sxs-lookup"><span data-stu-id="9343a-233">Make sure to set a primary file in the asset (the main video file).</span></span>

![Fichiers d’élément multimédia dans AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="9343a-235">*Fichiers d’élément multimédia dans AMSE*</span><span class="sxs-lookup"><span data-stu-id="9343a-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="9343a-236">Sélectionnez l’élément et choisissez de l’encoder avec Premium Encoder.</span><span class="sxs-lookup"><span data-stu-id="9343a-236">Select the asset and choose to encode it with Premium Encoder.</span></span> <span data-ttu-id="9343a-237">Téléchargez le flux de travail et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="9343a-237">Upload the workflow and select it.</span></span>

<span data-ttu-id="9343a-238">Cliquez sur le bouton pour transmettre les données au processeur, puis ajoutez le code XML suivant pour définir les propriétés d’exécution :</span><span class="sxs-lookup"><span data-stu-id="9343a-238">Click the button to pass data to the processor, and add the following XML to set the runtime properties:</span></span>

![Premium Encoder dans AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="9343a-240">*Premium Encoder dans AMSE*</span><span class="sxs-lookup"><span data-stu-id="9343a-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="9343a-241">Ensuite, collez les données XML suivantes.</span><span class="sxs-lookup"><span data-stu-id="9343a-241">Then, paste the following XML data.</span></span> <span data-ttu-id="9343a-242">Vous devez spécifier le nom du fichier vidéo pour le composant Media File Input et pour la propriété primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="9343a-242">You need to specify the name of the video file for both the Media File Input and primarySourceFile.</span></span> <span data-ttu-id="9343a-243">Spécifiez le nom de fichier pour le logo.</span><span class="sxs-lookup"><span data-stu-id="9343a-243">Specify the name of the file name for the logo too.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

![setRuntimeProperties](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture20_amsexmldata.png)

<span data-ttu-id="9343a-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="9343a-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="9343a-246">Si vous utilisez le Kit de développement logiciel (SDK) .NET pour créer et exécuter la tâche, ces données XML doivent être transmises en tant que chaîne de configuration.</span><span class="sxs-lookup"><span data-stu-id="9343a-246">If you use the .NET SDK to create and run the task, this XML data has to be passed as the configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="9343a-247">Une fois la tâche effectuée, le fichier MP4 dans l’élément de sortie affiche la superposition.</span><span class="sxs-lookup"><span data-stu-id="9343a-247">After the job is complete, the MP4 file in the output asset displays the overlay!</span></span>

![Superposition sur la vidéo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="9343a-249">*Superposition sur la vidéo*</span><span class="sxs-lookup"><span data-stu-id="9343a-249">*Overlay on the video*</span></span>

<span data-ttu-id="9343a-250">Vous pouvez télécharger l’exemple de flux de travail sur [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span><span class="sxs-lookup"><span data-stu-id="9343a-250">You can download the sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="9343a-251">Exemple 2 : Encodage de plusieurs langues audio</span><span class="sxs-lookup"><span data-stu-id="9343a-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="9343a-252">Vous trouverez un exemple de workflow d’encodage de plusieurs langues audio dans [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span><span class="sxs-lookup"><span data-stu-id="9343a-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="9343a-253">Ce dossier contient un exemple de workflow qui peut être utilisé pour encoder un fichier MXF en une ressource contenant plusieurs fichiers MP4 avec plusieurs pistes audio.</span><span class="sxs-lookup"><span data-stu-id="9343a-253">This folder contains a sample workflow which can be used to encode a MXF file to a multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="9343a-254">Ce workflow suppose que le fichier MXF contient une piste audio. Les pistes audio supplémentaires doivent être transmises en tant que fichiers audio distincts (WAV ou MP4...).</span><span class="sxs-lookup"><span data-stu-id="9343a-254">This workflow assumes that the MXF file contains one audio track ; the additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="9343a-255">Pour effectuer l’encodage, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9343a-255">To encode, please follow these steps:</span></span>

* <span data-ttu-id="9343a-256">Créez une ressource Media Services avec le fichier MXF et les fichiers audio (de 0 à 18 fichiers audio).</span><span class="sxs-lookup"><span data-stu-id="9343a-256">Create a Media Services asset with the MXF file and the Audio files (0 to 18 audio files).</span></span>
* <span data-ttu-id="9343a-257">Assurez-vous que le fichier MXF est défini comme fichier principal.</span><span class="sxs-lookup"><span data-stu-id="9343a-257">Make sure that the MXF file is set as a primary file.</span></span>
* <span data-ttu-id="9343a-258">Créez un travail et une tâche à l’aide du processeur de workflow d’encodeur premium.</span><span class="sxs-lookup"><span data-stu-id="9343a-258">Create a job and a task using the Premium Workflow Encoder processor.</span></span> <span data-ttu-id="9343a-259">Utilisez le workflow fourni (MultiMP4-1080p-19audio-v1.workflow).</span><span class="sxs-lookup"><span data-stu-id="9343a-259">Use the workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="9343a-260">Transmettez les données setruntime.xml à la tâche (si vous utilisez Azure Media Services Explorer, utilisez le bouton « Transmettre les données xml au workflow »).</span><span class="sxs-lookup"><span data-stu-id="9343a-260">Pass the setruntime.xml data to the task (if you use Azure Media Services Explorer, use the “pass xml data to the workflow” button).</span></span>
  * <span data-ttu-id="9343a-261">Mettez à jour les données XML pour spécifier les noms de fichier et balises de langues corrects.</span><span class="sxs-lookup"><span data-stu-id="9343a-261">Please update the XML data to specify the correct file names and languages tags.</span></span>
  * <span data-ttu-id="9343a-262">Le workflow comporte des éléments audio nommés de Audio 1 à Audio 18.</span><span class="sxs-lookup"><span data-stu-id="9343a-262">The workflow has audio components named Audio 1 to Audio 18.</span></span>
  * <span data-ttu-id="9343a-263">RFC5646 est pris en charge pour la balise de langue.</span><span class="sxs-lookup"><span data-stu-id="9343a-263">RFC5646 is supported for the language tag.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
<transcodeRequest>
  <setRuntimeProperties>
    <property propertyPath="Media File Input Video/filename" value="MainVideo.mxf" />
    <property propertyPath="Language/language_code" value="en" />
    <property propertyPath="/primarySourceFile" value="MainVideo.mxf" />
    <property propertyPath="Audio 1/Media File Input/filename" value="french-audio.wav" />
    <property propertyPath="Audio 1/Language/language_code" value="fr" />
    <property propertyPath="Audio 2/Media File Input/filename" value="german-audio.wav" />
    <property propertyPath="Audio 2/Language/language_code" value="de" />
    <property propertyPath="Audio 3/Media File Input/filename" value="japanese-audio.wav" />
    <property propertyPath="Audio 3/Language/language_code" value="ja" />
  </setRuntimeProperties>
</transcodeRequest>
```

* <span data-ttu-id="9343a-264">La ressource encodée contiendra des pistes audio en plusieurs langues, qui doivent être sélectionnables dans Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="9343a-264">The encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="9343a-265">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9343a-265">See also</span></span>
* [<span data-ttu-id="9343a-266">Présentation de l’encodage Premium dans Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="9343a-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="9343a-267">Utilisation de l’encodage Premium dans Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="9343a-267">How to use Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="9343a-268">Encodage de contenu à la demande avec Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="9343a-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="9343a-269">Codecs et formats de Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="9343a-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="9343a-270">Exemples de fichiers de workflow</span><span class="sxs-lookup"><span data-stu-id="9343a-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="9343a-271">Outil Azure Media Services Explorer</span><span class="sxs-lookup"><span data-stu-id="9343a-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="9343a-272">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="9343a-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="9343a-273">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="9343a-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
