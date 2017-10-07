---
title: aaaUse hello rendu de traitement par lots Azure service toorender dans le cloud de hello | Documents Microsoft
description: "Créez des travaux de rendu sur des machines virtuelles Azure directement à partir de Maya et sur une base de paiement à l’utilisation."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: tamram
ms.openlocfilehash: 3fb78d883311bbc3ab62743b7d1b111ffad177cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-rendering-service"></a>Prise en main hello service de traitement par lots de rendu

Hello service de rendu de traitement par lots Azure offre des fonctionnalités de rendu de l’échelle du cloud sur une base de paiement à l’utilisation. Hello rendu de traitement par lots de service gère la planification des tâches et file d’attente, la gestion des échecs de tentatives et des auto-mise à l’échelle pour votre opération de rendu. Hello service de traitement par lots de rendu prend en charge Autodesk Maya, 3ds Max et Arnold, avec prise en charge pour les autres applications sera bientôt disponible. Hello lot plug-in pour Maya 2017 rend facile toostart un travail de rendu sur Azure directement à partir de votre bureau. 

## <a name="supported-applications"></a>Applications prises en charge

Hello service de traitement par lots de rendu prend actuellement en charge hello suivant des applications :

- Autodesk Maya
- Autodesk 3ds Max
- Autodesk Arnold

## <a name="prerequisites"></a>Composants requis

service de traitement par lots de rendu toouse hello, vous devez :

