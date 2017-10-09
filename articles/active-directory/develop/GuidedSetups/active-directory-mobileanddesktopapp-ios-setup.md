---
title: "aaaAzure AD v2 iOS route - le programme d’installation | Documents Microsoft"
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
ms.openlocfilehash: 62c4ee9a2d4ccaec780bee09fb4bc34cff2eb6df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-ios-application"></a><span data-ttu-id="6edeb-103">Configuration de votre application iOS</span><span class="sxs-lookup"><span data-stu-id="6edeb-103">Setting up your iOS application</span></span>

<span data-ttu-id="6edeb-104">Cette section fournit des instructions pas à pas toocreate un nouveau toodemonstrate de projet comment toointegrate une application iOS (Swift) avec *connectez-vous avec Microsoft* afin qu’il peut interroger les API Web qui requièrent un jeton.</span><span class="sxs-lookup"><span data-stu-id="6edeb-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate an iOS application (Swift) with *Sign-In with Microsoft* so it can query Web APIs that require a token.</span></span>

> <span data-ttu-id="6edeb-105">Vous préférez toodownload de projet XCode de cet exemple à la place ?</span><span class="sxs-lookup"><span data-stu-id="6edeb-105">Prefer toodownload this sample's XCode project instead?</span></span> <span data-ttu-id="6edeb-106">[Télécharger un projet](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) et ignorer toohello [étape de Configuration](#create-an-application-express) exemple de code hello tooconfigure avant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="6edeb-106">[Download a project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


## <a name="install-carthage-toodownload-and-build-msal"></a><span data-ttu-id="6edeb-107">Installer les toodownload Carthage et générer MSAL</span><span class="sxs-lookup"><span data-stu-id="6edeb-107">Install Carthage toodownload and build MSAL</span></span>
<span data-ttu-id="6edeb-108">Gestionnaire de package de Carthage est utilisé pendant la période d’évaluation hello de MSAL : il s’intègre avec XCode tout en conservant la possibilité de hello pour la bibliothèque Microsoft toomake modifications toohello.</span><span class="sxs-lookup"><span data-stu-id="6edeb-108">Carthage package manager is used during hello preview period of MSAL – it integrates with XCode while maintaining hello ability for Microsoft toomake changes toohello library.</span></span>

