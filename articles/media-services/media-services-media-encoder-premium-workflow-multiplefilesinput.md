---
title: "aaaMultiple d’entrée des fichiers et des propriétés de composant avec l’encodeur Premium - Azure | Documents Microsoft"
description: "Cette rubrique explique comment toouse setRuntimeProperties toouse entrée plusieurs fichiers et passer le processeur multimédia de données personnalisé toohello Workflow d’encodeur multimédia Premium."
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
ms.openlocfilehash: e14d10fbf9669e0b88e5ba1c519f1ba5e0bafdd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="f5029-103">Utilisation de plusieurs fichiers d’entrée et propriétés du composant avec Premium Encoder</span><span class="sxs-lookup"><span data-stu-id="f5029-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="f5029-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f5029-104">Overview</span></span>
<span data-ttu-id="f5029-105">Il existe des scénarios dans lesquels vous devrez peut-être toocustomize propriétés du composant, spécifiez l’élément XML de liste contenu ou envoyer plusieurs fichiers d’entrée lorsque vous soumettez une tâche avec hello **Workflow d’encodeur multimédia Premium** processeur multimédia.</span><span class="sxs-lookup"><span data-stu-id="f5029-105">There are scenarios in which you might need toocustomize component properties, specify Clip List XML content, or send multiple input files when you submit a task with hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="f5029-106">Voici quelques exemples :</span><span class="sxs-lookup"><span data-stu-id="f5029-106">Some examples are:</span></span>