- Un [compte Azure](https://azure.microsoft.com/free/). 
- **Un compte Azure Batch.** Pour obtenir des conseils sur la création d’un compte Batch Bonjour portail Azure, consultez [créer un compte de traitement par lots avec hello Azure portal](batch-account-create-portal.md).
- **Un compte de stockage Azure.** ressources Hello utilisées pour votre opération de rendu sont stockées dans le stockage Azure. Vous pouvez créer un compte de stockage automatiquement lorsque vous configurez votre compte Batch. Vous pouvez également utiliser un compte de stockage existant. toolearn en savoir plus sur les comptes de stockage, consultez [comment toocreate, gérer ou supprimer un compte de stockage Bonjour Azure portal](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

toouse hello lot plug-in pour Maya, vous devez :

- **Maya 2017**
- **Arnold for Maya**

Vous pouvez également utiliser hello [portail Azure](https://portal.azure.com) toocreate les pools d’ordinateurs virtuels qui sont préconfigurés avec Maya, 3ds Arnold et Max. Vous pouvez utiliser les travaux de portail toomonitor hello et diagnostiquer les tâches qui ont échoué en téléchargeant les journaux des applications et par la connexion à distance des machines virtuelles de tooindividual à l’aide du protocole RDP ou SSH.

## <a name="basic-batch-concepts"></a>Concepts Batch de base

Avant de commencer à l’aide du service de traitement par lots de rendu hello, il est utile toobe familiarisé avec quelques concepts de traitement par lots, y compris les nœuds de calcul, les pools et les travaux. toolearn plus sur Azure Batch en général, consultez [exécuter des charges de travail intrinsèquement parallèles avec lot](batch-technical-overview.md).

### <a name="pools"></a>Pools

Batch est un service de plateforme permettant d’exécuter des tâches nécessitant beaucoup de ressources système, comme un rendu, sur un **pool** de **nœuds de calcul**. Chacun des nœuds de calcul dans un pool est une machine virtuelle Azure exécutant Windows ou Linux. 

Pour plus d’informations sur les pools de lot et de nœuds de calcul, consultez hello [Pool](batch-api-basics.md#pool) et [de nœud de calcul](batch-api-basics.md#compute-node) sections [parallèles à grande échelle de développer des solutions avec le traitement par lots de calcul](batch-api-basics.md).

### <a name="jobs"></a>Tâches

Un lot **travail** est une collection de tâches qui s’exécutent sur hello nœuds de calcul dans un pool. Lorsque vous soumettez un travail de rendu, lot divise le travail de hello en tâches et distribue des nœuds de calcul hello tâches toohello dans hello pool toorun.

Pour plus d’informations sur les tâches de traitement par lots, consultez hello [travail](batch-api-basics.md#job) section [parallèles à grande échelle de développer des solutions avec le traitement par lots de calcul](batch-api-basics.md).

## <a name="use-hello-batch-plug-in-for-maya-toosubmit-a-render-job"></a>Utilisez hello lot plug-in pour Maya toosubmit un travail de rendu

Avec hello plug-in pour Maya du lot, vous pouvez envoyer un toohello de travail service directement à partir de Maya de lot de rendu. Hello les sections suivantes décrire comment les tooconfigure hello de travail à partir du plug-in de hello et envoyez-le. 

### <a name="load-hello-batch-plug-in-in-maya"></a>Charger hello lot plug-in Maya

Hello lot plug-in est disponible sur [GitHub](https://github.com/Azure/azure-batch-maya/releases). Décompressez le répertoire de tooa hello archive de votre choix. Vous pouvez charger le plug-in de hello directement à partir de hello *azure_batch_maya* active.

hello de tooload plug-in Maya :

1. Exécutez Maya.
2. Ouvrez **Fenêtre** > **Paramètres/Préférences** > **Plug-in Manager** (Gestionnaire de plug-in).
3. Cliquez sur **Parcourir**.
4. Accédez tooand sélectionnez *azure_batch_maya/plug-in/AzureBatch.py*.

### <a name="authenticate-access-tooyour-batch-and-storage-accounts"></a>Authentifier des comptes de stockage et de traitement par lots de tooyour accès

hello de toouse plug-in, vous devez tooauthenticate à l’aide de votre lot d’Azure et les clés de compte de stockage Azure. tooretrieve vos clés de compte :

1. Bonjour complet plug-in Maya et sélectionnez hello **Config** onglet.
2. Accédez toohello [portail Azure](https://portal.azure.com).
3. Sélectionnez **comptes Batch** hello menu de gauche. Si nécessaire, cliquez sur **Plus Services** et filtrez sur _Batch_.
4. Recherchez le compte de traitement par lots de hello souhaité dans la liste de hello.
5. Sélectionnez hello **clés** toodisplay d’élément de menu votre nom de compte, l’URL de compte et les clés d’accès :
    - Collez l’URL du compte Batch hello hello **Service** champ hello lot plug-in.
    - Nom du compte coller hello en hello **compte Batch** champ.
    - Clé de compte principal coller hello en hello **clé Batch** champ.
7. Sélectionnez les comptes de stockage hello menu de gauche. Si nécessaire, cliquez sur **Plus Services** et filtrez sur _Stockage_.
8. Localiser le compte de stockage hello souhaité dans la liste de hello.
9. Sélectionnez hello **clés d’accès** nom de compte de stockage menu élément toodisplay hello et des clés.
    - Nom de compte de stockage coller hello en hello **compte de stockage** champ hello lot plug-in.
    - Clé de compte principal coller hello en hello **clé de stockage** champ.
10. Cliquez sur **authentifier** tooensure hello plug-in peut accéder à ces deux comptes.

Une fois que vous avez correctement authentifié, les jeux de plug-in hello hello trop de champ d’état**authentifié**: 

![Authentifier vos comptes de stockage et Batch](./media/batch-rendering-service/authentication.png)

### <a name="configure-a-pool-for-a-render-job"></a>Configurer un pool pour un travail de rendu

Une fois que vous avez authentifié vos comptes de stockage et Batch, définissez un pool pour votre travail de rendu. plug-in de Hello enregistre vos sélections entre les sessions. Une fois que vous avez configuré votre configuration préférée, vous n’aurez pas toomodify il sauf si elle change.

Hello sections suivantes vous guident hello disponible options disponibles sur hello **Submit** onglet :

#### <a name="specify-a-new-or-existing-pool"></a>Spécifier un pool nouveau ou existant

toospecify un pool sur laquelle travail rendu hello toorun, sélectionnez hello **Submit** onglet. Cet onglet propose des options permettant de créer un pool ou d’un sélectionner un existant :

- Vous pouvez **automatiquement configurer un pool pour ce travail** (option par défaut de hello). Lorsque vous choisissez cette option, traitement par lots crée le pool hello exclusivement pour le travail en cours hello, et automatiquement suppressions hello lorsque hello rendre la tâche est terminée. Cette option est préférable lorsque vous avez un toocomplete de travail rendu unique.
- Vous pouvez **réutiliser un pool persistant existant**. Si vous disposez d’un pool existant qui est inactif, vous pouvez spécifier ce pool de travail de rendu hello en cours d’exécution en la sélectionnant dans la liste déroulante de hello. Réutilisation d’un pool persistant existant enregistre hello durée tooprovision hello pool.  
- Vous pouvez **créer un pool persistant**. Cette option crée un pool pour l’exécution du travail de hello. Elle ne supprime pas le pool de hello fois hello terminée, afin que vous puissiez le réutiliser pour les futurs travaux. Sélectionnez cette option lorsque vous avez un toorun besoin continu restituer des travaux. Sur les tâches suivantes, vous pouvez sélectionner **réutiliser un pool persistant** toouse hello pool permanent que vous avez créé pour la tâche hello.

![Spécifier le pool, l’image de système d’exploitation, la taille de machine virtuelle et la licence](./media/batch-rendering-service/submit.png)

Pour plus d’informations sur l’augmentation des coûts pour les machines virtuelles Azure, consultez hello [Forum aux questions sur la tarification Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/#faq) et [Forum aux questions sur la tarification Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/#faq).

#### <a name="specify-hello-os-image-tooprovision"></a>Spécifiez tooprovision d’image hello du système d’exploitation

Vous pouvez spécifier le type hello du système d’exploitation image toouse tooprovision de nœuds de calcul dans le pool de hello sur hello **Env** onglet (environnement). Traitement par lots prend actuellement en charge hello possibilités d’image pour le rendu des tâches suivantes :

|Système d’exploitation  |Image  |
|---------|---------|
|Linux     |Préversion CentOS Batch |
|Windows     |Préversion Windows Batch |

#### <a name="choose-a-vm-size"></a>Choisir une taille de machine virtuelle

Vous pouvez spécifier la taille de machine virtuelle hello sur hello **Env** onglet. Pour plus d’informations sur les tailles de machine virtuelle disponibles, consultez [Tailles des machines virtuelles Linux dans Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) et [Tailles des machines virtuelles Windows dans Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes). 

![Spécifiez l’image de machine virtuelle du système d’exploitation hello et la taille sur l’onglet de Env hello](./media/batch-rendering-service/environment.png)

#### <a name="specify-licensing-options"></a>Spécifier les options de licence

Vous pouvez spécifier des licences hello vous souhaitez toouse sur hello **Env** onglet. Options disponibles :

- **Maya**, qui est activée par défaut.
- **Arnold**, qui est activé si Arnold est détecté en tant que moteur de rendu active hello dans Maya.

 Si vous le souhaitez toorender à l’aide de votre propre licence, vous pouvez configurer votre point de terminaison de licence en ajoutant hello approprié variables toohello table d’environnement. Dans ce cas, être toodeselect qu’options de licence hello par défaut.

> [!IMPORTANT]
> Vous êtes facturé pour une utilisation de licences de hello pendant l’exécutant de machines virtuelles dans le pool de hello, même si hello machines virtuelles ne sont pas actuellement utilisés pour le rendu. tooavoid des frais supplémentaires, accédez à toohello **Pools** onglet et redimensionner des nœuds de too0 hello pool jusqu'à ce que vous êtes prêt toorun une autre tâche de rendu. 
>
>

#### <a name="manage-persistent-pools"></a>Gérer des pools persistants

Vous pouvez gérer un pool existant persistant sur hello **Pools** onglet. Sélection d’un pool à partir de la liste de hello indique l’état actuel de hello du pool de hello.

À partir de hello **Pools** onglet, vous pouvez également supprimer le pool de hello et redimensionner le nombre de hello d’ordinateurs virtuels dans le pool de hello. Vous pouvez redimensionner un tooavoid de nœuds too0 pool encourir de frais entre les charges de travail.

![Afficher, redimensionner et supprimer des pools](./media/batch-rendering-service/pools.png)

### <a name="configure-a-render-job-for-submission"></a>Configurer un travail de rendu pour l’envoi

Une fois que vous avez spécifié les paramètres hello pour le pool hello qui exécutera les travaux de rendu hello, configurer la tâche hello lui-même. 

#### <a name="specify-scene-parameters"></a>Spécifier les paramètres de scène

Hello lot plug-in détecte le moteur de rendu que vous utilisez actuellement dans Maya et hello affiche approprié des paramètres sur hello de rendu **Submit** onglet. Ces paramètres incluent l’image de démarrage hello, image, préfixe de sortie et image. Vous pouvez remplacer les paramètres de rendu du fichier hello scène en spécifiant des paramètres différents dans hello plug-in. Modifications que vous apportez toohello paramètres de plug-in ne sont pas persistantes toohello arrière scène paramètres de rendu du fichier, donc vous pouvez apporter des modifications sur une base de tâche par tâche sans avoir besoin de fichier de scène tooreupload hello.

Hello plug-in vous avertit si le moteur que vous avez sélectionné dans Maya de rendu de hello n’est pas pris en charge.

Si vous chargez une nouvelle séquence lorsque hello plug-in est ouvert, cliquez sur hello **Actualiser** bouton toomake vraiment hello sont mis à jour.

#### <a name="resolve-asset-paths"></a>Résoudre les chemins d’accès de ressources

Lorsque vous chargez le plug-in de hello, il analyse le fichier de scène hello pour les références de fichier externe. Ces références sont affichées dans hello **actifs** onglet. Si un chemin d’accès référencé ne peut pas être résolu, hello plug-in de tentative de fichier de hello toolocate dans quelques emplacements par défaut, y compris :

- emplacement de Hello du fichier de scène hello 
- du projet actif Hello _sourceimages_ Active
- répertoire de travail actuel Hello. 

Si les actifs de hello toujours est introuvable, elle est répertoriée avec une icône d’avertissement :

![Les ressources manquantes sont affichées avec une icône d’avertissement](./media/batch-rendering-service/missing_assets.png)

Si vous connaissez emplacement hello d’une référence de fichier non résolues, vous pouvez cliquer sur hello avertissement icône toobe vous y êtes invité tooadd un chemin de recherche. Hello puis plug-in utilise cette tooresolve de tooattempt de chemin d’accès de recherche de toutes les ressources manquantes. Vous pouvez ajouter n’importe quel nombre de chemins de recherche.

Lorsqu’une référence est résolue, elle est répertoriée avec une icône verte :

![Les ressources résolues sont affichées avec une icône verte](./media/batch-rendering-service/found_assets.png)

Si votre scène requiert d’autres fichiers que hello plug-in n’a pas détecté, vous pouvez ajouter des fichiers ou répertoires. Hello d’utilisation **ajouter des fichiers** et **ajouter un répertoire** boutons. Si vous chargez une nouvelle séquence lorsque hello plug-in est ouvert, être vraiment tooclick **Actualiser** références de la scène tooupdate hello.

#### <a name="upload-assets-tooan-asset-project"></a>Télécharger le projet d’actifs tooan actifs

Lorsque vous envoyez un travail de rendu, hello référencé fichiers affichés dans hello **actifs** onglet sont automatiquement téléchargé tooAzure stockage sous forme de projet actif. Vous pouvez également télécharger des fichiers d’éléments multimédias hello indépendamment d’un travail de rendu, à l’aide de hello **télécharger** bouton sur hello **actifs** nom du projet actif onglet hello est spécifié dans hello **projet**champ et est nommé d’après le projet de Maya hello actif par défaut. Lorsque des fichiers sont téléchargés, structure de fichier local hello est conservé. 

Une fois téléchargées, les ressources peuvent être référencées par n’importe quel nombre de travaux de rendu. Tous les composants téléchargés sont travail tooany disponibles qui référence le projet d’actifs hello, ils sont inclus dans la scène de hello ou non. projet d’actifs hello toochange référencé par votre tâche suivante, modifier le nom hello Bonjour **projet** champ hello **actifs** onglet. S’il existe des fichiers référencés que vous souhaitez tooexclude de télécharger, les désélectionner à l’aide du bouton hello verte en regard de la liste de hello.

#### <a name="submit-and-monitor-hello-render-job"></a>Soumettre et hello du moniteur restituer de travail

Une fois que vous avez configuré la tâche de rendu hello Bonjour plug-in, cliquez sur hello **soumettre un travail** bouton sur hello **Submit** onglet toosubmit hello travail tooBatch :

![Envoi de la tâche de rendu hello](./media/batch-rendering-service/submit_job.png)

Vous pouvez surveiller une tâche qui est en cours d’exécution à partir de hello **travaux** onglet hello plug-in. Sélectionnez une tâche de hello liste toodisplay hello état actuel du travail de hello. Vous pouvez également utiliser cette toocancel onglet et supprimer des travaux, ainsi que les journaux de rendu et toodownload hello sorties. 

modifier les sorties de toodownload, hello **génère** répertoire de destination souhaité de champ tooset hello. Cliquez sur hello ENGRENAGE icône toostart un processus en arrière-plan qui surveille le travail de hello et télécharger des sorties qu’il progresse : 

![Afficher l’état du travail et télécharger des sorties](./media/batch-rendering-service/jobs.png)

Vous pouvez fermer Maya sans interrompre le processus de téléchargement hello.

## <a name="next-steps"></a>Étapes suivantes

toolearn en savoir plus sur le traitement par lots, consultez [exécuter des charges de travail intrinsèquement parallèles avec lot](batch-technical-overview.md).