- <span data-ttu-id="6edeb-109">Téléchargez et installez la version la plus récente de Carthage hello [ici](https://github.com/Carthage/Carthage/releases "Carthage les URL de téléchargement")</span><span class="sxs-lookup"><span data-stu-id="6edeb-109">Download and install hello latest release of Carthage [here](https://github.com/Carthage/Carthage/releases "Carthage download URL")</span></span>

## <a name="creating-your-application"></a><span data-ttu-id="6edeb-110">Création de votre application</span><span class="sxs-lookup"><span data-stu-id="6edeb-110">Creating your application</span></span>

1.  <span data-ttu-id="6edeb-111">Ouvrez Xcode et sélectionnez `Create a new Xcode project`.</span><span class="sxs-lookup"><span data-stu-id="6edeb-111">Open Xcode and select `Create a new Xcode project`</span></span>
2.  <span data-ttu-id="6edeb-112">Sélectionnez `iOS` > `Single view Application` et cliquez sur *Next*.</span><span class="sxs-lookup"><span data-stu-id="6edeb-112">Select `iOS` > `Single view Application` and click *Next*</span></span>
3.  <span data-ttu-id="6edeb-113">Donnez un nom de produit puis cliquez sur *Next*.</span><span class="sxs-lookup"><span data-stu-id="6edeb-113">Give a product name and click *Next*</span></span>
4.  <span data-ttu-id="6edeb-114">Sélectionnez un dossier toocreate votre application et cliquez sur *créer*</span><span class="sxs-lookup"><span data-stu-id="6edeb-114">Select a folder toocreate your app and click *Create*</span></span>

## <a name="build-hello-msal-framework"></a><span data-ttu-id="6edeb-115">Build hello MSAL Framework</span><span class="sxs-lookup"><span data-stu-id="6edeb-115">Build hello MSAL Framework</span></span>

<span data-ttu-id="6edeb-116">Suivez les instructions de hello sous toopull et puis générez la version la plus récente des bibliothèques MSAL à l’aide de Carthage hello :</span><span class="sxs-lookup"><span data-stu-id="6edeb-116">Follow hello instructions below toopull and then build hello latest version of MSAL libraries using Carthage:</span></span>

1.  <span data-ttu-id="6edeb-117">Ouvrez hello bash terminal et accédez le dossier racine de l’application toohello</span><span class="sxs-lookup"><span data-stu-id="6edeb-117">Open hello bash terminal and go toohello App’s root folder</span></span>
2.  <span data-ttu-id="6edeb-118">Hello copie ci-dessous et les coller dans hello bash terminal toocreate un fichier 'Cartfile' :</span><span class="sxs-lookup"><span data-stu-id="6edeb-118">Copy hello below and paste in hello bash terminal toocreate a ‘Cartfile’ file:</span></span>

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
<span data-ttu-id="6edeb-119">Copiez et collez hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="6edeb-119">Copy and paste hello below.</span></span> <span data-ttu-id="6edeb-120">Cette commande extrait les dépendances dans un dossier Carthage/extractions, puis génère hello MSAL bibliothèque :</span><span class="sxs-lookup"><span data-stu-id="6edeb-120">This command fetches dependencies into a Carthage/Checkouts folder, then builds hello MSAL library:</span></span>
</li>
</ol>

```bash
carthage update
```

> <span data-ttu-id="6edeb-121">processus Hello ci-dessus est utilisé toodownload et build hello bibliothèque d’authentification Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="6edeb-121">hello process above is used toodownload and build hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="6edeb-122">MSAL gère l’acquisition, la mise en cache et actualisation utilisateur jetons utilisés tooaccess API protégé par hello Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="6edeb-122">MSAL handles acquiring, caching and refreshing user tokens used tooaccess APIs protected by hello Azure Active Directory v2.</span></span>

## <a name="add-hello-msal-framework-tooyour-application"></a><span data-ttu-id="6edeb-123">Ajouter une application de tooyour framework hello MSAL</span><span class="sxs-lookup"><span data-stu-id="6edeb-123">Add hello MSAL framework tooyour application</span></span>
1.  <span data-ttu-id="6edeb-124">Dans Xcode, ouvrez hello `General` onglet</span><span class="sxs-lookup"><span data-stu-id="6edeb-124">In Xcode, open hello `General` tab</span></span>
2.  <span data-ttu-id="6edeb-125">Accédez toohello `Linked Frameworks and Libraries` et cliquez sur`+`</span><span class="sxs-lookup"><span data-stu-id="6edeb-125">Go toohello `Linked Frameworks and Libraries` section and click `+`</span></span>
3.  <span data-ttu-id="6edeb-126">Sélectionnez `Add other…`.</span><span class="sxs-lookup"><span data-stu-id="6edeb-126">Select `Add other…`</span></span>
4.  <span data-ttu-id="6edeb-127">Sélectionnez : `Carthage` > `Build` > `iOS` > `MSAL.framework` et cliquez sur *Open*.</span><span class="sxs-lookup"><span data-stu-id="6edeb-127">Select: `Carthage` > `Build` > `iOS` > `MSAL.framework` and click *Open*.</span></span> <span data-ttu-id="6edeb-128">Vous devez voir `MSAL.framework` ajouté toohello liste.</span><span class="sxs-lookup"><span data-stu-id="6edeb-128">You should see `MSAL.framework` added toohello list.</span></span>
5.  <span data-ttu-id="6edeb-129">Accédez trop`Build Phases` onglet, puis cliquez sur `+` icône, choisissez`New Run Script Phase`</span><span class="sxs-lookup"><span data-stu-id="6edeb-129">Go too`Build Phases` tab, and click `+` icon, choose `New Run Script Phase`</span></span>
6.  <span data-ttu-id="6edeb-130">Ajouter hello suivant contenu toohello *zone de script*:</span><span class="sxs-lookup"><span data-stu-id="6edeb-130">Add hello following contents toohello *script area*:</span></span>

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="6edeb-131">Ajouter hello suivant trop<code>Input Files</code> en cliquant sur <code>+</code>:</span><span class="sxs-lookup"><span data-stu-id="6edeb-131">Add hello following too<code>Input Files</code> by clicking <code>+</code>:</span></span>
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a><span data-ttu-id="6edeb-132">Création de l’interface utilisateur de votre application</span><span class="sxs-lookup"><span data-stu-id="6edeb-132">Creating your application’s UI</span></span>
<span data-ttu-id="6edeb-133">Un fichier Main.storyboard doit être automatiquement créé dans le cadre de votre modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="6edeb-133">A Main.storyboard file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="6edeb-134">Suivez les instructions de hello sous toocreate hello interface utilisateur d’application :</span><span class="sxs-lookup"><span data-stu-id="6edeb-134">Follow hello instructions below toocreate hello app UI:</span></span>

1.  <span data-ttu-id="6edeb-135">Touche CTRL enfoncée et cliquez sur `Main.storyboard` toobring haut du menu contextuel de hello, puis cliquez sur :`Open As` > `Source Code`</span><span class="sxs-lookup"><span data-stu-id="6edeb-135">Control+click `Main.storyboard` toobring up hello contextual menu, and then click: `Open As` > `Source Code`</span></span>
2.  <span data-ttu-id="6edeb-136">Remplacez hello `<scenes>` nœud avec le code hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="6edeb-136">Replace hello `<scenes>` node with hello code below:</span></span>

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
