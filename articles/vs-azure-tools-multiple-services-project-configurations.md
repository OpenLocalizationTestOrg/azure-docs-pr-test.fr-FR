---
title: "aaaConfiguring votre projet Windows Azure à l’aide de plusieurs configurations de service | Documents Microsoft"
description: "Découvrez le projet de service de cloud tooconfigure Azure en modifiant les fichiers ServiceDefinition.csdef et ServiceConfiguration.cscfg hello."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a4fb79ed-384f-4183-9f74-5cac257206b9
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 14222266093eb876db0ac9ce8d3d17a04c65d1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-your-azure-project-using-multiple-service-configurations"></a>Configuration de votre projet Azure à l'aide de plusieurs configurations de service
Un projet de service cloud Azure comprend deux fichiers de configuration : ServiceDefinition.csdef et ServiceConfiguration.cscfg. Ces fichiers sont empaquetés avec votre application de service cloud Azure et déploiement tooAzure.

* Hello **ServiceDefinition.csdef** fichier contient des métadonnées hello requis par hello environnement Azure pour les besoins de hello de votre application de service cloud, y compris les rôles qu’il contient. Ce fichier contient également les paramètres de configuration qui s’appliquent à des instances de tooall. Ces paramètres de configuration peuvent être lus lors de l’exécution à l’aide de hello API Runtime d’hébergement du Service Azure. Ce fichier ne peut pas être mis à jour lorsque votre service est en cours d’exécution dans Azure.
* Hello **ServiceConfiguration.cscfg** fichier définit les valeurs pour les paramètres de configuration hello définis dans le fichier de définition de service hello et spécifie le nombre hello de toorun d’instances pour chaque rôle. Ce fichier peut être mis à jour lorsque votre service cloud est en cours d’exécution dans Azure.

Hello Azure Tools pour Microsoft Visual Studio fournit des pages de propriétés que vous pouvez utiliser les paramètres de configuration tooset stockés dans ces fichiers. tooaccess hello des pages de propriétés, double-cliquez sur la référence de rôle hello sous le projet de service cloud Azure hello dans l’Explorateur de solutions, ou référence de rôle hello, sélectionnez **propriétés**, comme illustré dans la figure suivante de hello.

![VS_Solution_Explorer_Roles_Properties](./media/vs-azure-tools-multiple-services-project-configurations/IC784076.png)

