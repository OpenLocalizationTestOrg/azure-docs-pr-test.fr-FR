---
title: "aaaSmooth didacticiel d’application de diffusion en continu Windows Store | Documents Microsoft"
description: "Découvrez comment toouse Azure Media Services toocreate une application du Windows Store en c# avec un MediaElement XML contrôler tooplayback Smooth diffuser du contenu."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0fa5d8c5-3d5f-4886-ae55-fb6de4f5256d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: juliako
ms.openlocfilehash: b02aa2c7f68fe22a23ea846d72fdd23bfba2b19c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="4749e-103">Comment tooBuild un Smooth Streaming Application du Windows Store</span><span class="sxs-lookup"><span data-stu-id="4749e-103">How tooBuild a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="4749e-104">Hello Smooth Streaming Client SDK pour Windows 8 permet les applications du Windows Store les développeurs toobuild qui peuvent lire le contenu de diffusion en continu lisse à la demande et en direct.</span><span class="sxs-lookup"><span data-stu-id="4749e-104">hello Smooth Streaming Client SDK for Windows 8 enables developers toobuild Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="4749e-105">En outre lecture de base toohello de Smooth Streaming également de contenu, hello SDK fournit des fonctionnalités puissantes comme la protection de Microsoft PlayReady, restriction de niveau de qualité, Live magnétoscope numérique, le flux audio commutation, à l’écoute des mises à jour de l’état (telles que les modifications au niveau de qualité ) et les événements d’erreur et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="4749e-105">In addition toohello basic playback of Smooth Streaming content, hello SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="4749e-106">Pour plus d’informations des fonctionnalités de hello pris en charge, consultez hello [notes de publication](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span><span class="sxs-lookup"><span data-stu-id="4749e-106">For more information of hello supported features, see hello [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="4749e-107">Pour plus d’informations, consultez [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="4749e-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="4749e-108">Le didacticiel se compose de quatre leçons :</span><span class="sxs-lookup"><span data-stu-id="4749e-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="4749e-109">Création d'une application Windows Store de diffusion en continu lisse de base</span><span class="sxs-lookup"><span data-stu-id="4749e-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="4749e-110">Ajouter un barre tooControl hello Media progression du curseur</span><span class="sxs-lookup"><span data-stu-id="4749e-110">Add a Slider Bar tooControl hello Media Progress</span></span>
3. <span data-ttu-id="4749e-111">Sélection des flux de diffusion en continu lisse</span><span class="sxs-lookup"><span data-stu-id="4749e-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="4749e-112">Sélection des pistes de diffusion en continu lisse</span><span class="sxs-lookup"><span data-stu-id="4749e-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4749e-113">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="4749e-113">Prerequisites</span></span>
* <span data-ttu-id="4749e-114">Windows 8 32 bits ou 64 bits.</span><span class="sxs-lookup"><span data-stu-id="4749e-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="4749e-115">Vous pouvez télécharger la [version d'évaluation de Windows 8 Entreprise](http://msdn.microsoft.com/evalcenter/jj554510.aspx) sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="4749e-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="4749e-116">Visual Studio 2012 ou Visual Studio Express 2012 (ou une version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="4749e-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="4749e-117">Vous pouvez obtenir la version d’évaluation à partir de hello [ici](http://www.microsoft.com/visualstudio/11/downloads).</span><span class="sxs-lookup"><span data-stu-id="4749e-117">You can get hello trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="4749e-118">[Kit de développement logiciel (SDK) du client Microsoft de diffusion en continu lisse pour Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span><span class="sxs-lookup"><span data-stu-id="4749e-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="4749e-119">solution Hello terminé pour chaque leçon peut être téléchargée à partir d’exemples de Code pour développeurs MSDN (Code Gallery) :</span><span class="sxs-lookup"><span data-stu-id="4749e-119">hello completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="4749e-120">[Leçon 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) : un lecteur multimédia Smooth Streaming pour Windows 8,</span><span class="sxs-lookup"><span data-stu-id="4749e-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="4749e-121">[Leçon 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) : un lecteur multimédia simple Smooth Streaming pour Windows 8 doté d’une fonction de contrôle avec barre de curseur,</span><span class="sxs-lookup"><span data-stu-id="4749e-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="4749e-122">[Leçon 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) : un lecteur multimédia Smooth Streaming pour Windows 8 avec sélection de flux,</span><span class="sxs-lookup"><span data-stu-id="4749e-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="4749e-123">[Leçon 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) : un lecteur multimédia Smooth Streaming pour Windows 8 avec sélection des pistes.</span><span class="sxs-lookup"><span data-stu-id="4749e-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="4749e-124">Leçon 1 : créer une application Windows Store de diffusion en continu lisse de base</span><span class="sxs-lookup"><span data-stu-id="4749e-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="4749e-125">Dans cette leçon, vous créerez une application du Windows Store avec un contrôle MediaElement tooplay contenu Smooth Streaming contenu.</span><span class="sxs-lookup"><span data-stu-id="4749e-125">In this lesson, you will create a Windows Store application with a MediaElement control tooplay Smooth Stream content.</span></span>  <span data-ttu-id="4749e-126">exécution de l’application Hello ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="4749e-126">hello running application looks like:</span></span>

![Exemple d'application Windows Store de diffusion en continu lisse][PlayerApplication]

<span data-ttu-id="4749e-128">Pour plus d'informations sur le développement d'une application Windows Store, consultez la rubrique [Développement d'applications fantastiques pour Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span><span class="sxs-lookup"><span data-stu-id="4749e-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="4749e-129">Cette leçon contient hello procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="4749e-129">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="4749e-130">Création d'un projet Windows Store</span><span class="sxs-lookup"><span data-stu-id="4749e-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="4749e-131">Interface utilisateur du concepteur hello (XAML)</span><span class="sxs-lookup"><span data-stu-id="4749e-131">Design hello user interface (XAML)</span></span>
3. <span data-ttu-id="4749e-132">Modifier hello fichier code-behind</span><span class="sxs-lookup"><span data-stu-id="4749e-132">Modify hello code behind file</span></span>
4. <span data-ttu-id="4749e-133">Compiler et tester l’application hello</span><span class="sxs-lookup"><span data-stu-id="4749e-133">Compile and test hello application</span></span>

<span data-ttu-id="4749e-134">**toocreate un projet Windows Store**</span><span class="sxs-lookup"><span data-stu-id="4749e-134">**toocreate a Windows Store project**</span></span>

1. <span data-ttu-id="4749e-135">Exécutez Visual Studio 2012 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="4749e-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="4749e-136">À partir de hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="4749e-136">From hello **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="4749e-137">À partir de la boîte de dialogue Nouveau projet hello, type ou sélectionnez hello suivant des valeurs :</span><span class="sxs-lookup"><span data-stu-id="4749e-137">From hello New Project dialog, type or select  hello following values:</span></span>

| <span data-ttu-id="4749e-138">Nom</span><span class="sxs-lookup"><span data-stu-id="4749e-138">Name</span></span> | <span data-ttu-id="4749e-139">Valeur</span><span class="sxs-lookup"><span data-stu-id="4749e-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4749e-140">Groupe de modèles</span><span class="sxs-lookup"><span data-stu-id="4749e-140">Template group</span></span> |<span data-ttu-id="4749e-141">Installed/Templates/Visual C#/Windows Store</span><span class="sxs-lookup"><span data-stu-id="4749e-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="4749e-142">Modèle</span><span class="sxs-lookup"><span data-stu-id="4749e-142">Template</span></span> |<span data-ttu-id="4749e-143">Application vide (XAML)</span><span class="sxs-lookup"><span data-stu-id="4749e-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="4749e-144">Nom</span><span class="sxs-lookup"><span data-stu-id="4749e-144">Name</span></span> |<span data-ttu-id="4749e-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="4749e-145">SSPlayer</span></span> |
| <span data-ttu-id="4749e-146">Lieu</span><span class="sxs-lookup"><span data-stu-id="4749e-146">Location</span></span> |<span data-ttu-id="4749e-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="4749e-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="4749e-148">Nom de la solution</span><span class="sxs-lookup"><span data-stu-id="4749e-148">Solution Name</span></span> |<span data-ttu-id="4749e-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="4749e-149">SSPlayer</span></span> |
| <span data-ttu-id="4749e-150">Créer un répertoire pour la solution</span><span class="sxs-lookup"><span data-stu-id="4749e-150">Create directory for solution</span></span> |<span data-ttu-id="4749e-151">(sélectionné)</span><span class="sxs-lookup"><span data-stu-id="4749e-151">(selected)</span></span> |

1. <span data-ttu-id="4749e-152">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4749e-152">Click **OK**.</span></span>

<span data-ttu-id="4749e-153">**tooadd un toohello référence SDK de Client de diffusion en continu lisse**</span><span class="sxs-lookup"><span data-stu-id="4749e-153">**tooadd a reference toohello Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="4749e-154">Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **SSPlayer**, puis cliquez sur **Ajouter une référence**.</span><span class="sxs-lookup"><span data-stu-id="4749e-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="4749e-155">Tapez ou sélectionnez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="4749e-155">Type or select hello following values:</span></span>

| <span data-ttu-id="4749e-156">Nom</span><span class="sxs-lookup"><span data-stu-id="4749e-156">Name</span></span> | <span data-ttu-id="4749e-157">Valeur</span><span class="sxs-lookup"><span data-stu-id="4749e-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4749e-158">Groupe de référence</span><span class="sxs-lookup"><span data-stu-id="4749e-158">Reference group</span></span> |<span data-ttu-id="4749e-159">Windows/Extensions</span><span class="sxs-lookup"><span data-stu-id="4749e-159">Windows/Extensions</span></span> |
| <span data-ttu-id="4749e-160">Référence</span><span class="sxs-lookup"><span data-stu-id="4749e-160">Reference</span></span> |<span data-ttu-id="4749e-161">Sélectionnez le Kit de développement logiciel (SDK) du client de diffusion en continu lisse pour Windows 8 et le package Runtime Microsoft Visual C++</span><span class="sxs-lookup"><span data-stu-id="4749e-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="4749e-162">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4749e-162">Click **OK**.</span></span> 

<span data-ttu-id="4749e-163">Après avoir ajouté des références de hello, vous devez sélectionner la plate-forme hello ciblé (x64 ou x86), ajout de références ne fonctionne pas pour la configuration de la plateforme Any CPU.</span><span class="sxs-lookup"><span data-stu-id="4749e-163">After adding hello references, you must select hello targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="4749e-164">Dans l'Explorateur de solutions, un symbole d'avertissement jaune s'affiche pour indiquer les références ajoutées.</span><span class="sxs-lookup"><span data-stu-id="4749e-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="4749e-165">**interface utilisateur de toodesign hello lecteur**</span><span class="sxs-lookup"><span data-stu-id="4749e-165">**toodesign hello player user interface**</span></span>

1. <span data-ttu-id="4749e-166">Dans l’Explorateur de solutions, double-cliquez sur **MainPage.xaml** tooopen dans la conception de hello afficher.</span><span class="sxs-lookup"><span data-stu-id="4749e-166">From Solution Explorer, double click **MainPage.xaml** tooopen it in hello design view.</span></span>
2. <span data-ttu-id="4749e-167">Recherchez hello  **&lt;grille&gt;**  et  **&lt;/Grid&gt;**  balises hello fichier XAML et de code suivant de hello de coller entre les balises de hello deux :</span><span class="sxs-lookup"><span data-stu-id="4749e-167">Locate hello **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags hello XAML file, and paste hello following code between hello two tags:</span></span>

         <Grid.RowDefinitions>

            <RowDefinition Height="20"/>    <!-- spacer -->
            <RowDefinition Height="50"/>    <!-- media controls -->
            <RowDefinition Height="100*"/>  <!-- media element -->
            <RowDefinition Height="80*"/>   <!-- media stream and track selection -->
            <RowDefinition Height="50"/>    <!-- status bar -->
         </Grid.RowDefinitions>

         <StackPanel Name="spMediaControl" Grid.Row="1" Orientation="Horizontal">
            <TextBlock x:Name="tbSource" Text="Source :  " FontSize="16" FontWeight="Bold" VerticalAlignment="Center" />
            <TextBox x:Name="txtMediaSource" Text="http://ecn.channel9.msdn.com/o9/content/smf/smoothcontent/elephantsdream/Elephants_Dream_1024-h264-st-aac.ism/manifest" FontSize="10" Width="700" Margin="0,4,0,10" />
            <Button x:Name="btnSetSource" Content="Set Source" Width="111" Height="43" Click="btnSetSource_Click"/>
            <Button x:Name="btnPlay" Content="Play" Width="111" Height="43" Click="btnPlay_Click"/>
            <Button x:Name="btnPause" Content="Pause"  Width="111" Height="43" Click="btnPause_Click"/>
            <Button x:Name="btnStop" Content="Stop"  Width="111" Height="43" Click="btnStop_Click"/>
            <CheckBox x:Name="chkAutoPlay" Content="Auto Play" Height="55" Width="Auto" IsChecked="{Binding AutoPlay, ElementName=mediaElement, Mode=TwoWay}"/>
            <CheckBox x:Name="chkMute" Content="Mute" Height="55" Width="67" IsChecked="{Binding IsMuted, ElementName=mediaElement, Mode=TwoWay}"/>
         </StackPanel>

         <StackPanel Name="spMediaElement" Grid.Row="2" Height="435" Width="1072"
                    HorizontalAlignment="Center" VerticalAlignment="Center">
            <MediaElement x:Name="mediaElement" Height="356" Width="924" MinHeight="225"
                          HorizontalAlignment="Center" VerticalAlignment="Center" 
                          AudioCategory="BackgroundCapableMedia" />
            <StackPanel Orientation="Horizontal">
                <Slider x:Name="sliderProgress" Width="924" Height="44"
                        HorizontalAlignment="Center" VerticalAlignment="Center"
                        PointerPressed="sliderProgress_PointerPressed"/>
                <Slider x:Name="sliderVolume" 
                        HorizontalAlignment="Right" VerticalAlignment="Center" Orientation="Vertical" 
                        Height="79" Width="148" Minimum="0" Maximum="1" StepFrequency="0.1" 
                        Value="{Binding Volume, ElementName=mediaElement, Mode=TwoWay}" 
                        ToolTipService.ToolTip="{Binding Value, RelativeSource={RelativeSource Mode=Self}}"/>
            </StackPanel>
         </StackPanel>

         <StackPanel Name="spStatus" Grid.Row="4" Orientation="Horizontal">
            <TextBlock x:Name="tbStatus" Text="Status :  " 
               FontSize="16" FontWeight="Bold" VerticalAlignment="Center" HorizontalAlignment="Center" />
            <TextBox x:Name="txtStatus" FontSize="10" Width="700" VerticalAlignment="Center"/>
         </StackPanel>
   
   <span data-ttu-id="4749e-168">Hello contrôle MediaElement est un support tooplayback utilisé.</span><span class="sxs-lookup"><span data-stu-id="4749e-168">hello MediaElement control is used tooplayback media.</span></span> <span data-ttu-id="4749e-169">contrôle de curseur Hello nommé sliderProgress servira en cours du support hello prochaine leçon toocontrol hello.</span><span class="sxs-lookup"><span data-stu-id="4749e-169">hello slider control named sliderProgress will be used in hello next lesson toocontrol hello media progress.</span></span>
3. <span data-ttu-id="4749e-170">Appuyez sur **CTRL + S** fichier hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="4749e-170">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="4749e-171">Hello contrôle MediaElement ne prend pas en charge la diffusion en continu lisse contenu out-of-box.</span><span class="sxs-lookup"><span data-stu-id="4749e-171">hello MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="4749e-172">tooenable hello Smooth Streaming prise en charge, vous devez inscrire le gestionnaire hello octet-stream diffusion en continu par l’extension de nom de fichier et le type MIME.</span><span class="sxs-lookup"><span data-stu-id="4749e-172">tooenable hello Smooth Streaming support, you must register hello Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="4749e-173">tooregister, vous utilisez (méthode MediaExtensionManager.RegisterByteStremHandler hello) de l’espace de noms Windows.Media hello.</span><span class="sxs-lookup"><span data-stu-id="4749e-173">tooregister, you use hello MediaExtensionManager.RegisterByteStremHandler method of hello Windows.Media namespace.</span></span>

<span data-ttu-id="4749e-174">Dans ce fichier XAML, certains gestionnaires d’événements sont associés à des contrôles de hello.</span><span class="sxs-lookup"><span data-stu-id="4749e-174">In this XAML file, some event handlers are associated with hello controls.</span></span>  <span data-ttu-id="4749e-175">Vous devez définir les gestionnaires d'événements en question.</span><span class="sxs-lookup"><span data-stu-id="4749e-175">You must define those event handlers.</span></span>

<span data-ttu-id="4749e-176">**toomodify hello fichier code-behind**</span><span class="sxs-lookup"><span data-stu-id="4749e-176">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="4749e-177">Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.</span><span class="sxs-lookup"><span data-stu-id="4749e-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="4749e-178">Haut hello du fichier de hello, ajoutez hello qui suit à l’aide d’instruction :</span><span class="sxs-lookup"><span data-stu-id="4749e-178">At hello top of hello file, add hello following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="4749e-179">Au début de hello Hello **MainPage** de classe, ajoutez hello suivant du membre de données :</span><span class="sxs-lookup"><span data-stu-id="4749e-179">At hello beginning of hello **MainPage** class, add hello following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="4749e-180">À fin hello Hello **MainPage** constructeur, ajoutez hello deux lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4749e-180">At hello end of hello **MainPage** constructor, add hello following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="4749e-181">À fin hello Hello **MainPage** de classe, collez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="4749e-181">At hello end of hello **MainPage** class, paste hello following code:</span></span>
   
         # region UI Button Click Events
         private void btnPlay_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Play();
         txtStatus.Text = "MediaElement is playing ...";
         }
         private void btnPause_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Pause();
         txtStatus.Text = "MediaElement is paused";
         }
         private void btnSetSource_Click(object sender, RoutedEventArgs e)
         {

         sliderProgress.Value = 0;
         mediaElement.Source = new Uri(txtMediaSource.Text);

         if (chkAutoPlay.IsChecked == true)
         {
             txtStatus.Text = "MediaElement is playing ...";
         }
         else
         {
             txtStatus.Text = "Click hello Play button tooplay hello media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek tooposition " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

<span data-ttu-id="4749e-182">Gestionnaire d’événements sliderProgress_PointerPressed Hello est défini ici.</span><span class="sxs-lookup"><span data-stu-id="4749e-182">hello sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="4749e-183">Il existe plusieurs tooget de toodo fonctionne qu’il fonctionne, qui seront abordée dans la leçon suivante de hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4749e-183">There are more works toodo tooget it working, which will be covered in hello next lesson of this tutorial.</span></span>
6. <span data-ttu-id="4749e-184">Appuyez sur **CTRL + S** fichier hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="4749e-184">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="4749e-185">Hello hello terminé fichier code-behind doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="4749e-185">hello finished hello code behind file shall look like this:</span></span>

![Codeview dans Visual Studio d'une application Windows Store de diffusion en continu lisse][CodeViewPic]

<span data-ttu-id="4749e-187">**application de hello toocompile et de test**</span><span class="sxs-lookup"><span data-stu-id="4749e-187">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="4749e-188">À partir de hello **générer** menu, cliquez sur **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="4749e-188">From hello **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="4749e-189">Modification **plateforme de solution Active** toomatch votre plateforme de développement.</span><span class="sxs-lookup"><span data-stu-id="4749e-189">Change **Active solution platform** toomatch your development platform.</span></span>
3. <span data-ttu-id="4749e-190">Appuyez sur **F6** projet hello de toocompile.</span><span class="sxs-lookup"><span data-stu-id="4749e-190">Press **F6** toocompile hello project.</span></span> 
4. <span data-ttu-id="4749e-191">Appuyez sur **F5** application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="4749e-191">Press **F5** toorun hello application.</span></span>
5. <span data-ttu-id="4749e-192">Haut hello du application hello, vous pouvez utiliser la valeur par défaut de hello URL de diffusion en continu lisse ou entrez un nom différent.</span><span class="sxs-lookup"><span data-stu-id="4749e-192">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="4749e-193">Cliquez sur **Définir la source**.</span><span class="sxs-lookup"><span data-stu-id="4749e-193">Click **Set Source**.</span></span> <span data-ttu-id="4749e-194">Étant donné que **lecture Auto** est activée par défaut, hello la lecture du média est automatiquement.</span><span class="sxs-lookup"><span data-stu-id="4749e-194">Because **Auto Play** is enabled by default, hello media shall play automatically.</span></span>  <span data-ttu-id="4749e-195">Vous pouvez contrôler les média hello à l’aide de hello **lire**, **Pause** et **arrêter** boutons.</span><span class="sxs-lookup"><span data-stu-id="4749e-195">You can control hello media using hello **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="4749e-196">Vous pouvez contrôler le volume de support hello à l’aide du curseur vertical de hello.</span><span class="sxs-lookup"><span data-stu-id="4749e-196">You can control hello media volume using hello vertical slider.</span></span>  <span data-ttu-id="4749e-197">Toutefois, hello curseur horizontal pour le contrôle hello progression de média n’est pas entièrement encore implémentée.</span><span class="sxs-lookup"><span data-stu-id="4749e-197">However hello horizontal slider for controlling hello media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="4749e-198">Vous avez terminé la leçon 1.</span><span class="sxs-lookup"><span data-stu-id="4749e-198">You have completed lesson1.</span></span>  <span data-ttu-id="4749e-199">Dans cette leçon, vous utilisez un tooplayback de contrôle MediaElement contenu Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="4749e-199">In this lesson, you use a MediaElement control tooplayback Smooth Streaming content.</span></span>  <span data-ttu-id="4749e-200">Dans la leçon suivante de hello, vous allez ajouter une progression de hello curseur toocontrol Hello contenu Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="4749e-200">In hello next lesson, you will add a slider toocontrol hello progress of hello Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a><span data-ttu-id="4749e-201">Leçon 2 : Ajouter un barre tooControl hello Media progression du curseur</span><span class="sxs-lookup"><span data-stu-id="4749e-201">Lesson 2: Add a Slider Bar tooControl hello Media Progress</span></span>

<span data-ttu-id="4749e-202">Dans la leçon 1, vous avez créé une application du Windows Store avec un tooplayback de contrôle MediaElement XAML diffusion en continu le contenu du média.</span><span class="sxs-lookup"><span data-stu-id="4749e-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control tooplayback Smooth Streaming media content.</span></span>  <span data-ttu-id="4749e-203">Elle offre des fonctions de lecture multimédia de base, comme le démarrage, l'arrêt et la pause.</span><span class="sxs-lookup"><span data-stu-id="4749e-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="4749e-204">Dans cette leçon, vous allez ajouter une application de toohello contrôle slider barre.</span><span class="sxs-lookup"><span data-stu-id="4749e-204">In this lesson, you will add a slider bar control toohello application.</span></span>

<span data-ttu-id="4749e-205">Dans ce didacticiel, nous allons utiliser un minuteur tooupdate hello curseur en fonction de la position actuelle de hello Hello contrôle MediaElement.</span><span class="sxs-lookup"><span data-stu-id="4749e-205">In this tutorial, we will use a timer tooupdate hello slider position based on hello current position of hello MediaElement control.</span></span>  <span data-ttu-id="4749e-206">curseur de Hello commencer et se terminer temps également toobe besoin de mettre à jour en cas de contenu en direct.</span><span class="sxs-lookup"><span data-stu-id="4749e-206">hello slider start and end time also need toobe updated in case of live content.</span></span>  <span data-ttu-id="4749e-207">Cela peut être mieux gérée dans les événements de mise à jour source adaptive hello.</span><span class="sxs-lookup"><span data-stu-id="4749e-207">This can be better handled in hello adaptive source update event.</span></span>

<span data-ttu-id="4749e-208">Les sources multimédias sont des objets qui produisent des données multimédias.</span><span class="sxs-lookup"><span data-stu-id="4749e-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="4749e-209">programme de résolution de source Hello prend un flux d’URL ou d’octets et crée la source de média approprié hello pour ce contenu.</span><span class="sxs-lookup"><span data-stu-id="4749e-209">hello source resolver takes a URL or byte stream and creates hello appropriate media source for that content.</span></span>  <span data-ttu-id="4749e-210">programme de résolution de source Hello consiste hello standard pour des sources de médias toocreate hello applications.</span><span class="sxs-lookup"><span data-stu-id="4749e-210">hello source resolver is hello standard way for hello applications toocreate media sources.</span></span> 

<span data-ttu-id="4749e-211">Cette leçon contient hello procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="4749e-211">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="4749e-212">Inscrire le Gestionnaire de diffusion en continu lisse hello</span><span class="sxs-lookup"><span data-stu-id="4749e-212">Register hello Smooth Streaming handler</span></span> 
2. <span data-ttu-id="4749e-213">Ajoutez des gestionnaires d’événements de niveau hello source adaptive manager</span><span class="sxs-lookup"><span data-stu-id="4749e-213">Add hello adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="4749e-214">Ajoutez des gestionnaires d’événements au niveau source adaptive hello</span><span class="sxs-lookup"><span data-stu-id="4749e-214">Add hello adaptive source level event handlers</span></span>
4. <span data-ttu-id="4749e-215">Ajout de gestionnaires d'événements MediaElement</span><span class="sxs-lookup"><span data-stu-id="4749e-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="4749e-216">Ajout du code lié à la barre de curseur</span><span class="sxs-lookup"><span data-stu-id="4749e-216">Add slider bar related code</span></span>
6. <span data-ttu-id="4749e-217">Compiler et tester l’application hello</span><span class="sxs-lookup"><span data-stu-id="4749e-217">Compile and test hello application</span></span>

<span data-ttu-id="4749e-218">**propertyset hello tooregister hello flux d’octets de diffusion en continu lisse gestionnaire et passez**</span><span class="sxs-lookup"><span data-stu-id="4749e-218">**tooregister hello Smooth Streaming byte-stream handler and pass hello propertyset**</span></span>

1. <span data-ttu-id="4749e-219">Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.</span><span class="sxs-lookup"><span data-stu-id="4749e-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="4749e-220">Au début de hello du fichier de hello, ajoutez hello à l’aide d’instruction :</span><span class="sxs-lookup"><span data-stu-id="4749e-220">At hello beginning of hello file, add hello following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="4749e-221">Au début de hello Hello classe MainPage, ajoutez hello suivant des membres de données :</span><span class="sxs-lookup"><span data-stu-id="4749e-221">At hello beginning of hello MainPage class, add hello following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="4749e-222">À l’intérieur hello **MainPage** constructeur, ajoutez hello après le code après hello **cela. Initialiser Components() ;**  ligne et les lignes de code hello d’enregistrement écrits dans la leçon précédente de hello :</span><span class="sxs-lookup"><span data-stu-id="4749e-222">Inside hello **MainPage** constructor, add hello following code after hello **this.Initialize Components();** line and hello registration code lines written in hello previous lesson:</span></span>

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="4749e-223">À l’intérieur hello **MainPage** constructeur, modifier hello de hello deux RegisterByteStreamHandler méthodes tooadd les deux paramètres :</span><span class="sxs-lookup"><span data-stu-id="4749e-223">Inside hello **MainPage** constructor, modify hello two RegisterByteStreamHandler methods tooadd hello forth parameters:</span></span>

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass hello propertyset. 
         // http://*.ism/manifest URI resources will be resolved by Byte-stream handler.
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "text/xml", 
            propertySet );
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "application/vnd.ms-sstr+xml", 
         propertySet);
6. <span data-ttu-id="4749e-224">Appuyez sur **CTRL + S** fichier hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="4749e-224">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="4749e-225">**Gestionnaire d’événements de niveau tooadd hello source adaptive manager**</span><span class="sxs-lookup"><span data-stu-id="4749e-225">**tooadd hello adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="4749e-226">Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.</span><span class="sxs-lookup"><span data-stu-id="4749e-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="4749e-227">À l’intérieur hello **MainPage** de classe, ajoutez hello suivant du membre de données :</span><span class="sxs-lookup"><span data-stu-id="4749e-227">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="4749e-228">private AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="4749e-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="4749e-229">À fin hello Hello **MainPage** de classe, ajoutez hello suivant du Gestionnaire d’événements :</span><span class="sxs-lookup"><span data-stu-id="4749e-229">At hello end of hello **MainPage** class, add hello following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="4749e-230">À fin hello Hello **MainPage** constructeur, ajoutez hello suivant ligne toosubscribe toohello adaptative source ouvert événement :</span><span class="sxs-lookup"><span data-stu-id="4749e-230">At hello end of hello **MainPage** constructor, add hello following line toosubscribe toohello adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="4749e-231">Appuyez sur **CTRL + S** fichier hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="4749e-231">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="4749e-232">**gestionnaires d’événements au niveau source adaptive tooadd**</span><span class="sxs-lookup"><span data-stu-id="4749e-232">**tooadd adaptive source level event handlers**</span></span>

1. <span data-ttu-id="4749e-233">Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.</span><span class="sxs-lookup"><span data-stu-id="4749e-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="4749e-234">À l’intérieur hello **MainPage** de classe, ajoutez hello suivant du membre de données :</span><span class="sxs-lookup"><span data-stu-id="4749e-234">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="4749e-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span><span class="sxs-lookup"><span data-stu-id="4749e-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="4749e-236">À fin hello Hello **MainPage** de classe, ajoutez hello suivant des gestionnaires d’événements :</span><span class="sxs-lookup"><span data-stu-id="4749e-236">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

         # region Adaptive Source Level Events
         private void mediaElement_ManifestReady(AdaptiveSource sender, ManifestReadyEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
            manifestObject = args.AdaptiveSource.Manifest;
         }

         private void mediaElement_AdaptiveSourceStatusUpdated(AdaptiveSource sender, AdaptiveSourceStatusUpdatedEventArgs args)
         {

            adaptiveSourceStatusUpdate = args;
         }

         private void mediaElement_AdaptiveSourceFailed(AdaptiveSource sender, AdaptiveSourceFailedEventArgs args)
         {

            txtStatus.Text = "Error: " + args.HttpResponse;
         }

         # endregion Adaptive Source Level Events
4. <span data-ttu-id="4749e-237">À fin hello Hello **mediaElement AdaptiveSourceOpened** (méthode), ajouter hello après les événements de code toosubscribe toohello :</span><span class="sxs-lookup"><span data-stu-id="4749e-237">At hello end of hello **mediaElement AdaptiveSourceOpened** method, add hello following code toosubscribe toohello events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="4749e-238">Appuyez sur **CTRL + S** fichier hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="4749e-238">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="4749e-239">Hello mêmes événements sont disponibles sur Adaptive Gestionnaire niveau de la Source, qui peut être utilisé pour la gestion des fonctionnalités tooall media éléments communs application hello.</span><span class="sxs-lookup"><span data-stu-id="4749e-239">hello same events are available on Adaptive Source manger level as well, which can be used for handling functionality common tooall media elements in hello app.</span></span> <span data-ttu-id="4749e-240">Chaque AdaptiveSource inclut ses propres événements et tous les événements AdaptiveSource sont affichés en cascade dans AdaptiveSourceManager.</span><span class="sxs-lookup"><span data-stu-id="4749e-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="4749e-241">**gestionnaires d’événements tooadd élément multimédia**</span><span class="sxs-lookup"><span data-stu-id="4749e-241">**tooadd Media Element event handlers**</span></span>

1. <span data-ttu-id="4749e-242">Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.</span><span class="sxs-lookup"><span data-stu-id="4749e-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="4749e-243">À fin hello Hello **MainPage** de classe, ajoutez hello suivant des gestionnaires d’événements :</span><span class="sxs-lookup"><span data-stu-id="4749e-243">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

         # region Media Element Event Handlers
         private void MediaOpened(object sender, RoutedEventArgs e)
         {

            txtStatus.Text = "MediaElement opened";
         }

         private void MediaFailed(object sender, ExceptionRoutedEventArgs e)
         {

            txtStatus.Text= "MediaElement failed: " + e.ErrorMessage;
         }

         private void MediaEnded(object sender, RoutedEventArgs e)
         {

            txtStatus.Text ="MediaElement ended.";
         }

         # endregion Media Element Event Handlers
3. <span data-ttu-id="4749e-244">À fin hello Hello **MainPage** constructeur, ajoutez hello après les événements de code toosubscript toohello :</span><span class="sxs-lookup"><span data-stu-id="4749e-244">At hello end of hello **MainPage** constructor, add hello following code toosubscript toohello events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="4749e-245">Appuyez sur **CTRL + S** fichier hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="4749e-245">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="4749e-246">**curseur tooadd connexe code barres**</span><span class="sxs-lookup"><span data-stu-id="4749e-246">**tooadd slider bar related code**</span></span>

1. <span data-ttu-id="4749e-247">Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.</span><span class="sxs-lookup"><span data-stu-id="4749e-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="4749e-248">Au début de hello du fichier de hello, ajoutez hello à l’aide d’instruction :</span><span class="sxs-lookup"><span data-stu-id="4749e-248">At hello beginning of hello file, add hello following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="4749e-249">À l’intérieur hello **MainPage** de classe, ajoutez hello suivant des membres de données :</span><span class="sxs-lookup"><span data-stu-id="4749e-249">Inside hello **MainPage** class, add hello following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="4749e-250">À fin hello Hello **MainPage** constructeur, ajoutez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="4749e-250">At hello end of hello **MainPage** constructor, add hello following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="4749e-251">À fin hello Hello **MainPage** de classe, ajoutez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="4749e-251">At hello end of hello **MainPage** class, add hello following code:</span></span>

         # region sliderMediaPlayer
         private double SliderFrequency(TimeSpan timevalue)
         {

            long absvalue = 0;
            double stepfrequency = -1;

            if (manifestObject != null)
            {
                absvalue = manifestObject.Duration - (long)manifestObject.StartTime;
            }
            else
            {
                absvalue = mediaElement.NaturalDuration.TimeSpan.Ticks;
            }

            TimeSpan totalDVRDuration = new TimeSpan(absvalue);

            if (totalDVRDuration.TotalMinutes >= 10 && totalDVRDuration.TotalMinutes < 30)
            {
               stepfrequency = 10;
            }
            else if (totalDVRDuration.TotalMinutes >= 30 
                     && totalDVRDuration.TotalMinutes < 60)
            {
                stepfrequency = 30;
            }
            else if (totalDVRDuration.TotalHours >= 1)
            {
                stepfrequency = 60;
            }

            return stepfrequency;
         }

         void updateSliderPositionoNTicks(object sender, object e)
         {

            sliderProgress.Value = mediaElement.Position.TotalSeconds;
         }

         public void setupTimer()
         {

            sliderPositionUpdateDispatcher = new DispatcherTimer();
            sliderPositionUpdateDispatcher.Interval = new TimeSpan(0, 0, 0, 0, 300);
            startTimer();
         }

         public void startTimer()
         {

            sliderPositionUpdateDispatcher.Tick += updateSliderPositionoNTicks;
            sliderPositionUpdateDispatcher.Start();
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderStartTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.StartTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Minimum = absvalue;
            });
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderEndTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Maximum = absvalue;
            });
         }

         # endregion sliderMediaPlayer
      
>[!NOTE]
><span data-ttu-id="4749e-252">CoreDispatcher est modifications toomake utilisé toohello l’interface utilisateur de thread non thread d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4749e-252">CoreDispatcher is used toomake changes toohello UI thread from non UI Thread.</span></span> <span data-ttu-id="4749e-253">En cas de goulot d’étranglement sur le thread dispatcher, développeur peut choisir toouse répartiteur fournie par l’élément d’interface utilisateur qu'il envisage de tooupdate.</span><span class="sxs-lookup"><span data-stu-id="4749e-253">In case of bottleneck on dispatcher thread, developer can choose toouse dispatcher provided by UI-element he/she intends tooupdate.</span></span>  <span data-ttu-id="4749e-254">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="4749e-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="4749e-255">À fin hello Hello **mediaElement_AdaptiveSourceStatusUpdated** (méthode), ajouter hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="4749e-255">At hello end of hello **mediaElement_AdaptiveSourceStatusUpdated** method, add hello following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="4749e-256">À fin hello Hello **MediaOpened** (méthode), ajouter hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="4749e-256">At hello end of hello **MediaOpened** method, add hello following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="4749e-257">Appuyez sur **CTRL + S** fichier hello de toosave.</span><span class="sxs-lookup"><span data-stu-id="4749e-257">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="4749e-258">**application de hello toocompile et de test**</span><span class="sxs-lookup"><span data-stu-id="4749e-258">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="4749e-259">Appuyez sur **F6** projet hello de toocompile.</span><span class="sxs-lookup"><span data-stu-id="4749e-259">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="4749e-260">Appuyez sur **F5** application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="4749e-260">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="4749e-261">Haut hello du application hello, vous pouvez utiliser la valeur par défaut de hello URL de diffusion en continu lisse ou entrez un nom différent.</span><span class="sxs-lookup"><span data-stu-id="4749e-261">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="4749e-262">Cliquez sur **Définir la source**.</span><span class="sxs-lookup"><span data-stu-id="4749e-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="4749e-263">Barre de défilement test hello.</span><span class="sxs-lookup"><span data-stu-id="4749e-263">Test hello slider bar.</span></span>

<span data-ttu-id="4749e-264">Vous avez terminé la leçon 2.</span><span class="sxs-lookup"><span data-stu-id="4749e-264">You have completed lesson 2.</span></span>  <span data-ttu-id="4749e-265">Dans cette leçon, vous avez ajouté une tooapplication de curseur.</span><span class="sxs-lookup"><span data-stu-id="4749e-265">In this lesson you added a slider tooapplication.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="4749e-266">Leçon 3 : sélectionner les flux de diffusion en continu lisse</span><span class="sxs-lookup"><span data-stu-id="4749e-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="4749e-267">Smooth Streaming est contenu toostream compatibles avec plusieurs pistes audio langage sont sélectionnables par les visionneuses hello.</span><span class="sxs-lookup"><span data-stu-id="4749e-267">Smooth Streaming is capable toostream content with multiple language audio tracks that are selectable by hello viewers.</span></span>  <span data-ttu-id="4749e-268">Dans cette leçon, vous allez activer le flux de données tooselect visionneuses.</span><span class="sxs-lookup"><span data-stu-id="4749e-268">In this lesson, you will enable viewers tooselect streams.</span></span> <span data-ttu-id="4749e-269">Cette leçon contient hello procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="4749e-269">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="4749e-270">Modifier le fichier XAML de hello</span><span class="sxs-lookup"><span data-stu-id="4749e-270">Modify hello XAML file</span></span>
2. <span data-ttu-id="4749e-271">Modifier le fichier de behand code hello</span><span class="sxs-lookup"><span data-stu-id="4749e-271">Modify hello code behand file</span></span>
3. <span data-ttu-id="4749e-272">Compiler et tester l’application hello</span><span class="sxs-lookup"><span data-stu-id="4749e-272">Compile and test hello application</span></span>

<span data-ttu-id="4749e-273">**fichier XAML de hello toomodify**</span><span class="sxs-lookup"><span data-stu-id="4749e-273">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="4749e-274">Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Concepteur de vues**.</span><span class="sxs-lookup"><span data-stu-id="4749e-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="4749e-275">Recherchez &lt;Grid.RowDefinitions&gt;et modifier hello RowDefinitions afin qu’ils ressemble à :</span><span class="sxs-lookup"><span data-stu-id="4749e-275">Locate &lt;Grid.RowDefinitions&gt;, and modify hello RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="4749e-276">À l’intérieur hello &lt;grille&gt;&lt;/Grid&gt; ajouter des balises, hello de code suivant toodefine un contrôle listbox, donc les utilisateurs peuvent voir liste hello de flux de données disponibles et sélectionnez le flux de données :</span><span class="sxs-lookup"><span data-stu-id="4749e-276">Inside hello &lt;Grid&gt;&lt;/Grid&gt; tags, add hello following code toodefine a listbox control, so users can see hello list of available streams, and select streams:</span></span>

         <Grid Name="gridStreamAndBitrateSelection" Grid.Row="3">
            <Grid.RowDefinitions>
                <RowDefinition Height="300"/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="250*"/>
                <ColumnDefinition Width="250*"/>
            </Grid.ColumnDefinitions>
            <StackPanel Name="spStreamSelection" Grid.Row="1" Grid.Column="0">
                <StackPanel Orientation="Horizontal">
                    <TextBlock Name="tbAvailableStreams" Text="Available Streams:" FontSize="16" VerticalAlignment="Center"></TextBlock>
                    <Button Name="btnChangeStreams" Content="Submit" Click="btnChangeStream_Click"/>
                </StackPanel>
                <ListBox x:Name="lbAvailableStreams" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                    ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
                    <ListBox.ItemTemplate>
                        <DataTemplate>
                            <CheckBox Content="{Binding Name}" IsChecked="{Binding isChecked, Mode=TwoWay}" />
                        </DataTemplate>
                    </ListBox.ItemTemplate>
                </ListBox>
            </StackPanel>
         </Grid>
4. <span data-ttu-id="4749e-277">Appuyez sur **CTRL + S** modifications de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="4749e-277">Press **CTRL+S** toosave hello changes.</span></span>

<span data-ttu-id="4749e-278">**toomodify hello fichier code-behind**</span><span class="sxs-lookup"><span data-stu-id="4749e-278">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="4749e-279">Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.</span><span class="sxs-lookup"><span data-stu-id="4749e-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="4749e-280">Au sein de l’espace de noms SSPlayer hello, ajoutez une nouvelle classe :</span><span class="sxs-lookup"><span data-stu-id="4749e-280">Inside hello SSPlayer namespace, add a new class:</span></span>
   
        #region class Stream
   
        public class Stream
        {
            private IManifestStream stream;
            public bool isCheckedValue;
            public string name;
   
            public string Name
            {
                get { return name; }
                set { name = value; }
            }
   
            public IManifestStream ManifestStream
            {
                get { return stream; }
                set { stream = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    // mMke hello video stream always checked.
                    if (stream.Type == MediaStreamType.Video)
                    {
                        isCheckedValue = true;
                    }
                    else
                    {
                        isCheckedValue = value;
                    }
                }
            }
   
            public Stream(IManifestStream streamIn)
            {
                stream = streamIn;
                name = stream.Name;
            }
        }
        #endregion class Stream
3. <span data-ttu-id="4749e-281">Au début de hello Hello classe MainPage, ajoutez hello suivant des définitions de variables :</span><span class="sxs-lookup"><span data-stu-id="4749e-281">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="4749e-282">Au sein de hello classe MainPage, ajoutez hello suivant région :</span><span class="sxs-lookup"><span data-stu-id="4749e-282">Inside hello MainPage class, add hello following region:</span></span>
   
        #region stream selection
        ///<summary>
        ///Functionality tooselect streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from hello mediaElement_ManifestReady event handler 
        // tooretrieve hello streams and populate them toohello local data members.
        public void getStreams(Manifest manifestObject)
        {
            availableStreams = new List<Stream>();
            availableVideoStreams = new List<Stream>();
            availableAudioStreams = new List<Stream>();
            availableTextStreams = new List<Stream>();
   
            try
            {
                for (int i = 0; i<manifestObject.AvailableStreams.Count; i++)
                {
                    Stream newStream = new Stream(manifestObject.AvailableStreams[i]);
                    newStream.isChecked = false;
   
                    //populate hello stream lists based on hello types
                    availableStreams.Add(newStream);
   
                    switch (newStream.ManifestStream.Type)
                    {
                        case MediaStreamType.Video:
                            availableVideoStreams.Add(newStream);
                            break;
                        case MediaStreamType.Audio:
                            availableAudioStreams.Add(newStream);
                            break;
                        case MediaStreamType.Text:
                            availableTextStreams.Add(newStream);
                            break;
                    }
   
                    // Select hello default selected streams from hello manifest.
                    for (int j = 0; j<manifestObject.SelectedStreams.Count; j++)
                    {
                        string selectedStreamName = manifestObject.SelectedStreams[j].Name;
                        if (selectedStreamName.Equals(newStream.Name))
                        {
                            newStream.isChecked = true;
                            break;
                        }
                    }
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function set hello list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update hello stream check box list on hello UI
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableStreams.ItemsSource = availableStreams; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function creates a selected streams list
        private void createSelectedStreamsList(List<IManifestStream> selectedStreams)
        {
            bool isOneVideoSelected = false;
            bool isOneAudioSelected = false;
   
            // Only one video stream can be selected
            for (int j = 0; j<availableVideoStreams.Count; j++)
            {
                if (availableVideoStreams[j].isChecked && (!isOneVideoSelected))
                {
                    selectedStreams.Add(availableVideoStreams[j].ManifestStream);
                    isOneVideoSelected = true;
                }
            }
   
            // Select hello frist video stream from hello list if no video stream is selected
            if (!isOneVideoSelected)
            {
                availableVideoStreams[0].isChecked = true;
                selectedStreams.Add(availableVideoStreams[0].ManifestStream);
            }
   
            // Only one audio stream can be selected
            for (int j = 0; j<availableAudioStreams.Count; j++)
            {
                if (availableAudioStreams[j].isChecked && (!isOneAudioSelected))
                {
                    selectedStreams.Add(availableAudioStreams[j].ManifestStream);
                    isOneAudioSelected = true;
                    txtStatus.Text = "hello audio stream is changed too" + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select hello frist audio stream from hello list if no audio steam is selected.
            if (!isOneAudioSelected)
            {
                availableAudioStreams[0].isChecked = true;
                selectedStreams.Add(availableAudioStreams[0].ManifestStream);
            }
   
            // Multiple text streams are supported.
            for (int j = 0; j < availableTextStreams.Count; j++)
            {
                if (availableTextStreams[j].isChecked)
                {
                    selectedStreams.Add(availableTextStreams[j].ManifestStream);
                }
            }
        }
   
        // Change streams on a smooth streaming presentation with multiple video streams.
        private async void changeStreams(List<IManifestStream> selectStreams)
        {
            try
            {
                IReadOnlyList<IStreamChangedResult> returnArgs =
                    await manifestObject.SelectStreamsAsync(selectStreams);
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
        #endregion stream selection
5. <span data-ttu-id="4749e-283">Recherchez hello mediaElement_ManifestReady méthode, ajoutez hello suivant du code à la fin de hello de fonction hello :</span><span class="sxs-lookup"><span data-stu-id="4749e-283">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="4749e-284">Par conséquent, lorsque le manifeste de MediaElement est prêt, hello code obtient une liste de flux de données disponible hello et remplit la zone de liste de l’interface utilisateur de hello avec la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="4749e-284">So when MediaElement manifest is ready, hello code gets a list of hello available streams, and populates hello UI list box with hello list.</span></span>
6. <span data-ttu-id="4749e-285">À l’intérieur de hello classe MainPage, recherchez hello UI boutons cliquez sur la région d’événements et ajoutez hello après la définition de fonction :</span><span class="sxs-lookup"><span data-stu-id="4749e-285">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="4749e-286">**application de hello toocompile et de test**</span><span class="sxs-lookup"><span data-stu-id="4749e-286">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="4749e-287">Appuyez sur **F6** projet hello de toocompile.</span><span class="sxs-lookup"><span data-stu-id="4749e-287">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="4749e-288">Appuyez sur **F5** application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="4749e-288">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="4749e-289">Haut hello du application hello, vous pouvez utiliser la valeur par défaut de hello URL de diffusion en continu lisse ou entrez un nom différent.</span><span class="sxs-lookup"><span data-stu-id="4749e-289">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="4749e-290">Cliquez sur **Définir la source**.</span><span class="sxs-lookup"><span data-stu-id="4749e-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="4749e-291">langue par défaut de Hello est audio_eng.</span><span class="sxs-lookup"><span data-stu-id="4749e-291">hello default language is audio_eng.</span></span> <span data-ttu-id="4749e-292">Essayez tooswitch entre audio_eng et audio_es.</span><span class="sxs-lookup"><span data-stu-id="4749e-292">Try tooswitch between audio_eng and audio_es.</span></span> <span data-ttu-id="4749e-293">Chaque fois que vous, vous sélectionnez un flux de données, vous devez cliquer sur bouton d’envoi hello.</span><span class="sxs-lookup"><span data-stu-id="4749e-293">Everytime, you select a new stream, you must click hello Submit button.</span></span>

<span data-ttu-id="4749e-294">Vous avez terminé la leçon 3.</span><span class="sxs-lookup"><span data-stu-id="4749e-294">You have completed lesson 3.</span></span>  <span data-ttu-id="4749e-295">Dans cette leçon, vous ajoutez des flux toochoose hello fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4749e-295">In this lesson, you add hello functionality toochoose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="4749e-296">Leçon 4 : sélectionner les pistes de diffusion en continu lisse</span><span class="sxs-lookup"><span data-stu-id="4749e-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="4749e-297">Une présentation de diffusion en continu lisse peut contenir plusieurs fichiers vidéo encodés comportant des niveaux de qualité (débit) et des résolutions différents.</span><span class="sxs-lookup"><span data-stu-id="4749e-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="4749e-298">Dans cette leçon, vous allez activer les utilisateurs tooselect pistes.</span><span class="sxs-lookup"><span data-stu-id="4749e-298">In this lesson, you will enable users tooselect tracks.</span></span> <span data-ttu-id="4749e-299">Cette leçon contient hello procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="4749e-299">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="4749e-300">Modifier le fichier XAML de hello</span><span class="sxs-lookup"><span data-stu-id="4749e-300">Modify hello XAML file</span></span>
2. <span data-ttu-id="4749e-301">Modifier le fichier de behand code hello</span><span class="sxs-lookup"><span data-stu-id="4749e-301">Modify hello code behand file</span></span>
3. <span data-ttu-id="4749e-302">Compiler et tester l’application hello</span><span class="sxs-lookup"><span data-stu-id="4749e-302">Compile and test hello application</span></span>

<span data-ttu-id="4749e-303">**fichier XAML de hello toomodify**</span><span class="sxs-lookup"><span data-stu-id="4749e-303">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="4749e-304">Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Concepteur de vues**.</span><span class="sxs-lookup"><span data-stu-id="4749e-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="4749e-305">Recherchez hello &lt;grille&gt; balise avec le nom de hello **gridStreamAndBitrateSelection**, ajouter hello suivant du code à fin hello de balise de hello :</span><span class="sxs-lookup"><span data-stu-id="4749e-305">Locate hello &lt;Grid&gt; tag with hello name **gridStreamAndBitrateSelection**, append hello following code at hello end of hello tag:</span></span>
   
         <StackPanel Name="spBitRateSelection" Grid.Row="1" Grid.Column="1">
         <StackPanel Orientation="Horizontal">
             <TextBlock Name="tbBitRate" Text="Available Bitrates:" FontSize="16" VerticalAlignment="Center"/>
             <Button Name="btnChangeTracks" Content="Submit" Click="btnChangeTrack_Click" />
         </StackPanel>
         <ListBox x:Name="lbAvailableVideoTracks" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                  ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
             <ListBox.ItemTemplate>
                 <DataTemplate>
                     <CheckBox Content="{Binding Bitrate}" IsChecked="{Binding isChecked, Mode=TwoWay}"/>
                 </DataTemplate>
             </ListBox.ItemTemplate>
         </ListBox>
         </StackPanel>
3. <span data-ttu-id="4749e-306">Appuyez sur **CTRL + S** toosave il change.</span><span class="sxs-lookup"><span data-stu-id="4749e-306">Press **CTRL+S** toosave he changes</span></span>

<span data-ttu-id="4749e-307">**toomodify hello fichier code-behind**</span><span class="sxs-lookup"><span data-stu-id="4749e-307">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="4749e-308">Dans l'Explorateur de solutions, cliquez avec le bouton droit sur **MainPage.xaml**, puis cliquez sur **Afficher le code**.</span><span class="sxs-lookup"><span data-stu-id="4749e-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="4749e-309">Au sein de l’espace de noms SSPlayer hello, ajoutez une nouvelle classe :</span><span class="sxs-lookup"><span data-stu-id="4749e-309">Inside hello SSPlayer namespace, add a new class:</span></span>
   
        #region class Track
        public class Track
        {
            private IManifestTrack trackInfo;
            public string _bitrate;
            public bool isCheckedValue;
   
            public IManifestTrack TrackInfo
            {
                get { return trackInfo; }
                set { trackInfo = value; }
            }
   
            public string Bitrate
            {
                get { return _bitrate; }
                set { _bitrate = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    isCheckedValue = value;
                }
            }
   
            public Track(IManifestTrack trackInfoIn)
            {
                trackInfo = trackInfoIn;
                _bitrate = trackInfoIn.Bitrate.ToString();
            }
            //public Track() { }
        }
        #endregion class Track
3. <span data-ttu-id="4749e-310">Au début de hello Hello classe MainPage, ajoutez hello suivant des définitions de variables :</span><span class="sxs-lookup"><span data-stu-id="4749e-310">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="4749e-311">Au sein de hello classe MainPage, ajoutez hello suivant région :</span><span class="sxs-lookup"><span data-stu-id="4749e-311">Inside hello MainPage class, add hello following region:</span></span>
   
        #region track selection
        /// <summary>
        /// Functionality tooselect video streams
        /// </summary>
   
        /// This Function gets hello tracks for hello selected video stream
        public void getTracks(Manifest manifestObject)
        {
            availableTracks = new List<Track>();
   
            IManifestStream videoStream = getVideoStream();
            IReadOnlyList<IManifestTrack> availableTracksLocal = videoStream.AvailableTracks;
            IReadOnlyList<IManifestTrack> selectedTracksLocal = videoStream.SelectedTracks;
   
            try
            {
                for (int i = 0; i < availableTracksLocal.Count; i++)
                {
                    Track thisTrack = new Track(availableTracksLocal[i]);
                    thisTrack.isChecked = true;
   
                    for (int j = 0; j < selectedTracksLocal.Count; j++)
                    {
                        string selectedTrackName = selectedTracksLocal[j].Bitrate.ToString();
                        if (selectedTrackName.Equals(thisTrack.Bitrate))
                        {
                            thisTrack.isChecked = true;
                            break;
                        }
                    }
                    availableTracks.Add(thisTrack);
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = e.Message;
            }
        }
   
        // This function gets hello video stream that is playing
        private IManifestStream getVideoStream()
        {
            IManifestStream videoStream = null;
            for (int i = 0; i < manifestObject.SelectedStreams.Count; i++)
            {
                if (manifestObject.SelectedStreams[i].Type == MediaStreamType.Video)
                {
                    videoStream = manifestObject.SelectedStreams[i];
                    break;
                }
            }
            return videoStream;
        }
   
        // This function set hello UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update hello track check box list on hello UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of hello selected tracks.
        private void createSelectedTracksList(List<IManifestTrack> selectedTracks)
        {
            // Create a list of selected tracks
            for (int j = 0; j < availableTracks.Count; j++)
            {
                if (availableTracks[j].isCheckedValue == true)
                {
                    selectedTracks.Add(availableTracks[j].TrackInfo);
                }
            }
        }
   
        // This function selects hello tracks based on user selection 
        private void changeTracks(List<IManifestTrack> selectedTracks)
        {
            IManifestStream videoStream = getVideoStream();
            try
            {
                videoStream.SelectTracks(selectedTracks);
            }
            catch (Exception ex)
            {
                txtStatus.Text = ex.Message;
            }
        }
        #endregion track selection
5. <span data-ttu-id="4749e-312">Recherchez hello mediaElement_ManifestReady méthode, ajoutez hello suivant du code à la fin de hello de fonction hello :</span><span class="sxs-lookup"><span data-stu-id="4749e-312">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="4749e-313">À l’intérieur de hello classe MainPage, recherchez hello UI boutons cliquez sur la région d’événements et ajoutez hello après la définition de fonction :</span><span class="sxs-lookup"><span data-stu-id="4749e-313">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="4749e-314">**application de hello toocompile et de test**</span><span class="sxs-lookup"><span data-stu-id="4749e-314">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="4749e-315">Appuyez sur **F6** projet hello de toocompile.</span><span class="sxs-lookup"><span data-stu-id="4749e-315">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="4749e-316">Appuyez sur **F5** application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="4749e-316">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="4749e-317">Haut hello du application hello, vous pouvez utiliser la valeur par défaut de hello URL de diffusion en continu lisse ou entrez un nom différent.</span><span class="sxs-lookup"><span data-stu-id="4749e-317">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="4749e-318">Cliquez sur **Définir la source**.</span><span class="sxs-lookup"><span data-stu-id="4749e-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="4749e-319">Par défaut, toutes les pistes hello du flux vidéo de hello sont sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="4749e-319">By default, all of hello tracks of hello video stream are selected.</span></span> <span data-ttu-id="4749e-320">tooexperiment hello bit de taux de change, vous pouvez sélectionnez hello plus faible vitesse de transmission disponible, puis hello plus haute vitesse de transmission disponible.</span><span class="sxs-lookup"><span data-stu-id="4749e-320">tooexperiment hello bit rate changes, you can select hello lowest bit rate available, and then select hello highest bit rate available.</span></span> <span data-ttu-id="4749e-321">Vous devez cliquer sur Envoyer après chaque modification.</span><span class="sxs-lookup"><span data-stu-id="4749e-321">You must click Submit after each change.</span></span>  <span data-ttu-id="4749e-322">Vous pouvez voir les modifications de la qualité vidéo hello.</span><span class="sxs-lookup"><span data-stu-id="4749e-322">You can see hello video quality changes.</span></span>

<span data-ttu-id="4749e-323">Vous avez terminé la leçon 4.</span><span class="sxs-lookup"><span data-stu-id="4749e-323">You have completed lesson 4.</span></span>  <span data-ttu-id="4749e-324">Dans cette leçon, vous ajoutez hello fonctionnalité toochoose pistes.</span><span class="sxs-lookup"><span data-stu-id="4749e-324">In this lesson, you add hello functionality toochoose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="4749e-325">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="4749e-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="4749e-326">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="4749e-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="4749e-327">Autres ressources :</span><span class="sxs-lookup"><span data-stu-id="4749e-327">Other Resources:</span></span>
* [<span data-ttu-id="4749e-328">Comment toobuild une application Smooth Streaming Windows 8 JavaScript avec les fonctionnalités avancées</span><span class="sxs-lookup"><span data-stu-id="4749e-328">How toobuild a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="4749e-329">Présentation technique de la diffusion en continu lisse</span><span class="sxs-lookup"><span data-stu-id="4749e-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

