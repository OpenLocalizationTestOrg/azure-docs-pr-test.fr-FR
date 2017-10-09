---
title: "Rendre hello lecteur D: d’un ordinateur virtuel un disque de données | Documents Microsoft"
description: "Décrit comment toochange lettres de lecteur une machine virtuelle Windows afin que vous pouvez utiliser le lecteur D: de hello comme un lecteur de données."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a>Utilisez le lecteur D: de hello comme un lecteur de données sur une machine virtuelle Windows
Si votre application doit toouse hello données toostore du lecteur D, suivez ces instructions de toouse une lettre de lecteur différente pour le disque temporaire de hello. Si vous n’utilisez jamais de données de toostore hello disque temporaire que vous avez besoin de tookeep.

Si vous redimensionnez ou **arrêtez (Désallouez)** un ordinateur virtuel, il peut déclencher la sélection élective de hello machine virtuelle tooa nouveau hyperviseur. Ce placement peut également être déclenché par un événement de maintenance planifié ou non planifié. Dans ce scénario, le disque temporaire de hello sera réaffecté toohello première lettre de lecteur disponible. Si vous avez une application qui nécessite plus précisément de lecteur D: de hello, vous devez toofollow ces étapes tootemporarily déplacement hello pagefile.sys, attachez un nouveau disque de données et lui attribuer hello lettre D, puis déplacement pagefile.sys de hello sauvegarder le lecteur temporaire de toohello. Une fois terminé, Azure ne prendre précédent hello D: si hello VM déplace l’hyperviseur de différents tooa.

Pour plus d’informations sur la façon dont Azure utilise le disque temporaire de hello, consultez [présentation lecteur temporaire de hello sur des Machines virtuelles Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="attach-hello-data-disk"></a>Attacher le disque de données hello
Vous devez tout d’abord, tooattach hello données disque toohello virtual machine. toodo ce à l’aide du portail de hello, consultez [tooattach une données managées de disque Bonjour Azure portal](attach-managed-disk-portal.md).

## <a name="temporarily-move-pagefilesys-tooc-drive"></a>Déplacer temporairement le fichier pagefile.sys tooC lecteur
1. Connecter l’ordinateur virtuel de toohello. 
2. Avec le bouton hello **Démarrer** menu et sélectionnez **système**.
3. Dans le menu de gauche hello, sélectionnez **les paramètres système avancés**.
4. Bonjour **performances** section, sélectionnez **paramètres**.
5. Sélectionnez hello **avancé** onglet.
6. Bonjour **mémoire virtuelle** section, sélectionnez **modification**.
7. Sélectionnez hello **C** lecteur, puis cliquez sur **taille gérée par le système** puis cliquez sur **définir**.
8. Sélectionnez hello **D** lecteur, puis cliquez sur **aucun fichier d’échange** puis cliquez sur **définir**.
9. Cliquez sur Appliquer. Vous obtiendrez un avertissement que toobe redémarré pour hello modifications tootake affectent a besoin de cet ordinateur hello.
10. Redémarrez l’ordinateur virtuel de hello.

## <a name="change-hello-drive-letters"></a>Modifier les lettres de lecteur hello
1. Une fois hello machine virtuelle redémarre, reconnectez-vous toohello machine virtuelle.
2. Cliquez sur hello **Démarrer** menu et le type **diskmgmt.msc** et appuyez sur ENTRÉE. La Gestion des disques démarre.
3. Avec le bouton droit sur **D**, hello lecteur de stockage temporaire, puis sélectionnez **modifier la lettre de lecteur et les chemins d’accès**.
4. Sous la lettre du lecteur, sélectionnez un nouveau lecteur (**T**, par exemple), puis cliquez sur **OK**. 
5. Avec le bouton droit sur le disque de données hello, puis sélectionnez **modifier la lettre de lecteur et les chemins d’accès**.
6. Sous la lettre de lecteur, sélectionnez le lecteur **D**, puis cliquez sur **OK**. 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a>Déplacer le lecteur de stockage temporaire pagefile.sys toohello précédent
1. Avec le bouton hello **Démarrer** menu et sélectionnez **système**
2. Dans le menu de gauche hello, sélectionnez **les paramètres système avancés**.
3. Bonjour **performances** section, sélectionnez **paramètres**.
4. Sélectionnez hello **avancé** onglet.
5. Bonjour **mémoire virtuelle** section, sélectionnez **modification**.
6. Sélectionnez le lecteur de hello du système d’exploitation **C** et cliquez sur **aucun fichier d’échange** puis cliquez sur **définir**.
7. Sélectionnez le lecteur de stockage temporaire hello **T** puis cliquez sur **taille gérée par le système** puis cliquez sur **définir**.
8. Cliquez sur **Apply**. Vous obtiendrez un avertissement que toobe redémarré pour hello modifications tootake affectent a besoin de cet ordinateur hello.
9. Redémarrez l’ordinateur virtuel de hello.

## <a name="next-steps"></a>Étapes suivantes
* Vous pouvez augmenter hello stockage disponible tooyour virtual machine par [y attacher un disque de données supplémentaires](attach-managed-disk-portal.md).

