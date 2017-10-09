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
## <a name="setting-up-your-ios-application"></a>Configuration de votre application iOS

Cette section fournit des instructions pas à pas toocreate un nouveau toodemonstrate de projet comment toointegrate une application iOS (Swift) avec *connectez-vous avec Microsoft* afin qu’il peut interroger les API Web qui requièrent un jeton.

> Vous préférez toodownload de projet XCode de cet exemple à la place ? [Télécharger un projet](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) et ignorer toohello [étape de Configuration](#create-an-application-express) exemple de code hello tooconfigure avant l’exécution.


## <a name="install-carthage-toodownload-and-build-msal"></a>Installer les toodownload Carthage et générer MSAL
Gestionnaire de package de Carthage est utilisé pendant la période d’évaluation hello de MSAL : il s’intègre avec XCode tout en conservant la possibilité de hello pour la bibliothèque Microsoft toomake modifications toohello.

- Téléchargez et installez la version la plus récente de Carthage hello [ici](https://github.com/Carthage/Carthage/releases "Carthage les URL de téléchargement")

## <a name="creating-your-application"></a>Création de votre application

1.  Ouvrez Xcode et sélectionnez `Create a new Xcode project`.
2.  Sélectionnez `iOS` > `Single view Application` et cliquez sur *Next*.
3.  Donnez un nom de produit puis cliquez sur *Next*.
4.  Sélectionnez un dossier toocreate votre application et cliquez sur *créer*

## <a name="build-hello-msal-framework"></a>Build hello MSAL Framework

Suivez les instructions de hello sous toopull et puis générez la version la plus récente des bibliothèques MSAL à l’aide de Carthage hello :

1.  Ouvrez hello bash terminal et accédez le dossier racine de l’application toohello
2.  Hello copie ci-dessous et les coller dans hello bash terminal toocreate un fichier 'Cartfile' :

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
Copiez et collez hello ci-dessous. Cette commande extrait les dépendances dans un dossier Carthage/extractions, puis génère hello MSAL bibliothèque :
</li>
</ol>

```bash
carthage update
```

> processus Hello ci-dessus est utilisé toodownload et build hello bibliothèque d’authentification Microsoft (MSAL). MSAL gère l’acquisition, la mise en cache et actualisation utilisateur jetons utilisés tooaccess API protégé par hello Azure Active Directory v2.

## <a name="add-hello-msal-framework-tooyour-application"></a>Ajouter une application de tooyour framework hello MSAL
1.  Dans Xcode, ouvrez hello `General` onglet
2.  Accédez toohello `Linked Frameworks and Libraries` et cliquez sur`+`
3.  Sélectionnez `Add other…`.
4.  Sélectionnez : `Carthage` > `Build` > `iOS` > `MSAL.framework` et cliquez sur *Open*. Vous devez voir `MSAL.framework` ajouté toohello liste.
5.  Accédez trop`Build Phases` onglet, puis cliquez sur `+` icône, choisissez`New Run Script Phase`
6.  Ajouter hello suivant contenu toohello *zone de script*:

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Ajouter hello suivant trop<code>Input Files</code> en cliquant sur <code>+</code>:
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a>Création de l’interface utilisateur de votre application
Un fichier Main.storyboard doit être automatiquement créé dans le cadre de votre modèle de projet. Suivez les instructions de hello sous toocreate hello interface utilisateur d’application :

1.  Touche CTRL enfoncée et cliquez sur `Main.storyboard` toobring haut du menu contextuel de hello, puis cliquez sur :`Open As` > `Source Code`
2.  Remplacez hello `<scenes>` nœud avec le code hello ci-dessous :

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
