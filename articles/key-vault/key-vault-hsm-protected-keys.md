---
title: "aaaHow toogenerate transfert protégée par HSM clés et d’Azure Key Vault | Documents Microsoft"
description: "Utilisez cette toohelp article vous planifiez, générez et transférez votre propre toouse clés protégées par HSM avec Azure Key Vault. Cette méthode est également appelée BYOK (Bring Your Own Key, ou apportez votre propre clé)."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a>Comment toogenerate et transfert de clés protégées par HSM pour Azure Key Vault
## <a name="introduction"></a>Introduction
Pour plus de sûreté, lorsque vous utilisez le coffre de clés Azure, vous pouvez importer ou générer des clés dans les modules de sécurité matériel (HSM) qui ne quittent jamais les limites HSM hello. Ce scénario est souvent désignée tooas *mettre votre propre clé*, ou BYOK. Hello HSM sont FIPS 140-2 niveau 2 validé. Coffre de clés Azure utilise famille nShield de Thales de modules de sécurité matériels tooprotect vos clés.

Utilisez les informations de hello dans cette toohelp de rubrique, vous planifiez, générez et transférez votre propre toouse clés protégées par HSM avec Azure Key Vault.

Cette fonctionnalité n’est pas disponible pour Azure en Chine.

> [!NOTE]
> Pour plus d’informations sur le coffre de clés Azure, consultez la page [Présentation du coffre de clés Azure](key-vault-whatis.md)  
>
> Pour voir un didacticiel de mise en route incluant un coffre de clés pour les clés protégées par HSM, consultez la section [Prise en main du coffre de clés Azure](key-vault-get-started.md).
>
>

Plus d’informations sur la génération et transfert d’une clé protégée par HSM sur hello Internet :

* Vous générez la clé de hello à partir d’une station de travail hors connexion, ce qui réduit la surface d’attaque hello.
* clé de Hello est chiffré avec une clé d’échange de clé (clés), qui reste chiffrée jusqu'à ce qu’il est transféré toohello HSM de coffre de clés Azure. Hello uniquement une version chiffrée de votre clé quitte la station de travail d’origine hello.
* ensemble d’outils Hello définit des propriétés sur votre clé de locataire qui lie votre clé toohello monde de sécurité Azure Key Vault. Par conséquent, après que HSM de coffre de clés Azure hello reçu et déchiffré votre clé, ils sont les seuls pouvez l’utiliser. Il est impossible d’exporter votre clé. Cette liaison est appliquée par hello de sécurité matériels Thales.
* Hello Key Exchange Key (KEK) qui est utilisé tooencrypt votre clé est générée au sein des HSM de coffre de clés Azure hello et n’est pas exportable. les modules HSM Hello appliquent qu’il ne peut y avoir aucune version claire de hello veillent à l’extérieur de hello HSM. En outre, ensemble d’outils hello inclut une attestation de Thales indiquant que hello n’est pas exportable et a été généré à l’intérieur d’un HSM authentique conçu par Thales.
* ensemble d’outils Hello inclut une attestation de Thales indiquant que le coffre de clés Azure monde de sécurité a également été généré sur un module de sécurité matériel authentique conçu par Thales hello. Cette attestation s’avère tooyou que Microsoft utilise du matériel authentique.
* Microsoft utilise des KEK et des mondes de sécurité séparés dans chaque région géographique. Cette séparation garantit que votre clé peut être utilisée uniquement dans les centres de données dans la région de hello dans lequel vous l’avez chiffrée. Par exemple, la clé d’un client européen ne peut pas être utilisée dans des centres de données d’Amérique du Nord ou d’ Asie.

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a>Autres informations sur les services de sécurité matériels Thales et Microsoft
Thales e-Security est des principaux fournisseurs mondiaux le chiffrement des données et des services financiers cyber sécurité solutions toohello haute technologie, fabrication, gouvernement et secteurs de la technologie. Avec un 40 ans de protection et les gouvernements des informations, les solutions Thales sont utilisées par quatre hello cinq plus grandes aérospatial d’énergie et de sociétés de. Leurs solutions sont également utilisées par 22 pays de l’OTAN, et sécurisent plus de 80 % des transactions de paiement dans le monde.

