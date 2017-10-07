---
title: configurations et des profils de service aaaHow toomanage | Documents Microsoft
description: "Découvrez comment toowork avec les fichiers de configuration de profils et les configurations de service | lequel stocker les paramètres pour les environnements de déploiement hello et paramètres de publication des services de cloud computing."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7da8c551-fb06-4057-b5c7-c77f4b39d803
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/11/2017
ms.author: kraigb
ms.openlocfilehash: 1dba9df2fa57fe94dacc90ae74b05ccdc28270c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-service-configurations-and-profiles"></a>Comment toomanage configurations du service et profils
## <a name="overview"></a>Vue d'ensemble
Lorsque vous publiez un service cloud, Visual Studio stocke les informations de configuration dans deux types de fichiers de configuration : les configurations de service et les profils. Configurations de service (fichiers .cscfg) stockent les paramètres pour les environnements de déploiement hello pour un service cloud Azure. Azure utilise ces fichiers de configuration pour gérer vos services cloud. Sur hello autre part, le magasin de profils (fichiers .azurePubxml) paramètres de publication des services de cloud computing. Ces paramètres sont un enregistrement de ce que vous sélectionnez lorsque vous utilisez hello Assistant Publication et sont utilisés localement par Visual Studio. Cette rubrique explique comment toowork avec les deux types de fichiers de configuration.

## <a name="service-configurations"></a>Configurations de service
Vous pouvez créer plusieurs toouse de configurations de service pour chacun de vos environnements de déploiement. Par exemple, vous pouvez créer une configuration de service pour l’environnement local de hello que vous utilisez toorun et testez une application Windows Azure et une autre configuration de service pour votre environnement de production.

Vous pouvez ajouter, supprimer, renommer et modifier ces configurations de service selon vos besoins. Vous pouvez gérer ces configurations de service à partir de Visual Studio, comme indiqué dans hello après l’illustration.

![Gérer les configurations de service](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-service-config.png)

Vous pouvez également ouvrir hello **gérer les Configurations** boîte de dialogue pages de propriétés du rôle hello. propriétés de hello tooopen pour un rôle dans votre projet Windows Azure, ouvrez le menu contextuel de hello pour ce rôle, puis choisissez **propriétés**. Sur hello **paramètres** onglet, développez hello **Configuration du Service** liste, puis sélectionnez **gérer** tooopen hello **gérer les Configurations de**boîte de dialogue.

### <a name="tooadd-a-service-configuration"></a>tooadd une configuration de service
1. Dans l’Explorateur de solutions, ouvrez le menu contextuel hello hello projet Windows Azure, puis sélectionnez **gérer les Configurations**.
   
    Hello **gérer les Configurations de Service** boîte de dialogue s’affiche.
2. tooadd une configuration de service, vous devez créer une copie d’une configuration existante. toodo, choisissez hello configuration que vous souhaitez toocopy à partir de la liste des noms hello, puis sélectionnez **créer une copie**.
3. Configuration du service hello toogive (facultatif) un autre nom, choisissez configuration hello de service à partir de la liste des noms hello, puis sélectionnez **renommer**. Bonjour **nom** zone de texte, entrez un nom hello que vous souhaitez toouse pour cette configuration de service, puis sélectionnez **OK**.
   
    Un nouveau fichier de configuration de service nommé ServiceConfiguration. [Nouveau nom] .cscfg est ajouté toohello projet Azure dans l’Explorateur de solutions.

### <a name="toodelete-a-service-configuration"></a>toodelete une configuration de service
1. Dans l’Explorateur de solutions, ouvrez le menu contextuel hello hello projet Windows Azure, puis sélectionnez **gérer les Configurations**.
   
    Hello **gérer les Configurations de Service** boîte de dialogue s’affiche.
2. toodelete une configuration de service, choisissez configuration de hello que vous souhaitez toodelete de hello **nom** liste, puis sélectionnez **supprimer**. Une boîte de dialogue s’affiche tooverify que vous souhaitez toodelete cette configuration.
3. Sélectionnez **Supprimer**.
   
     fichier de configuration de service Hello est supprimé de hello projet Azure dans l’Explorateur de solutions.

### <a name="toorename-a-service-configuration"></a>toorename une configuration de service
1. Dans l’Explorateur de solutions, ouvrez le menu contextuel hello hello projet Windows Azure, puis **gérer les Configurations**.
   
    Hello **gérer les Configurations de Service** boîte de dialogue s’affiche.
2. toorename une configuration de service, choisissez nouvelle configuration de service hello hello **nom** liste, puis sélectionnez **renommer**. Bonjour **nom** zone de texte, entrez un nom hello que vous souhaitez toouse pour cette configuration de service, puis sélectionnez **OK**.
   
    nom Hello hello service du fichier de configuration est modifié dans hello projet Azure dans l’Explorateur de solutions.

### <a name="toochange-a-service-configuration"></a>toochange une configuration de service
* Si vous souhaitez toochange une configuration de service, ouvrez le menu contextuel hello rôle spécifique de hello vous souhaitez toochange Bonjour projet Windows Azure, puis sélectionnez **propriétés**. Consultez [Comment : configurer des rôles de hello pour un Service de Cloud Azure avec Visual Studio](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) pour plus d’informations.

