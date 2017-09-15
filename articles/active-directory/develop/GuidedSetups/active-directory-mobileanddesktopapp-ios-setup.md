---
title: "Prise en main d’Azure AD v2 iOS - Paramétrage | Microsoft Docs"
description: "Cet article explique comment les applications iOS (Swift) peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: d25353a61b2a60bff28aa0679d38110e77d19e64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
## <a name="setting-up-your-ios-application"></a><span data-ttu-id="de5e3-103">Configuration de votre application iOS</span><span class="sxs-lookup"><span data-stu-id="de5e3-103">Setting up your iOS application</span></span>

<span data-ttu-id="de5e3-104">Cette section fournit des instructions détaillées sur la façon de créer un projet pour illustrer comment intégrer une application iOS (Swift) avec l’option *Se connecter avec Microsoft* pour pouvoir interroger des API web qui nécessitent un jeton.</span><span class="sxs-lookup"><span data-stu-id="de5e3-104">This section provides step-by-step instructions for how to create a new project to demonstrate how to integrate an iOS application (Swift) with *Sign-In with Microsoft* so it can query Web APIs that require a token.</span></span>

> <span data-ttu-id="de5e3-105">Vous préférez télécharger le projet XCode de cet exemple ?</span><span class="sxs-lookup"><span data-stu-id="de5e3-105">Prefer to download this sample's XCode project instead?</span></span> <span data-ttu-id="de5e3-106">[Téléchargez un projet](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) et passez à l’étape [Configuration](#create-an-application-express) pour configurer l’exemple de code avant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="de5e3-106">[Download a project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing.</span></span>


## <a name="install-carthage-to-download-and-build-msal"></a><span data-ttu-id="de5e3-107">Installer Carthage pour télécharger et générer la bibliothèque MSAL</span><span class="sxs-lookup"><span data-stu-id="de5e3-107">Install Carthage to download and build MSAL</span></span>
<span data-ttu-id="de5e3-108">Le gestionnaire de package Carthage est utilisé pendant la période d’évaluation de la bibliothèque MSAL (Microsoft Authentication Library) : il s’intègre avec XCode tout en permettant à Microsoft de continuer à apporter des modifications à la bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="de5e3-108">Carthage package manager is used during the preview period of MSAL – it integrates with XCode while maintaining the ability for Microsoft to make changes to the library.</span></span>