Microsoft a collaboré avec l’état de hello Thales tooenhance clipart modules de sécurité matériels. Ces améliorations permettent d’avantages de types hello tooget des services hébergés sans renoncer au contrôle de vos clés. Plus précisément, ces améliorations permettent à Microsoft de gérer hello modules de sécurité matériels afin que vous n’avez pas à. Comme un cloud que service, Azure Key Vault passe à la mention abrégée toomeet pics se produisent l’utilisation de votre organisation. AT hello même temps, votre clé est protégée à l’intérieur de Microsoft : vous conservez le contrôle hello son cycle de vie, car vous générez hello clé et la transférez HSM du tooMicrosoft.

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a>Mise en œuvre du principe BYOK (Apportez votre propre clé, pour le coffre de clés Azure
Hello d’utilisation suivante des informations et des procédures si vous allez générer votre propre clé protégée par HSM et transférez-le tooAzure le coffre de clés : hello apportez votre propre scénario key (BYOK).

## <a name="prerequisites-for-byok"></a>Configuration requise pour BYOK
Consultez hello tableau pour obtenir la liste des composants requis pour mettre votre propre key (BYOK) pour Azure Key Vault.

| Prérequis | Plus d’informations |
| --- | --- |
| Un abonnement tooAzure |toocreate un coffre de clés Azure, vous avez besoin d’un abonnement Azure : [s’inscrire pour la version d’évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/) |
| clés protégées par HSM Hello Azure Key Vault Premium service couche toosupport |Pour plus d’informations sur les fonctionnalités et les niveaux de service hello pour Azure Key Vault, consultez hello [tarification d’Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/) site Web. |
| Modules de sécurité matérielle, cartes à puces et logiciel d’assistance de Thales |Vous devez avoir accès tooa Module de sécurité matériel Thales et opérationnelle notions de sécurité matériels Thales. Consultez [Module de sécurité matériel Thales](https://www.thales-esecurity.com/msrms/buy) pour la liste des modèles compatibles ou toopurchase un HSM si vous n’avez pas un hello. |
| Hello matériel et logiciels suivants :<ol><li>Une station de travail x64 hors connexion avec le système d’exploitation Windows 7 ou version ultérieure, et le logiciel Thales nShield version 11.50 ou ultérieure.<br/><br/>Si cette station de travail exécute Windows 7, vous devez [installer Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</li><li>Une station de travail qui est connecté toohello Internet et possède un système d’exploitation Windows minimal de Windows 7 et [Azure PowerShell](/powershell/azure/overview) **minimale version 1.1.0** installé.</li><li>Un lecteur USB ou tout autre appareil de stockage portable offrant au moins 16 Mo d’espace libre.</li></ol> |Pour des raisons de sécurité, nous vous recommandons de que cette première station de travail hello n’est pas connecté tooa réseau. Toutefois, cette recommandation n’est pas appliquée par programmation.<br/><br/>Notez que dans les instructions hello ci-après, cette station de travail est désignée tooas hello déconnecté station de travail.</p></blockquote><br/>En outre, si votre clé de locataire est pour un réseau de production, nous vous recommandons d’utiliser un deuxième poste de travail toodownload hello ensemble d’outils et de téléchargement hello clé de locataire. Mais à des fins de test, vous pouvez utiliser hello même station de travail comme hello premier.<br/><br/>Notez que dans les instructions hello ci-après, cette deuxième station de travail est station de travail référencé tooas hello connecté à Internet.</p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a>Générer et transférer votre clé tooAzure HSM pour coffre de clés
Vous allez utiliser hello suivant cinq étapes toogenerate et transférer votre clé tooan HSM pour coffre de clés Azure :

* [Étape 1 : Préparez votre station de travail connectée à Internet](#step-1-prepare-your-internet-connected-workstation)
* [Étape 2 : Préparez votre station de travail déconnectée](#step-2-prepare-your-disconnected-workstation)
* [Étape 3 : Générez votre clé](#step-3-generate-your-key)
* [Étape 4 : Réparez votre clé pour le transfert](#step-4-prepare-your-key-for-transfer)
* [Étape 5 : Transférer votre clé tooAzure le coffre de clés](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a>Étape 1 : Préparez votre station de travail connectée à Internet
Pour cette première étape, hello procédures suivantes sur votre station de travail qui est connecté toohello Internet.

### <a name="step-11-install-azure-powershell"></a>Étape 1.1 : installer Azure PowerShell
À partir de hello Internet station de travail connectée, téléchargez et installez les module PowerShell Azure hello qui inclut des applets de commande de hello toomanage Azure Key Vault. Cela nécessite au moins la version 0.8.13.

Pour obtenir des instructions d’installation, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

### <a name="step-12-get-your-azure-subscription-id"></a>Étape 1.2 : Obtenez votre ID d’abonnement Azure.
Démarrez une session Azure PowerShell et connectez-vous tooyour compte Azure à l’aide de hello de commande suivante :

        Add-AzureAccount
Dans la fenêtre contextuelle du navigateur de hello, entrez votre nom d’utilisateur de compte Azure et un mot de passe. Ensuite, utilisez hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) commande :

        Get-AzureSubscription
À partir de la sortie de hello, recherchez les ID de hello pour l’abonnement hello que vous utiliserez pour Azure Key Vault. Vous aurez besoin cet ID d’abonnement ultérieurement.

Ne fermez pas la fenêtre d’Azure PowerShell hello.

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a>Étape 1.3 : Télécharger un ensemble d’outils BYOK de hello pour Azure Key Vault
Accédez toohello Microsoft Download Center et [télécharger l’ensemble d’outils de la solution BYOK d’Azure Key Vault hello](http://www.microsoft.com/download/details.aspx?id=45345) pour votre instance Azure ou une région géographique. Utilisez hello suit hachage du package toodownload de nom package informations tooidentify hello et son SHA-256 correspondante :

- - -
**États-Unis**

KeyVault-BYOK-Tools-UnitedStates.zip

760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B

- - -
**Europe :**

KeyVault-BYOK-outils-Europe.zip

7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D

- - -
**Asie :**

KeyVault-BYOK-Tools-AsiaPacific.zip

813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8

- - -
**Amérique latine :**

KeyVault-BYOK-Tools-LatinAmerica.zip

3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0

- - -
**Japon :**

KeyVault-BYOK-Tools-Japan.zip

453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90

- - -
**Corée :**

KeyVault-BYOK-Tools-Korea.zip

C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A

- - -
**Australie :**

KeyVault-BYOK-Tools-Australia.zip

4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B

- - -
[**Azure Government :**](https://azure.microsoft.com/features/gov/)

KeyVault-BYOK-Tools-USGovCloud.zip

3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64

- - -
**Département de la Défense des États-Unis :**

KeyVault-BYOK-Tools-USGovernmentDoD.zip

A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D

- - -
**Canada :**

KeyVault-BYOK-Tools-Canada.zip

30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7

- - -
**Allemagne :**

KeyVault-BYOK-Tools-Germany.zip

5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261

- - -
**Inde :**

KeyVault-BYOK-Tools-India.zip

136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7

- - -
**Royaume-Uni :**

KeyVault-BYOK-Tools-UnitedKingdom.zip

ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268

- - -

l’intégrité de hello toovalidate de votre d’outils BYOK téléchargé, à partir de votre session Azure PowerShell, utilisez hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) applet de commande.

    Get-FileHash KeyVault-BYOK-Tools-*.zip

ensemble d’outils Hello inclut des éléments suivants de hello :

* Un package Key Exchange Key (KEK) dont le nom commence par **BYOK-KEK-pkg-**
* Un package Security World dont le nom commence par **BYOK-SecurityWorld-pkg-**
* Un script python nommé **verifykeypackage.py**.
* Un fichier exécutable de ligne de commande nommé **KeyTransferRemote.exe** et les DLL associées.
* Un package redistribuable Visual C++ nommé **vcredist_x64.exe**.

Copiez hello package tooa USB ou un autre support de stockage portable.

## <a name="step-2-prepare-your-disconnected-workstation"></a>Étape 2 : Préparez votre station de travail déconnectée
Pour cette deuxième étape, hello suivant les procédures de station de travail hello qui n’est pas connecté tooa réseau (hello Internet ou votre réseau interne).

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a>Étape 2.1 : Préparer la station de travail hello déconnecté de sécurité matériel Thales
Installer le logiciel de support nCipher (Thales) hello sur un ordinateur Windows, puis joignez un ordinateur toothat de sécurité matériel Thales.

Assurez-vous que hello des outils Thales se trouvent dans votre chemin d’accès (**%nfast_home%\bin**). Par exemple, tapez Bonjour suivante :

        set PATH=%PATH%;"%nfast_home%\bin"

Pour plus d’informations, consultez hello Guide d’utilisation inclus avec hello HSM Thales.

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a>Étape 2.2 : Ensemble d’outils installation hello BYOK sur la station de travail hello déconnecté
Copier le package de l’ensemble d’outils BYOK hello de hello USB ou un autre support de stockage portable, puis hello suivant :

1. Extrayez les fichiers de hello hello téléchargé package dans n’importe quel dossier.
2. Depuis ce dossier, exécutez vcredist_x64.exe.
3. Suivez les instructions de hello toohello installer les composants d’exécution hello Visual C++ pour Visual Studio 2013.

## <a name="step-3-generate-your-key"></a>Étape 3 : Générez votre clé
Pour cette troisième étape, hello suivant les procédures de station de travail hello déconnecté. toocomplete cette étape de votre module de sécurité matériel doit être en mode d’initialisation. 


### <a name="step-31-change-hello-hsm-mode-tooi"></a>Étape 3.1 : Modifier hello HSM mode too'I'
Si vous utilisez Thales nShield Edge, le mode hello toochange : 1. Utilisez hello Mode bouton toohighlight hello mode requis. 2. Après quelques secondes, maintenez effacer hello pendant quelques secondes. Si la modification du mode de hello, hello DEL du nouveau mode cesse de clignoter et reste allumé. Hello voyant d’état peut flash irrégulière pendant quelques secondes et puis clignote régulièrement lorsque le périphérique de hello est prêt. Dans le cas contraire, hello périphérique reste dans le mode actuel hello, avec le mode approprié hello voyant allumé.

### <a name="step-32-create-a-security-world"></a>Étape 3.2 : Créez un monde de sécurité
Démarrez une invite de commandes et exécutez hello programme de nouveau monde Thales.

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

Ce programme crée un **Security World** fichier % NFAST_KMDATA%\local\world, qui correspond toohello c:\programdata\ncipher\key Management C:\ProgramData\nCipher\Key dossier. Vous pouvez utiliser des valeurs différentes pour le quorum de hello, mais dans notre exemple, vous êtes tooenter demandées trois cartes et nuls pour chacun d’eux des codes confidentiels. Ensuite, deux des trois cartes donnent monde de sécurité toohello un accès complet. Ces cartes constituent hello **ensemble de cartes administrateur** nouveau monde de sécurité hello.

Puis la hello suivant :

* Sauvegardez le fichier de hello world. Sécuriser et protéger le fichier de hello world, les cartes administrateur hello et leurs codes confidentiels et assurez-vous ne qu’aucune personne seule toomore d’accès à une carte.

### <a name="step-33-change-hello-hsm-mode-tooo"></a>Étape 3.3 : Modifier hello HSM mode too'O'
Si vous utilisez Thales nShield Edge, le mode hello toochange : 1. Utilisez hello Mode bouton toohighlight hello mode requis. 2. Après quelques secondes, maintenez effacer hello pendant quelques secondes. Si la modification du mode de hello, hello DEL du nouveau mode cesse de clignoter et reste allumé. Hello voyant d’état peut flash irrégulière pendant quelques secondes et puis clignote régulièrement lorsque le périphérique de hello est prêt. Dans le cas contraire, hello périphérique reste dans le mode actuel hello, avec le mode approprié hello voyant allumé.


### <a name="step-34-validate-hello-downloaded-package"></a>Étape 3.4 : Valider le package de hello téléchargé
Cette étape est facultative mais recommandée afin que vous pouvez valider les éléments suivants de hello :

* Hello clé d’échange de clés qui est inclus dans l’ensemble d’outils hello a été généré à partir d’un HSM Thales authentique.
* hachage Hello Hello World de sécurité qui est inclus dans l’ensemble d’outils hello a été généré dans un HSM Thales authentique.
* Hello clé d’échange n’est pas exportable.

> [!NOTE]
> toovalidate hello téléchargé le package, hello HSM doit être connectée, sous tension et doit avoir un monde de sécurité (par exemple hello une que vous avez créé).
>
>

toovalidate hello téléchargé package :

1. Exécutez hello script verifykeypackage.py en tapant hello suivantes, selon votre région géographique ou d’une instance d’Azure :

   * Pour l’Amérique du Nord :

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * Pour l’Europe :

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * Pour l’Asie :

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * Pour l’Amérique latine :

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * Pour le Japon :

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * Pour la Corée :

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * Pour l’Australie :

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * Pour [Azure Government](https://azure.microsoft.com/features/gov/), qui utilise l’instance hello US government Azure :

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * Pour le Département de la Défense des États-Unis :

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * Pour le Canada :

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * Pour l’Allemagne :

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * Pour l’Inde :

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > Hello logiciel Thales inclut python à %NFAST_HOME%\python\bin
     >
     >
2. Vérifiez que vous voyez suivants de hello, qui indiquent une validation réussie : **résultat : réussite**

Ce script valide la chaîne de signataire hello des toohello clé racine Thales. hachage Hello de cette clé racine est incorporé dans le script de hello et sa valeur doit être **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**. Vous pouvez également confirmer cette valeur séparément en visitant hello [site Web de Thales](http://www.thalesesec.com/).

Vous êtes maintenant prêt toocreate une nouvelle clé.

### <a name="step-35-create-a-new-key"></a>Étape 3.5 : Créez une clé
Générer une clé à l’aide de hello Thales **generatekey** programme.

Exécutez hello commande toogenerate hello clé suivante :

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

Lorsque vous exécutez cette commande, utilisez ces instructions :

* Hello paramètre *protéger* doit avoir la valeur toohello valeur **module**, comme indiqué. Ce paramétrage crée une clé protégée par module. ensemble d’outils de Hello BYOK ne prend pas en charge les clés protégées par OCS.
* Remplacez la valeur hello *contosokey* pour hello **ident** et **plainname** avec une valeur de chaîne. toominimize charge administrative et de réduire hello risque d’erreurs, nous vous recommandons d’utiliser hello même valeur pour les deux. Hello **ident** valeur doit contenir uniquement des chiffres, des tirets et des lettres minuscules.
* Hello pubexp est vide (par défaut) dans cet exemple, mais vous pouvez spécifier des valeurs spécifiques. Pour plus d’informations, consultez hello documentation Thales.

Cette commande crée un fichier de clé Tokénisée dans votre dossier %NFAST_KMDATA%\local avec un nom commençant par **key_simple_**, suivi par hello **ident** qui a été spécifié dans la commande hello. Par exemple : **key_simple_contosokey**. Ce fichier contient une clé chiffrée.

Sauvegardez ce fichier de clé à jeton dans un emplacement sûr.

> [!IMPORTANT]
> Lorsque vous transférerez ultérieurement votre clé tooAzure le coffre de clés, Microsoft ne peut pas exporter cette clé tooyou précédent, il est donc extrêmement important de sauvegarder votre monde de sécurité et de la clé en toute sécurité. Contactez Thales pour connaître les conseils et meilleures pratiques pour sauvegarder votre clé.
>
>

Vous est désormais prêt tootransfer votre clé tooAzure le coffre de clés.

## <a name="step-4-prepare-your-key-for-transfer"></a>Étape 4 : Réparez votre clé pour le transfert
Pour cette étape quatrième, hello suivant les procédures de station de travail hello déconnecté.

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a>Étape 4.1 : Créez une copie de votre clé avec des autorisations réduites

Ouvrez une nouvelle invite de commandes et modifier hello actuel toohello emplacement du répertoire où vous avez décompressé le fichier zip BYOK hello. autorisations de hello tooreduce sur votre clé, à partir d’une invite de commandes, exécutez une des hello suivantes, selon votre région géographique ou d’une instance d’Azure :

* Pour l’Amérique du Nord :

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* Pour l’Europe :

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* Pour l’Asie :

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* Pour l’Amérique latine :

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* Pour le Japon :

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* Pour la Corée :

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* Pour l’Australie :

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* Pour [Azure Government](https://azure.microsoft.com/features/gov/), qui utilise l’instance hello US government Azure :

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* Pour le Département de la Défense des États-Unis :

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* Pour le Canada :

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* Pour l’Allemagne :

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* Pour l’Inde :

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

Lorsque vous exécutez cette commande, remplacez *contosokey* par hello même valeur spécifiée dans **étape 3.5 : créer une nouvelle clé** de hello [générer votre clé](#step-3-generate-your-key) étape.

Vous êtes invité tooplug dans vos cartes administrateur de monde de sécurité.

Commande hello issue, vous voyez **résultat : réussite** et copie hello de votre clé avec autorisations réduites sont dans le fichier hello nommé key_xferacId_<contosokey>.

Vous pouvez inspecte hello ACL à l’aide de l’aide des commandes suivantes hello aux utilitaires Thales :

* aclprint.py :

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* kmfile-dump.exe :

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  Lorsque vous exécutez ces commandes, remplacez contosokey hello même valeur que vous avez spécifié dans **étape 3.5 : créer une nouvelle clé** de hello [générer votre clé](#step-3-generate-your-key) étape.

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a>Étape 4.2 : Chiffrez votre clé à l’aide clé de Microsoft Exchange
Exécutez une des hello suivant de commandes, selon votre région géographique ou d’une instance d’Azure :

* Pour l’Amérique du Nord :

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Pour l’Europe :

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Pour l’Asie :

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Pour l’Amérique latine :

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Pour le Japon :

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Pour la Corée :

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Pour l’Australie :

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Pour [Azure Government](https://azure.microsoft.com/features/gov/), qui utilise l’instance hello US government Azure :

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Pour le Département de la Défense des États-Unis :

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Pour le Canada :

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Pour l’Allemagne :

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* Pour l’Inde :

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

Lorsque vous exécutez cette commande, utilisez ces instructions :

* Remplacez *contosokey* avec l’identificateur hello que vous avez utilisé la clé de hello toogenerate dans **étape 3.5 : créer une nouvelle clé** de hello [générer votre clé](#step-3-generate-your-key) étape.
* Remplacez *SubscriptionID* avec l’ID de hello Hello abonnement Azure qui contient votre coffre de clés. Vous avez extrait cette valeur auparavant, dans **étape 1.2 : obtenir votre ID d’abonnement Azure** de hello [préparer votre station de travail connectée à Internet](#step-1-prepare-your-internet-connected-workstation) étape.
* Remplacez *ContosoFirstHSMKey* par une étiquette à utiliser pour votre nom de fichier de sortie.

Lorsque cette opération terminée avec succès, elle affiche **résultat : réussite** et un nouveau fichier dans le dossier actuel hello a hello suivant le nom : KeyTransferPackage -*ContosoFirstHSMkey*.byok

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a>Étape 4.3 : Copie de transfert de clé package toohello connecté à Internet poste de travail
Utiliser un lecteur USB ou un autre fichier de sortie de stockage portable toocopy hello de hello précédente (KeyTransferPackage-ContosoFirstHSMkey.byok) d’étape tooyour connecté à Internet station de travail.

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a>Étape 5 : Transférer votre clé tooAzure le coffre de clés
Pour cette étape finale, sur hello Internet station de travail connectée, utilisez hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) applet de commande tooupload hello package de transfert clé que vous avez copié à partir de hello déconnecté de station de travail toohello HSM pour coffre de clés Azure :

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

Si hello téléchargement réussit, vous consultez les propriétés affichées hello de clé hello que vous venez d’ajouter.

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez maintenant utiliser cette clé protégée HSM dans votre coffre de clés. Pour plus d’informations, consultez hello **si vous souhaitez un module de sécurité matériel (HSM) de toouse** section Bonjour [prise en main d’Azure Key Vault](key-vault-get-started.md) didacticiel.