## <a name="make-different-setting-combinations-by-using-profiles"></a>Réaliser différentes combinaisons de paramètres à l'aide des profils
En utilisant un profil, vous pouvez renseigner automatiquement hello **Assistant Publication** avec différentes combinaisons de paramètres à des fins différentes. Par exemple, vous pouvez créer un profil pour le débogage et un autre pour les versions finales. Dans ce cas, votre **déboguer** profil aurait **IntelliTrace** activé et hello **déboguer** configuration sélectionnée et votre **version** profil aurait **IntelliTrace** désactivée et hello **version** configuration sélectionnée. Vous pouvez également utiliser les différents profils toodeploy un service à l’aide d’un autre compte de stockage.

Lorsque vous exécutez l’Assistant hello pour hello première fois, un profil par défaut est créé. Visual Studio stocke le profil de hello dans un fichier comportant l’extension .azurePubXml, qui est ajoutée tooyour projet Windows Azure sous hello **profils** dossier. Si vous spécifiez manuellement les différentes options lorsque vous exécutez les Assistant hello plus tard, fichier de hello met automatiquement à jour. Avant d’exécuter hello suivant la procédure, vous devez avez déjà publié votre service cloud au moins une fois.

### <a name="tooadd-a-profile"></a>tooadd un profil
1. Ouvrez le menu contextuel de hello pour votre projet Windows Azure, puis **publier**.
2. Toohello suivant **cibler profile** liste, sélectionnez hello **enregistrer le profil** bouton, comme hello suivant montre l’illustration. Cette action vous crée un profil.
   
    ![Créer un profil](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/create-new-profile.png)
3. Une fois le profil de hello est créé, sélectionnez **< gérer... >** Bonjour **cibler profile** liste.
   
    Hello **gérer les profils** boîte de dialogue s’affiche en tant que hello suivant montre l’illustration.
   
    ![Boîte de dialogue Gérer les profils](./media/vs-azure-tools-service-configurations-and-profiles-how-to-manage/manage-profiles.png)
4. Bonjour **nom** liste, choisissez un profil, puis sélectionnez **créer une copie de**.
5. Choisissez hello **fermer** bouton.
   
    Hello nouveau profil apparaît dans la liste du profil cible hello.
6. Bonjour **cibler profile** répertorier, profil hello select que vous venez de créer. paramètres de l’Assistant de publication Hello sont renseignés avec les options de hello du profil de hello que vous avez sélectionné.
7. Sélectionnez hello **précédent** et **suivant** boutons toodisplay chaque page de l’Assistant Publication de hello et ensuite personnaliser les paramètres de hello pour ce profil. Pour plus d’informations, consultez [Assistant Publication d’application Azure](http://go.microsoft.com/fwlink/p/?LinkID=623085) .
8. Après avoir terminé la personnalisation des paramètres de hello, sélectionnez **suivant** page des paramètres toogo toohello précédent. profil de Hello est enregistré lorsque vous publiez un service de hello à l’aide de ces paramètres ou si vous sélectionnez **enregistrer** suivant liste toohello des profils.

### <a name="toorename-or-delete-a-profile"></a>toorename ou supprimer un profil
1. Ouvrez le menu contextuel de hello pour votre projet Windows Azure, puis **publier**.
2. Bonjour **cibler profile** liste, sélectionnez **gérer**.
3. Bonjour **gérer les profils** boîte de dialogue, profil hello select que vous souhaitez toodelete, puis sélectionnez **supprimer**.
4. Dans hello boîte de dialogue de confirmation qui s’affiche, sélectionnez **OK**.
5. Sélectionnez **Fermer**.

### <a name="toochange-a-profile"></a>toochange un profil
1. Ouvrez le menu contextuel de hello pour votre projet Windows Azure, puis **publier**.
2. Bonjour **cibler profile** liste, sélectionnez hello profil que toochange.
3. Sélectionnez hello **précédent** et **suivant** boutons toodisplay hello de chaque page d’Assistant Publication, puis modifier les paramètres hello souhaité. Pour plus d’informations, consultez [Assistant Publication d’application Azure](http://go.microsoft.com/fwlink/p/?LinkID=623085) .
4. Après avoir terminé la modification des paramètres de hello, sélectionnez **suivant** toohello arrière de toogo **paramètres** page.
5. (Facultatif) sélectionnez **publier** service de cloud de hello toopublish à l’aide de nouveaux paramètres de hello. Si vous ne souhaitez pas toopublish votre service cloud à ce stade et que vous fermez hello Assistant Publication, Visual Studio vous demande si vous souhaitez toosave hello modifications toohello profil.

## <a name="next-steps"></a>Étapes suivantes
toolearn sur la configuration des autres parties de votre projet Windows Azure depuis Visual Studio, consultez [configuration d’un projet Azure](http://go.microsoft.com/fwlink/p/?LinkID=623075)