Pour plus d’informations sur hello sous-jacente des schémas pour les fichiers de configuration de service et de définition de service hello, consultez hello [référence du schéma](https://msdn.microsoft.com/library/azure/dd179398.aspx). Pour plus d’informations sur la configuration du service, consultez [comment les Services de cloud computing tooConfigure](cloud-services/cloud-services-how-to-configure.md).

## <a name="configuring-role-properties"></a>Configuration des propriétés de rôle
pages de propriétés Hello pour un rôle web et un rôle de travail sont similaires, bien qu’il existe quelques différences près, décrites dans les sections suivantes de hello.

À partir de hello **mise en cache** page, vous pouvez configurer hello mise en cache des services Azure.

### <a name="configuration-page"></a>Page de configuration
Sur hello **Configuration** page, vous pouvez définir ces propriétés :

**Instances**

Ensemble hello **Instance** dénombrer les toohello de propriété d’instances de service de hello doit s’exécuter pour ce rôle.

Ensemble hello **taille de machine virtuelle** propriété trop**très petite**, **petit**, **support**, **grande**, ou **Très nombreuses**.  Pour en savoir plus, consultez la rubrique [Tailles de services cloud](cloud-services/cloud-services-sizes-specs.md).

**Action de démarrage** (rôle web uniquement)

Définissez cette toospecify de propriété Visual Studio doit lancer un navigateur web pour les points de terminaison hello HTTP ou points de terminaison HTTPS hello lorsque vous démarrez le débogage.

Hello, option du point de terminaison HTTPS est disponible uniquement si vous avez déjà défini un point de terminaison HTTPS pour votre rôle. Vous pouvez définir un point de terminaison HTTPS sur hello **points de terminaison** page de propriétés.

Si vous avez déjà ajouté un point de terminaison HTTPS, hello option de point de terminaison HTTPS est activée par défaut, et Visual Studio lance un navigateur pour ce point de terminaison lorsque vous démarrez le débogage, en outre navigateur tooa pour votre point de terminaison HTTP. Cela suppose que les deux options de démarrage soient activées.

**Diagnostics**

Par défaut, les diagnostics est activée pour le rôle Web de hello. Hello projet de service cloud Azure et compte de stockage sont définies à l’émulateur de stockage local toouse hello. Lorsque vous êtes prêt toodeploy tooAzure, vous pouvez sélectionner le bouton Générateur de hello (**...** ) tooupdate hello stockage compte toouse le stockage Azure dans le cloud de hello. Vous pouvez transférer le compte de stockage toohello hello diagnostics données à la demande ou à intervalles planifiés automatiquement. Pour plus d'informations sur les diagnostics Azure, consultez la page [Activation de Diagnostics dans Azure Cloud Services et Azure Virtual Machines](cloud-services/cloud-services-dotnet-diagnostics.md).

## <a name="settings-page"></a>Page Paramètres
Sur hello **paramètres** page, vous pouvez ajouter des paramètres de configuration pour votre service. Les paramètres de configuration sont des paires nom-valeur. Code qui s’exécute dans le rôle de hello peut lire des valeurs de hello des paramètres de configuration lors de l’exécution à l’aide des classes fournies par hello [bibliothèque managée Azure](http://go.microsoft.com/fwlink?LinkID=171026). Plus précisément, hello [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx) méthode retourne la valeur hello d’un paramètre de configuration nommé pendant l’exécution.

### <a name="configuring-a-connection-string-tooa-storage-account"></a>Configuration d’un compte de stockage tooa connexion chaîne
Une chaîne de connexion est un paramètre de configuration qui fournit des informations de connexion et d’authentification pour l’émulateur de stockage hello ou un compte de stockage Azure. Chaque fois que votre code doit accéder aux données de services de stockage Azure – autrement dit, blob, file d’attente ou de données de table : à partir du code en cours d’exécution dans un rôle, vous devez toodefine une chaîne de connexion pour ce compte de stockage.

Une chaîne de connexion qui pointe de compte de stockage Azure tooan doit utiliser un format défini. Pour plus d’informations sur la façon toocreate les chaînes de connexion, consultez [configurer des chaînes de connexion de stockage Azure](storage/common/storage-configure-connection-string.md).

Lorsque vous êtes prêt tootest votre service sur les services de stockage Azure hello ou lorsque vous êtes prêt toodeploy votre tooAzure de service cloud, vous pouvez modifier valeur hello de n’importe quel tooyour de toopoint de chaînes de connexion compte de stockage Azure. Sélectionnez (**…**) et **Entrer les informations d’identification du compte de stockage**. Entrez vos informations de compte, notamment le nom et la clé de votre compte. Bonjour **chaîne de connexion de compte de stockage** boîte de dialogue, vous pouvez également indiquer si vous souhaitez que les points de terminaison toouse hello par défaut HTTPS (option par défaut de hello), les points de terminaison HTTP hello par défaut ou les points de terminaison personnalisés. Vous pouvez décider toouse les points de terminaison personnalisés si vous avez enregistré un nom de domaine personnalisé pour votre service, comme décrit dans [configurer un nom de domaine personnalisé pour les données blob dans un compte de stockage Azure](storage/blobs/storage-custom-domain-name.md).

> [!IMPORTANT]
> Vous devez modifier votre tooan de toopoint de chaînes de connexion compte de stockage Azure avant de déployer votre service. Échec toodo, cela peut entraîner votre rôle pas toostart ou toocycle via hello États initialisation, occupés et arrêt.
> 
> 

## <a name="endpoints-page"></a>Page des points de terminaison
Un rôle de travail peut avoir un nombre quelconque de points de terminaison HTTP, HTTPS ou TCP. Points de terminaison peuvent être des points de terminaison d’entrée, qui sont des clients de tooexternal disponibles, ou les points de terminaison internes, qui sont des rôles disponibles tooother qui sont exécutent dans le service hello.

* les clients tooexternal disponible de point de terminaison toomake HTTP et les navigateurs Web Modifier tooinput de type de point de terminaison hello et spécifiez un nom et un numéro de port public.
* toomake HTTPS clients disponibles tooexternal de point de terminaison et les navigateurs Web, type de point de terminaison hello également modifier**d’entrée**et spécifiez un nom, un numéro de port public et un nom de certificat de gestion.
  
    Notez que, avant de pouvoir spécifier un certificat de gestion, vous devez définir les certificats hello sur hello **certificats** page de propriétés.
* toomake un point de terminaison disponible pour l’accès interne par les autres rôles dans le service cloud hello, modifiez toointernal de type de point de terminaison hello et spécifiez un nom et des ports privés possibles pour ce point de terminaison.

## <a name="local-storage-page"></a>Page de stockage local
Vous pouvez utiliser hello **stockage Local** tooreserve de page de propriété une ou plusieurs ressources de stockage local pour un rôle. Une ressource de stockage local est un répertoire réservé dans le système de fichiers hello Hello machine virtuelle Azure dans lequel s’exécute une instance d’un rôle.

## <a name="certificates-page"></a>Page Certificats
Sur hello **certificats** page, vous pouvez associer des certificats à votre rôle. certificats Hello que vous ajoutez peuvent être utilisé tooconfigure vos points de terminaison HTTPS sur hello **points de terminaison** page de propriétés.

Hello **certificats** page de propriétés ajoute des informations sur la configuration de votre service de certificats tooyour. Notez que vos certificats ne sont pas fournis avec votre service ; Vous devez télécharger séparément vos certificats tooAzure via hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885).

tooassociate un certificat à votre rôle, fournissez un nom pour le certificat de hello. Vous utilisez ce nom toorefer toohello certificat lorsque vous configurez un point de terminaison HTTPS sur hello **points de terminaison** page de propriétés. Ensuite, spécifiez si le magasin de certificats hello est **ordinateur Local** ou **utilisateur actuel** et le nom de hello du magasin de hello. Enfin, entrez l’empreinte numérique du certificat hello. Si les certificats hello sont Bonjour personnel actuel (My), vous pouvez entrer l’empreinte numérique du certificat hello en sélectionnant le certificat de hello depuis une liste. S’il se trouve dans un autre emplacement, entrez manuellement les valeur d’empreinte numérique hello.

Lorsque vous ajoutez un certificat à partir du magasin de certificats hello, tous les certificats intermédiaires sont automatiquement ajoutés toohello des paramètres de configuration pour vous. Ces certificats intermédiaires doivent également être téléchargés tooAzure dans l’ordre toocorrectly configurer votre service pour SSL.

Les certificats de gestion que vous associez à votre service s’appliquent tooyour service uniquement quand il est en cours d’exécution dans le cloud de hello. Lorsque votre service est en cours d’exécution dans l’environnement de développement local hello, il utilise un certificat standard géré par l’émulateur de calcul hello.

## <a name="configuring-hello-azure-cloud-service-project"></a>Configuration de projet de service cloud Azure hello
tooconfigure les paramètres qui s’appliquent de projet de service cloud Azure entière tooan, vous ouvrez d’abord hello raccourci menu pour ce nœud de projet, puis vous choisissez Propriétés tooopen ses pages de propriétés. Hello tableau suivant montre les pages de propriétés.

| Page Propriété | Description |
| --- | --- |
| Application |À partir de cette page, vous pouvez afficher plus d’informations sur la version de hello d’Azure Tools utilisée par ce projet de service cloud, et vous pouvez mettre à niveau toohello la version actuelle des outils de hello. |
| Événements de build |Sur cette page, vous pouvez définir des événements pré-build et post-build. |
| Développement |À partir de cette page, vous pouvez spécifier des instructions de configuration de build et de conditions hello dans lesquelles les événements post-build sont exécutés. |
| Web |À partir de cette page, vous pouvez configurer les paramètres qui concernent le serveur web de toohello. |