* <span data-ttu-id="f5029-107">Superposition vidéo de texte et en définissant la valeur de texte de hello (par exemple, date du jour hello) lors de l’exécution pour chaque vidéo d’entrée.</span><span class="sxs-lookup"><span data-stu-id="f5029-107">Overlaying text on video and setting hello text value (for example, hello current date) at runtime for each input video.</span></span>
* <span data-ttu-id="f5029-108">Personnalisation de hello Clip liste XML (toospecify de source d’un ou plusieurs fichiers, avec ou sans limitation, etc.).</span><span class="sxs-lookup"><span data-stu-id="f5029-108">Customizing hello Clip List XML (toospecify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="f5029-109">Recouvrir une image de logo sur vidéo d’entrée de hello tandis que hello vidéo est encodée.</span><span class="sxs-lookup"><span data-stu-id="f5029-109">Overlaying a logo image on hello input video while hello video is encoded.</span></span>
* <span data-ttu-id="f5029-110">Encodage de plusieurs langues audio.</span><span class="sxs-lookup"><span data-stu-id="f5029-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="f5029-111">toolet hello **Workflow d’encodeur multimédia Premium** savez que vous modifiez certaines propriétés dans le flux de travail hello lorsque vous créez la tâche hello ou que vous envoyez plusieurs fichiers d’entrée, vous avez une chaîne de configuration qui contient toouse  **setRuntimeProperties** et/ou **transcodeSource**.</span><span class="sxs-lookup"><span data-stu-id="f5029-111">toolet hello **Media Encoder Premium Workflow** know that you are changing some properties in hello workflow when you create hello task or send multiple input files, you have toouse a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="f5029-112">Cette rubrique explique comment toouse les.</span><span class="sxs-lookup"><span data-stu-id="f5029-112">This topic explains how toouse them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="f5029-113">Syntaxe de chaîne de configuration</span><span class="sxs-lookup"><span data-stu-id="f5029-113">Configuration string syntax</span></span>
<span data-ttu-id="f5029-114">tooset de chaîne de configuration Hello Bonjour encodage tâche utilise un document XML qui ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="f5029-114">hello configuration string tooset in hello encoding task uses an XML document that looks like this:</span></span>

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

<span data-ttu-id="f5029-115">Hello Voici le code hello c# qui lit un fichier de configuration XML hello, mettez-le à jour avec hello du nom de fichier vidéo et le passe toohello tâche dans un projet :</span><span class="sxs-lookup"><span data-stu-id="f5029-115">hello following is hello C# code that reads hello XML configuration from a file, update it with hello right video filename and passes it toohello task in a job:</span></span>

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass tooit hello name of hello 
// processor toouse for hello specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with hello encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify hello input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset toocontain hello results of hello job. 
// This output is specified as AssetCreationOptions.None, which 
// means hello output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a><span data-ttu-id="f5029-116">Personnalisation des propriétés du composant</span><span class="sxs-lookup"><span data-stu-id="f5029-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="f5029-117">Propriété avec une valeur simple</span><span class="sxs-lookup"><span data-stu-id="f5029-117">Property with a simple value</span></span>
<span data-ttu-id="f5029-118">Dans certains cas, il est utile toocustomize une propriété de composant avec le fichier de flux de travail hello qui est en train de toobe exécutée par le Workflow d’encodeur multimédia Premium.</span><span class="sxs-lookup"><span data-stu-id="f5029-118">In some cases, it is useful toocustomize a component property together with hello workflow file that is going toobe executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="f5029-119">Supposons que vous conçu un flux de travail que le texte superpositions sur vos vidéos, le texte hello (par exemple, date du jour hello) est supposé toobe ensemble lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="f5029-119">Suppose you designed a workflow that overlays text on your videos, and hello text (for example, hello current date) is supposed toobe set at runtime.</span></span> <span data-ttu-id="f5029-120">Pour cela, en envoyant toobe de texte hello définissez en tant que hello nouvelle valeur de propriété de texte hello du composant de superposition hello hello tâche de codage.</span><span class="sxs-lookup"><span data-stu-id="f5029-120">You can do this by sending hello text toobe set as hello new value for hello text property of hello overlay component from hello encoding task.</span></span> <span data-ttu-id="f5029-121">Vous pouvez utiliser ce mécanisme toochange autres propriétés d’un composant dans le flux de travail hello (par exemple hello position ou les couleurs de superposition de hello, hello de vitesse de transmission de l’encodeur de hello AVC, etc..).</span><span class="sxs-lookup"><span data-stu-id="f5029-121">You can use this mechanism toochange other properties of a component in hello workflow (such as hello position or color of hello overlay, hello bitrate of hello AVC encoder, etc.).</span></span>

<span data-ttu-id="f5029-122">**setRuntimeProperties** est toooverride utilisé une propriété dans les composants de flux de travail hello hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-122">**setRuntimeProperties** is used toooverride a property in hello components of hello workflow.</span></span>

<span data-ttu-id="f5029-123">Exemple :</span><span class="sxs-lookup"><span data-stu-id="f5029-123">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text tooImage Converter/text" value="Today is Friday hello 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a><span data-ttu-id="f5029-124">Propriété avec une valeur XML</span><span class="sxs-lookup"><span data-stu-id="f5029-124">Property with an XML value</span></span>
<span data-ttu-id="f5029-125">encapsuler des tooset une propriété qui attend une valeur XML, à l’aide de `<![CDATA[ and ]]>`.</span><span class="sxs-lookup"><span data-stu-id="f5029-125">tooset a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="f5029-126">Exemple :</span><span class="sxs-lookup"><span data-stu-id="f5029-126">Example:</span></span>

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
> <span data-ttu-id="f5029-127">Vérifiez que pas tooput chariot retournent juste après `<![CDATA[`.</span><span class="sxs-lookup"><span data-stu-id="f5029-127">Make sure not tooput a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="f5029-128">Valeur propertyPath</span><span class="sxs-lookup"><span data-stu-id="f5029-128">propertyPath value</span></span>
<span data-ttu-id="f5029-129">Dans les exemples précédents hello, hello propertyPath était « / du fichier multimédia/nom de fichier d’entrée » ou « / inactiveTimeout » ou « clipListXml ».</span><span class="sxs-lookup"><span data-stu-id="f5029-129">In hello previous examples, hello propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="f5029-130">Il s’agit, en général, nom hello du composant de hello, puis nom hello de propriété de hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-130">This is, in general, hello name of hello component, then hello name of hello property.</span></span> <span data-ttu-id="f5029-131">Hello chemin d’accès peut avoir des niveaux plus ou moins, tel que « / primarySourceFile » (hello propriété étant à la racine hello hello de flux de travail) ou « / vidéo/opacité de traitement/graphique » (car hello superposition est dans un groupe).</span><span class="sxs-lookup"><span data-stu-id="f5029-131">hello path can have more or fewer levels, like "/primarySourceFile" (because hello property is at hello root of hello workflow) or "/Video Processing/Graphic Overlay/Opacity" (because hello Overlay is in a group).</span></span>    

<span data-ttu-id="f5029-132">toocheck hello chemin d’accès au nom de propriété, utilisez bouton d’action hello située juste à côté de chaque propriété.</span><span class="sxs-lookup"><span data-stu-id="f5029-132">toocheck hello path and property name, use hello action button that is immediately beside each property.</span></span> <span data-ttu-id="f5029-133">Vous pouvez cliquer sur ce bouton d’action et sélectionner **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="f5029-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="f5029-134">Cette opération affiche vous hello réelle de nom de propriété de hello et immédiatement au-dessus d’elle, hello d’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="f5029-134">This will show you hello actual name of hello property, and immediately above it, hello namespace.</span></span>

![Action/Modifier](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Propriété](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="f5029-137">Fichiers d’entrée multiples</span><span class="sxs-lookup"><span data-stu-id="f5029-137">Multiple input files</span></span>
<span data-ttu-id="f5029-138">Chaque tâche que vous envoyez toohello **Workflow d’encodeur multimédia Premium** nécessite deux composants :</span><span class="sxs-lookup"><span data-stu-id="f5029-138">Each task that you submit toohello **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="f5029-139">Bonjour tout d’abord un est un *actif du flux de travail* qui contient un fichier de flux de travail.</span><span class="sxs-lookup"><span data-stu-id="f5029-139">hello first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="f5029-140">Vous pouvez concevoir des fichiers de flux de travail à l’aide de hello [le Concepteur de flux de travail](media-services-workflow-designer.md).</span><span class="sxs-lookup"><span data-stu-id="f5029-140">You can design workflow files by using hello [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="f5029-141">Hello second est un *multimédia* qui contient des fichiers de support hello que vous souhaitez tooencode.</span><span class="sxs-lookup"><span data-stu-id="f5029-141">hello second one is a *Media Asset* that contains hello media file(s) that you want tooencode.</span></span>

<span data-ttu-id="f5029-142">Lorsque vous envoyez plusieurs toohello de fichiers de support **Workflow d’encodeur multimédia Premium** hello suivant des contraintes d’encodeur, applique :</span><span class="sxs-lookup"><span data-stu-id="f5029-142">When you're sending multiple media files toohello **Media Encoder Premium Workflow** encoder, hello following constraints apply:</span></span>

* <span data-ttu-id="f5029-143">Tous les supports hello fichiers doivent être hello même *multimédia*.</span><span class="sxs-lookup"><span data-stu-id="f5029-143">All hello media files must be in hello same *Media Asset*.</span></span> <span data-ttu-id="f5029-144">L’utilisation de plusieurs éléments multimédias n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="f5029-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="f5029-145">Vous devez définir le fichier primaire de hello dans cet élément multimédia Media (dans l’idéal, il s’agit de hello principal fichier vidéo hello encodeur est demandé tooprocess).</span><span class="sxs-lookup"><span data-stu-id="f5029-145">You must set hello primary file in this Media Asset (ideally, this is hello main video file that hello encoder is asked tooprocess).</span></span>
* <span data-ttu-id="f5029-146">Il s’agit des données de configuration nécessaires toopass inclut hello **setRuntimeProperties** et/ou **transcodeSource** processeur de toohello d’élément.</span><span class="sxs-lookup"><span data-stu-id="f5029-146">It is necessary toopass configuration data that includes hello **setRuntimeProperties** and/or **transcodeSource** element toohello processor.</span></span>
  * <span data-ttu-id="f5029-147">**setRuntimeProperties** est la propriété de nom de fichier utilisé toooverride hello ou une autre propriété dans les composants de flux de travail hello hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-147">**setRuntimeProperties** is used toooverride hello filename property or another property in hello components of hello workflow.</span></span>
  * <span data-ttu-id="f5029-148">**transcodeSource** est utilisé toospecify hello contenu XML de liste de découpage.</span><span class="sxs-lookup"><span data-stu-id="f5029-148">**transcodeSource** is used toospecify hello Clip List XML content.</span></span>

<span data-ttu-id="f5029-149">Connexions dans le flux de travail hello :</span><span class="sxs-lookup"><span data-stu-id="f5029-149">Connections in hello workflow:</span></span>

* <span data-ttu-id="f5029-150">Si vous utilisez un ou plusieurs composants d’entrée de fichier de média et que vous prévoyez de toouse **setRuntimeProperties** toospecify hello du nom de fichier, puis ne se connectent pas hello fichier principal composant pin toothem.</span><span class="sxs-lookup"><span data-stu-id="f5029-150">If you use one or several Media File Input components and plan toouse **setRuntimeProperties** toospecify hello file name, then do not connect hello primary file component pin toothem.</span></span> <span data-ttu-id="f5029-151">Assurez-vous qu’il n’existe aucune connexion entre objet du fichier primaire hello et hello Media fichier que les entrées.</span><span class="sxs-lookup"><span data-stu-id="f5029-151">Make sure that there is no connection between hello primary file object and hello Media File Input(s).</span></span>
* <span data-ttu-id="f5029-152">Si vous préférez toouse Clip liste XML et un composant de Source de média, puis vous pouvez connecter les deux ensemble.</span><span class="sxs-lookup"><span data-stu-id="f5029-152">If you prefer toouse Clip List XML and one Media Source component, then you can connect both together.</span></span>

![Aucune connexion à partir du fichier Source principal tooMedia fichier d’entrée](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="f5029-154">*Il n’existe aucune connexion à partir du fichier primaire de hello tooMedia détecté (s) du fichier d’entrée si vous utilisez la propriété de nom de fichier setRuntimeProperties tooset hello.*</span><span class="sxs-lookup"><span data-stu-id="f5029-154">*There is no connection from hello primary file tooMedia File Input component(s) if you use setRuntimeProperties tooset hello filename property.*</span></span>

![Connexion à partir de la liste XML tooClip liste Source](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="f5029-156">*Vous pouvez connecter la liste XML tooMedia Source et utiliser transcodeSource.*</span><span class="sxs-lookup"><span data-stu-id="f5029-156">*You can connect Clip List XML tooMedia Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="f5029-157">Personnalisation du fichier XML de liste de séquences</span><span class="sxs-lookup"><span data-stu-id="f5029-157">Clip List XML customization</span></span>
<span data-ttu-id="f5029-158">Vous pouvez spécifier hello XML de liste de découpage dans un flux de travail hello lors de l’exécution à l’aide de **transcodeSource** dans la configuration de hello chaîne XML.</span><span class="sxs-lookup"><span data-stu-id="f5029-158">You can specify hello Clip List XML in hello workflow at runtime by using **transcodeSource** in hello configuration string XML.</span></span> <span data-ttu-id="f5029-159">Cela requiert épingler le hello XML de liste de découpage toobe connecté Source de média toohello composant dans le flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-159">This requires hello Clip List XML pin toobe connected toohello Media Source component in hello workflow.</span></span>

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

<span data-ttu-id="f5029-160">Si vous souhaitez toouse de /primarySourceFile toospecify cette sortie de hello tooname propriété fichiers à l’aide de « Expressions », nous vous recommandons de passer hello Clip liste XML en tant que propriété *après* propriété /primarySourceFile de hello, tooavoid Liste des images ayant hello être remplacée par le paramètre de /primarySourceFile hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-160">If you want toospecify /primarySourceFile toouse this property tooname hello output files by using 'Expressions', then we recommend passing hello Clip List XML as a property *after* hello /primarySourceFile property, tooavoid having hello Clip List be overridden by hello /primarySourceFile setting.</span></span>

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

<span data-ttu-id="f5029-161">Avec découpage précis de la trame supplémentaire :</span><span class="sxs-lookup"><span data-stu-id="f5029-161">With additional frame-accurate trimming:</span></span>

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

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a><span data-ttu-id="f5029-162">Exemple 1 : Superposer une image sur hello vidéo</span><span class="sxs-lookup"><span data-stu-id="f5029-162">Example 1 : Overlay an image on top of hello video</span></span>

### <a name="presentation"></a><span data-ttu-id="f5029-163">Présentation</span><span class="sxs-lookup"><span data-stu-id="f5029-163">Presentation</span></span>
<span data-ttu-id="f5029-164">Envisagez un exemple dans lequel vous souhaitez toooverlay une image de logo sur vidéo d’entrée de hello tandis que hello vidéo est encodée.</span><span class="sxs-lookup"><span data-stu-id="f5029-164">Consider an example in which you want toooverlay a logo image on hello input video while hello video is encoded.</span></span> <span data-ttu-id="f5029-165">Dans cet exemple, vidéo d’entrée de hello est nommé « Microsoft_HoloLens_Possibilities_816p24.mp4 » et le logo de hello est nommé « logo.png ».</span><span class="sxs-lookup"><span data-stu-id="f5029-165">In this example, hello input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and hello logo is named "logo.png".</span></span> <span data-ttu-id="f5029-166">Vous devez exécuter hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f5029-166">You should perform hello following steps:</span></span>

* <span data-ttu-id="f5029-167">Créer un composant de flux de travail avec le fichier de flux de travail de hello (voir hello exemple suivant).</span><span class="sxs-lookup"><span data-stu-id="f5029-167">Create a Workflow Asset with hello workflow file (see hello following example).</span></span>
* <span data-ttu-id="f5029-168">Créer une ressource multimédia, qui contient deux fichiers : MyInputVideo.mp4 comme hello fichier primaire et MyLogo.png.</span><span class="sxs-lookup"><span data-stu-id="f5029-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as hello primary file and MyLogo.png.</span></span>
* <span data-ttu-id="f5029-169">Envoyer un toohello tâche multimédia de Workflow d’encodeur multimédia Premium ressources du processeur par hello ci-dessus d’entrée et spécifier des hello suivant de chaîne de configuration.</span><span class="sxs-lookup"><span data-stu-id="f5029-169">Send a task toohello Media Encoder Premium Workflow media processor with hello above input assets and specify hello following configuration string.</span></span>

<span data-ttu-id="f5029-170">Configuration :</span><span class="sxs-lookup"><span data-stu-id="f5029-170">Configuration:</span></span>

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

<span data-ttu-id="f5029-171">Dans l’exemple hello ci-dessus, hello le nom de fichier vidéo de hello est envoyé toohello entrée de fichier de média composant hello primarySourceFile propriété.</span><span class="sxs-lookup"><span data-stu-id="f5029-171">In hello example above, hello name of hello video file is sent toohello Media File Input component and hello primarySourceFile property.</span></span> <span data-ttu-id="f5029-172">nom de Hello du fichier de logo hello est envoyé tooanother entrée de fichier de média qui est le composant de superposition graphique toohello connecté.</span><span class="sxs-lookup"><span data-stu-id="f5029-172">hello name of hello logo file is sent tooanother Media File Input that is connected toohello graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="f5029-173">nom de fichier vidéo Hello est envoyée toohello primarySourceFile propriété.</span><span class="sxs-lookup"><span data-stu-id="f5029-173">hello video file name is sent toohello primarySourceFile property.</span></span> <span data-ttu-id="f5029-174">Hello raison à cela est toouse cette propriété dans le flux de travail hello pour la génération du nom de fichier de sortie correcte hello à l’aide d’Expressions, par exemple.</span><span class="sxs-lookup"><span data-stu-id="f5029-174">hello reason for this is toouse this property in hello workflow for building hello correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="f5029-175">Procédure de création de workflow pas à pas</span><span class="sxs-lookup"><span data-stu-id="f5029-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="f5029-176">Voici hello étapes toocreate un workflow qui utilise deux fichiers comme entrée : une vidéo et une image.</span><span class="sxs-lookup"><span data-stu-id="f5029-176">Here are hello steps toocreate a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="f5029-177">Il sera superposer les images hello hello vidéo.</span><span class="sxs-lookup"><span data-stu-id="f5029-177">It will overlay hello image on top of hello video.</span></span>

<span data-ttu-id="f5029-178">Ouvrez **Concepteur de flux de travail** et sélectionnez **Fichier** > **Nouvel espace de travail** > **Plan de transcodage**.</span><span class="sxs-lookup"><span data-stu-id="f5029-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="f5029-179">nouveau flux de travail Hello montre trois éléments :</span><span class="sxs-lookup"><span data-stu-id="f5029-179">hello new workflow shows three elements:</span></span>

* <span data-ttu-id="f5029-180">Fichier source principal</span><span class="sxs-lookup"><span data-stu-id="f5029-180">Primary Source File</span></span>
* <span data-ttu-id="f5029-181">Fichier XML de liste de séquences</span><span class="sxs-lookup"><span data-stu-id="f5029-181">Clip List XML</span></span>
* <span data-ttu-id="f5029-182">Fichier/élément multimédia de sortie</span><span class="sxs-lookup"><span data-stu-id="f5029-182">Output File/Asset</span></span>  

![Nouveau workflow d’encodage](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="f5029-184">*Nouveau workflow d’encodage*</span><span class="sxs-lookup"><span data-stu-id="f5029-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="f5029-185">Dans le fichier de média d’entrée de commande tooaccept hello commencez par ajouter un composant Media fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="f5029-185">In order tooaccept hello input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="f5029-186">tooadd un flux de travail toohello du composant, regardez dans la zone de recherche du référentiel hello et faites glisser d’entrée de hello souhaité sur le volet de concepteur hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-186">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span>

<span data-ttu-id="f5029-187">Ensuite, ajoutez toobe de fichier vidéo hello utilisée pour la conception de votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="f5029-187">Next, add hello video file toobe used for designing your workflow.</span></span> <span data-ttu-id="f5029-188">Par conséquent, les toodo sur le volet d’arrière-plan hello dans le Concepteur de flux de travail et recherchez propriété du fichier Source principal hello sur le volet de droite propriété hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-188">toodo so, click hello background pane in Workflow Designer and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="f5029-189">Cliquez sur icône du dossier hello et sélectionnez le fichier vidéo approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-189">Click hello folder icon and select hello appropriate video file.</span></span>

![Primary Source File](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="f5029-191">*Primary Source File*</span><span class="sxs-lookup"><span data-stu-id="f5029-191">*Primary File Source*</span></span>

<span data-ttu-id="f5029-192">Ensuite, spécifiez le fichier vidéo de hello dans le composant d’entrée de fichier de média hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-192">Next, specify hello video file in hello Media File Input component.</span></span>   

![Source Media File Input](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="f5029-194">*Source Media File Input*</span><span class="sxs-lookup"><span data-stu-id="f5029-194">*Media File Input Source*</span></span>

<span data-ttu-id="f5029-195">Dès que cette opération est effectuée, composant de support, fichier d’entrée hello inspecter le fichier de hello et remplir ses codes confidentiels tooreflect hello fichier de sortie il inspecté.</span><span class="sxs-lookup"><span data-stu-id="f5029-195">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file that it inspected.</span></span>

<span data-ttu-id="f5029-196">étape suivante de Hello est tooadd un tooRec.709 espace de couleur « Updater de Type de données vidéo » toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-196">hello next step is tooadd a "Video Data Type Updater" toospecify hello color space tooRec.709.</span></span> <span data-ttu-id="f5029-197">Ajouter un « vidéo Format convertisseur » qui a le type de disposition/disposition tooData = PLANAIRE Configurable.</span><span class="sxs-lookup"><span data-stu-id="f5029-197">Add a "Video Format Converter" that is set tooData Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="f5029-198">Cela convertira hello flux vidéo tooa format qui peut être considéré comme une source de composant de superposition hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-198">This will convert hello video stream tooa format that can be taken as a source of hello overlay component.</span></span>

![Video Data Type Updater et Format Converter](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="f5029-200">*Video Data Type Updater et Format Converter*</span><span class="sxs-lookup"><span data-stu-id="f5029-200">*Video Data Type Updater and Format Converter*</span></span>

![Type de disposition = Planaire configurable](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<span data-ttu-id="f5029-202">*Le type de disposition est Planaire configurable*</span><span class="sxs-lookup"><span data-stu-id="f5029-202">*Layout type is Configurable Planar*</span></span>

<span data-ttu-id="f5029-203">Ensuite, ajoutez un composant de la superposition vidéo et se connecter hello (non compressé) vidéo broche toohello (non compressé) vidéo broche d’entrée de fichier de média hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-203">Next, add a Video Overlay component and connect hello (uncompressed) video pin toohello (uncompressed) video pin of hello media file input.</span></span>

<span data-ttu-id="f5029-204">Ajouter un autre support de fichier d’entrée (fichier de logo tooload hello), cliquez sur ce composant et renommez-le trop « Support fichier d’entrée Logo », puis sélectionnez une image (un fichier .png par exemple) dans la propriété de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-204">Add another Media File Input (tooload hello logo file), click on this component and rename it too"Media File Input Logo", and select an image (a .png file for example) in hello file property.</span></span> <span data-ttu-id="f5029-205">Se connecter hello image non compressés broche toohello image non compressés broche de superposition de hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-205">Connect hello Uncompressed image pin toohello Uncompressed image pin of hello overlay.</span></span>

![Composant Overlay et source du fichier d’image](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="f5029-207">*Composant Overlay et source du fichier d’image*</span><span class="sxs-lookup"><span data-stu-id="f5029-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="f5029-208">Si vous souhaitez que la position de hello toomodify du logo hello vidéo de hello (par exemple, vous pourriez tooposition à 10 pour cent sur les haut hello coin inférieur gauche de vidéo de hello), désactivez case à cocher « Entrée manuelle » hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-208">If you want toomodify hello position of hello logo on hello video (for example, you might want tooposition it at 10 percent off of hello top left corner of hello video), clear hello "Manual Input" check box.</span></span> <span data-ttu-id="f5029-209">Pour cela, car vous utilisez un composant de segment de recouvrement toohello du fichier de logo entrée de fichier de média tooprovide hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-209">You can do this because you are using a Media File Input tooprovide hello logo file toohello overlay component.</span></span>

![Position de superposition](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="f5029-211">*Position de superposition*</span><span class="sxs-lookup"><span data-stu-id="f5029-211">*Overlay position*</span></span>

<span data-ttu-id="f5029-212">tooencode hello flux vidéo tooH.264, ajoutez hello encodeur de vidéo AVC et l’aire du Concepteur de composants toohello encodeur AAC.</span><span class="sxs-lookup"><span data-stu-id="f5029-212">tooencode hello video stream tooH.264, add hello AVC Video Encoder and AAC encoder components toohello designer surface.</span></span> <span data-ttu-id="f5029-213">Connecter des codes confidentiels hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-213">Connect hello pins.</span></span>
<span data-ttu-id="f5029-214">Définissez encodeur AAC de hello et sélectionnez la Conversion de Format Audio/présélection : 2.0 (L, R).</span><span class="sxs-lookup"><span data-stu-id="f5029-214">Set up hello AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![Encodeurs audio et vidéo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="f5029-216">*Encodeurs audio et vidéo*</span><span class="sxs-lookup"><span data-stu-id="f5029-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="f5029-217">Ajoutez maintenant hello **ISO Mpeg-4 multiplexeur** et **fichier de sortie** composants et se connecter à des codes confidentiels hello comme indiqué.</span><span class="sxs-lookup"><span data-stu-id="f5029-217">Now add hello **ISO Mpeg-4 Multiplexer** and **File Output** components and connect hello pins as shown.</span></span>

![MP4 Multiplexer et File Output](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="f5029-219">*MP4 Multiplexer et File Output*</span><span class="sxs-lookup"><span data-stu-id="f5029-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="f5029-220">Vous devez tooset hello nom hello fichier de sortie.</span><span class="sxs-lookup"><span data-stu-id="f5029-220">You need tooset hello name for hello output file.</span></span> <span data-ttu-id="f5029-221">Cliquez sur hello **fichier de sortie** composant et modifier l’expression hello pour le fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="f5029-221">Click hello **File Output** component and edit hello expression for hello file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Nom de sortie du fichier](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="f5029-223">*Nom de sortie du fichier*</span><span class="sxs-lookup"><span data-stu-id="f5029-223">*File output name*</span></span>

<span data-ttu-id="f5029-224">Vous pouvez exécuter des flux de travail hello localement toocheck qu’elle s’exécute correctement.</span><span class="sxs-lookup"><span data-stu-id="f5029-224">You can run hello workflow locally toocheck that it is running correctly.</span></span>

<span data-ttu-id="f5029-225">Une fois terminé, vous pouvez l’exécuter dans Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="f5029-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="f5029-226">Tout d’abord, préparez un élément multimédia dans Azure Media Services avec deux fichiers : les fichiers vidéo hello et logo de hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-226">First, prepare an asset in Azure Media Services with two files in it: hello video file and hello logo.</span></span> <span data-ttu-id="f5029-227">Pour cela, à l’aide des API hello .NET ou REST.</span><span class="sxs-lookup"><span data-stu-id="f5029-227">You can do this by using hello .NET or REST API.</span></span> <span data-ttu-id="f5029-228">Également procéder à l’aide de hello portail Azure ou [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span><span class="sxs-lookup"><span data-stu-id="f5029-228">You can also do this by using hello Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="f5029-229">Ce didacticiel vous montre comment les ressources toomanage avec AMSE.</span><span class="sxs-lookup"><span data-stu-id="f5029-229">This tutorial shows you how toomanage assets with AMSE.</span></span> <span data-ttu-id="f5029-230">Il existe tooan actif de deux façons tooadd fichiers :</span><span class="sxs-lookup"><span data-stu-id="f5029-230">There are two ways tooadd files tooan asset:</span></span>

* <span data-ttu-id="f5029-231">Créez un dossier local, copiez des fichiers de hello deux et faites glisser hello dossier toohello **Asset** onglet.</span><span class="sxs-lookup"><span data-stu-id="f5029-231">Create a local folder, copy hello two files in it, and drag and drop hello folder toohello **Asset** tab.</span></span>
* <span data-ttu-id="f5029-232">Télécharger le fichier vidéo de hello comme composant, afficher des informations de ressource hello, accédez de fichiers (onglet) toohello et télécharger un fichier supplémentaire (logo).</span><span class="sxs-lookup"><span data-stu-id="f5029-232">Upload hello video file as an asset, display hello asset information, go toohello files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="f5029-233">Assurez-vous que tooset un fichier primaire actif d’hello (fichier vidéo principal hello).</span><span class="sxs-lookup"><span data-stu-id="f5029-233">Make sure tooset a primary file in hello asset (hello main video file).</span></span>

![Fichiers d’élément multimédia dans AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="f5029-235">*Fichiers d’élément multimédia dans AMSE*</span><span class="sxs-lookup"><span data-stu-id="f5029-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="f5029-236">Sélectionnez hello actif et choisissez tooencode avec l’encodeur Premium.</span><span class="sxs-lookup"><span data-stu-id="f5029-236">Select hello asset and choose tooencode it with Premium Encoder.</span></span> <span data-ttu-id="f5029-237">Télécharger les flux de travail hello et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="f5029-237">Upload hello workflow and select it.</span></span>

<span data-ttu-id="f5029-238">Cliquez sur le processeur toohello données hello bouton toopass et ajoutez hello XML tooset hello runtime propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="f5029-238">Click hello button toopass data toohello processor, and add hello following XML tooset hello runtime properties:</span></span>

![Premium Encoder dans AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="f5029-240">*Premium Encoder dans AMSE*</span><span class="sxs-lookup"><span data-stu-id="f5029-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="f5029-241">Ensuite, copiez les données XML suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-241">Then, paste hello following XML data.</span></span> <span data-ttu-id="f5029-242">Vous avez besoin de nom de hello toospecify de fichier vidéo de hello pour hello entrée de fichier de média et primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="f5029-242">You need toospecify hello name of hello video file for both hello Media File Input and primarySourceFile.</span></span> <span data-ttu-id="f5029-243">Spécifiez le nom hello hello du nom de fichier pour le logo de hello trop.</span><span class="sxs-lookup"><span data-stu-id="f5029-243">Specify hello name of hello file name for hello logo too.</span></span>

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

<span data-ttu-id="f5029-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="f5029-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="f5029-246">Si vous utilisez toocreate du Kit de développement .NET hello et exécuter la tâche hello, ces données XML toobe passé en tant que chaîne de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-246">If you use hello .NET SDK toocreate and run hello task, this XML data has toobe passed as hello configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="f5029-247">Une fois le travail de hello terminée, fichier hello MP4 Bonjour sortie asset affiche le segment de recouvrement hello !</span><span class="sxs-lookup"><span data-stu-id="f5029-247">After hello job is complete, hello MP4 file in hello output asset displays hello overlay!</span></span>

![Recouvrement sur hello vidéo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="f5029-249">*Recouvrement sur hello vidéo*</span><span class="sxs-lookup"><span data-stu-id="f5029-249">*Overlay on hello video*</span></span>

<span data-ttu-id="f5029-250">Vous pouvez télécharger le workflow exemple hello [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span><span class="sxs-lookup"><span data-stu-id="f5029-250">You can download hello sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="f5029-251">Exemple 2 : Encodage de plusieurs langues audio</span><span class="sxs-lookup"><span data-stu-id="f5029-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="f5029-252">Vous trouverez un exemple de workflow d’encodage de plusieurs langues audio dans [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span><span class="sxs-lookup"><span data-stu-id="f5029-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="f5029-253">Ce dossier contient un exemple de workflow qui peut être utilisé tooencode une ressource de fichiers MXF fichier tooa multiples MP4 avec plusieurs pistes audio.</span><span class="sxs-lookup"><span data-stu-id="f5029-253">This folder contains a sample workflow which can be used tooencode a MXF file tooa multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="f5029-254">Ce flux de travail suppose que ce fichier MXF hello contient une piste audio ; des pistes audio Hello supplémentaires doivent être passés en tant que fichiers audio distincts (WAV ou MP4...).</span><span class="sxs-lookup"><span data-stu-id="f5029-254">This workflow assumes that hello MXF file contains one audio track ; hello additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="f5029-255">tooencode, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f5029-255">tooencode, please follow these steps:</span></span>

* <span data-ttu-id="f5029-256">Créer un élément multimédia Media Services avec hello et fichier MXF hello Audio (fichiers 0 too18 audio).</span><span class="sxs-lookup"><span data-stu-id="f5029-256">Create a Media Services asset with hello MXF file and hello Audio files (0 too18 audio files).</span></span>
* <span data-ttu-id="f5029-257">Assurez-vous que ce fichier MXF hello est défini comme un fichier primaire.</span><span class="sxs-lookup"><span data-stu-id="f5029-257">Make sure that hello MXF file is set as a primary file.</span></span>
* <span data-ttu-id="f5029-258">Créer une tâche et une tâche à l’aide du processeur d’encodeur de flux de travail Premium hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-258">Create a job and a task using hello Premium Workflow Encoder processor.</span></span> <span data-ttu-id="f5029-259">Utilisez le workflow hello fourni (MultiMP4-1080p-19audio-v1.workflow).</span><span class="sxs-lookup"><span data-stu-id="f5029-259">Use hello workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="f5029-260">Passer la tâche de hello setruntime.xml données toohello (si vous utilisez l’Explorateur Azure Media Services, utilisation (bouton) « passer le flux de travail toohello de données xml » hello).</span><span class="sxs-lookup"><span data-stu-id="f5029-260">Pass hello setruntime.xml data toohello task (if you use Azure Media Services Explorer, use hello “pass xml data toohello workflow” button).</span></span>
  * <span data-ttu-id="f5029-261">Mettez à jour hello données toospecify hello fichier correct pour les langues et les noms de balises XML.</span><span class="sxs-lookup"><span data-stu-id="f5029-261">Please update hello XML data toospecify hello correct file names and languages tags.</span></span>
  * <span data-ttu-id="f5029-262">flux de travail Hello comporte des éléments audio nommés 1 Audio tooAudio 18.</span><span class="sxs-lookup"><span data-stu-id="f5029-262">hello workflow has audio components named Audio 1 tooAudio 18.</span></span>
  * <span data-ttu-id="f5029-263">RFC5646 est pris en charge pour la balise de langue hello.</span><span class="sxs-lookup"><span data-stu-id="f5029-263">RFC5646 is supported for hello language tag.</span></span>

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

* <span data-ttu-id="f5029-264">actif de Hello encodé contiendra des pistes audio de langue multiples et ces pistes doivent être sélectionnés dans Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="f5029-264">hello encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="f5029-265">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f5029-265">See also</span></span>
* [<span data-ttu-id="f5029-266">Présentation de l’encodage Premium dans Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="f5029-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="f5029-267">Comment toouse Premium encodage dans Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="f5029-267">How toouse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="f5029-268">Encodage de contenu à la demande avec Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="f5029-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="f5029-269">Codecs et formats de Media Encoder Premium Workflow</span><span class="sxs-lookup"><span data-stu-id="f5029-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="f5029-270">Exemples de fichiers de workflow</span><span class="sxs-lookup"><span data-stu-id="f5029-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="f5029-271">Outil Azure Media Services Explorer</span><span class="sxs-lookup"><span data-stu-id="f5029-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="f5029-272">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="f5029-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f5029-273">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="f5029-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