- <span data-ttu-id="de5e3-109">Téléchargez et installez la dernière version de Carthage [ici](https://github.com/Carthage/Carthage/releases "URL de téléchargement de Carthage")</span><span class="sxs-lookup"><span data-stu-id="de5e3-109">Download and install the latest release of Carthage [here](https://github.com/Carthage/Carthage/releases "Carthage download URL")</span></span>

## <a name="creating-your-application"></a><span data-ttu-id="de5e3-110">Création de votre application</span><span class="sxs-lookup"><span data-stu-id="de5e3-110">Creating your application</span></span>

1.  <span data-ttu-id="de5e3-111">Ouvrez Xcode et sélectionnez `Create a new Xcode project`.</span><span class="sxs-lookup"><span data-stu-id="de5e3-111">Open Xcode and select `Create a new Xcode project`</span></span>
2.  <span data-ttu-id="de5e3-112">Sélectionnez `iOS` > `Single view Application` et cliquez sur *Next*.</span><span class="sxs-lookup"><span data-stu-id="de5e3-112">Select `iOS` > `Single view Application` and click *Next*</span></span>
3.  <span data-ttu-id="de5e3-113">Donnez un nom de produit puis cliquez sur *Next*.</span><span class="sxs-lookup"><span data-stu-id="de5e3-113">Give a product name and click *Next*</span></span>
4.  <span data-ttu-id="de5e3-114">Sélectionnez un dossier où créer votre application, puis cliquez sur *Créer*.</span><span class="sxs-lookup"><span data-stu-id="de5e3-114">Select a folder to create your app and click *Create*</span></span>

## <a name="build-the-msal-framework"></a><span data-ttu-id="de5e3-115">Générer l’infrastructure MSAL</span><span class="sxs-lookup"><span data-stu-id="de5e3-115">Build the MSAL Framework</span></span>

<span data-ttu-id="de5e3-116">Suivez les instructions ci-dessous pour extraire puis générer la version la plus récente des bibliothèques MSAL à l’aide de Carthage :</span><span class="sxs-lookup"><span data-stu-id="de5e3-116">Follow the instructions below to pull and then build the latest version of MSAL libraries using Carthage:</span></span>

1.  <span data-ttu-id="de5e3-117">Ouvrez le terminal de l’interpréteur de commandes Bash et accédez au dossier racine de l’application.</span><span class="sxs-lookup"><span data-stu-id="de5e3-117">Open the bash terminal and go to the App’s root folder</span></span>
2.  <span data-ttu-id="de5e3-118">Copiez le code ci-dessous et collez-le dans le terminal de l’interpréteur de commandes Bash pour créer un fichier « Cartfile » :</span><span class="sxs-lookup"><span data-stu-id="de5e3-118">Copy the below and paste in the bash terminal to create a ‘Cartfile’ file:</span></span>

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="de5e3-119">Copiez et collez le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="de5e3-119">Copy and paste the below.</span></span> <span data-ttu-id="de5e3-120">Cette commande récupère les dépendances dans un dossier Carthage/Checkouts, puis génère la bibliothèque MSAL :</span><span class="sxs-lookup"><span data-stu-id="de5e3-120">This command fetches dependencies into a Carthage/Checkouts folder, then builds the MSAL library:</span></span>
</li>
</ol>

```bash
carthage update
```

> <span data-ttu-id="de5e3-121">Le processus ci-dessus sert à télécharger et à générer la bibliothèque MSAL.</span><span class="sxs-lookup"><span data-stu-id="de5e3-121">The process above is used to download and build the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="de5e3-122">La bibliothèque MSAL gère l’acquisition, la mise en cache et l’actualisation des jetons utilisateur qui servent à accéder aux API protégées par Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="de5e3-122">MSAL handles acquiring, caching and refreshing user tokens used to access APIs protected by the Azure Active Directory v2.</span></span>

## <a name="add-the-msal-framework-to-your-application"></a><span data-ttu-id="de5e3-123">Ajouter l’infrastructure MSAL à votre application</span><span class="sxs-lookup"><span data-stu-id="de5e3-123">Add the MSAL framework to your application</span></span>
1.  <span data-ttu-id="de5e3-124">Dans Xcode, ouvrez l’onglet `General`.</span><span class="sxs-lookup"><span data-stu-id="de5e3-124">In Xcode, open the `General` tab</span></span>
2.  <span data-ttu-id="de5e3-125">Accédez à la section `Linked Frameworks and Libraries` et cliquez sur `+`.</span><span class="sxs-lookup"><span data-stu-id="de5e3-125">Go to the `Linked Frameworks and Libraries` section and click `+`</span></span>
3.  <span data-ttu-id="de5e3-126">Sélectionnez `Add other…`.</span><span class="sxs-lookup"><span data-stu-id="de5e3-126">Select `Add other…`</span></span>
4.  <span data-ttu-id="de5e3-127">Sélectionnez : `Carthage` > `Build` > `iOS` > `MSAL.framework` et cliquez sur *Open*.</span><span class="sxs-lookup"><span data-stu-id="de5e3-127">Select: `Carthage` > `Build` > `iOS` > `MSAL.framework` and click *Open*.</span></span> <span data-ttu-id="de5e3-128">`MSAL.framework` devrait être ajouté à la liste.</span><span class="sxs-lookup"><span data-stu-id="de5e3-128">You should see `MSAL.framework` added to the list.</span></span>
5.  <span data-ttu-id="de5e3-129">Accédez à l’onglet `Build Phases`, cliquez sur l’icône `+`, puis choisissez `New Run Script Phase`.</span><span class="sxs-lookup"><span data-stu-id="de5e3-129">Go to `Build Phases` tab, and click `+` icon, choose `New Run Script Phase`</span></span>
6.  <span data-ttu-id="de5e3-130">Ajoutez le contenu suivant à la *zone de script* :</span><span class="sxs-lookup"><span data-stu-id="de5e3-130">Add the following contents to the *script area*:</span></span>

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="de5e3-131">Ajoutez le code suivant à <code>Input Files</code> en cliquant sur <code>+</code> :</span><span class="sxs-lookup"><span data-stu-id="de5e3-131">Add the following to <code>Input Files</code> by clicking <code>+</code>:</span></span>
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a><span data-ttu-id="de5e3-132">Création de l’interface utilisateur de votre application</span><span class="sxs-lookup"><span data-stu-id="de5e3-132">Creating your application’s UI</span></span>
<span data-ttu-id="de5e3-133">Un fichier Main.storyboard doit être automatiquement créé dans le cadre de votre modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="de5e3-133">A Main.storyboard file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="de5e3-134">Suivez les instructions ci-dessous pour créer l’interface utilisateur de l’application :</span><span class="sxs-lookup"><span data-stu-id="de5e3-134">Follow the instructions below to create the app UI:</span></span>

1.  <span data-ttu-id="de5e3-135">Maintenez la touche Ctrl enfoncée et cliquez sur `Main.storyboard` pour faire apparaître le menu contextuel, puis cliquez sur : `Open As` > `Source Code`</span><span class="sxs-lookup"><span data-stu-id="de5e3-135">Control+click `Main.storyboard` to bring up the contextual menu, and then click: `Open As` > `Source Code`</span></span>
2.  <span data-ttu-id="de5e3-136">Remplacez le nœud `<scenes>` par le code ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="de5e3-136">Replace the `<scenes>` node with the code below:</span></span>

```xml
 <scenes>
    <scene sceneID="tne-QT-ifu">
        <objects>
            <viewController id="BYZ-38-t0r" customClass="ViewController" customModule="MSALiOS" customModuleProvider="target" sceneMemberID="viewController">
                <layoutGuides>
                    <viewControllerLayoutGuide type="top" id="y3c-jy-aDJ"/>
                    <viewControllerLayoutGuide type="bottom" id="wfy-db-euE"/>
                </layoutGuides>
                <view key="view" contentMode="scaleToFill" id="8bC-Xf-vdC">
                    <rect key="frame" x="0.0" y="0.0" width="375" height="667"/>
                    <autoresizingMask key="autoresizingMask" widthSizable="YES" heightSizable="YES"/>
                    <subviews>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Microsoft Authentication Library" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="ifd-fu-zjm">
                            <rect key="frame" x="64" y="28" width="246" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Logging" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="98g-dc-BPL">
                            <rect key="frame" x="16" y="277" width="62" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="2rX-Vv-T1i">
                            <rect key="frame" x="87" y="100" width="200" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Call Microsoft Graph API"/>
                            <connections>
                                <action selector="callGraphButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="Kx0-JL-Bv9"/>
                            </connections>
                        </button>
                        <textView clipsSubviews="YES" multipleTouchEnabled="YES" contentMode="scaleToFill" fixedFrame="YES" editable="NO" textAlignment="natural" selectable="NO" translatesAutoresizingMaskIntoConstraints="NO" id="qXW-2z-J7K">
                            <rect key="frame" x="16" y="324" width="343" height="291"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <color key="backgroundColor" white="1" alpha="1" colorSpace="calibratedWhite"/>
                            <accessibility key="accessibilityConfiguration">
                                <accessibilityTraits key="traits" updatesFrequently="YES"/>
                            </accessibility>
                            <fontDescription key="fontDescription" type="system" pointSize="14"/>
                            <textInputTraits key="textInputTraits" autocapitalizationType="sentences"/>
                        </textView>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="9u4-b8-vmX">
                            <rect key="frame" x="137" y="138" width="100" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Sign-Out"/>
                            <connections>
                                <action selector="signoutButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="kZT-P8-0Zy"/>
                            </connections>
                        </button>
                    </subviews>
                    <color key="backgroundColor" red="1" green="1" blue="1" alpha="1" colorSpace="custom" customColorSpace="sRGB"/>
                </view>
                <connections>
                    <outlet property="loggingText" destination="qXW-2z-J7K" id="uqO-Yw-AsK"/>
                    <outlet property="signoutButton" destination="9u4-b8-vmX" id="OCh-qk-ldv"/>
                </connections>
            </viewController>
            <placeholder placeholderIdentifier="IBFirstResponder" id="dkx-z0-nzr" sceneMemberID="firstResponder"/>
        </objects>
        <point key="canvasLocation" x="140" y="137.18140929535232"/>
    </scene>
</scenes>
```
