---
title: aaaCreate et restaurer une sauvegarde dans BizTalk Services | Documents Microsoft
description: "BizTalk Services offre des fonctionnalités de sauvegarde et de restauration. Découvrez comment toocreate déterminer ce que sauvegarder et restaurer une sauvegarde. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a>Sauvegarde et restauration de BizTalk Services

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk Services offre des fonctionnalités de sauvegarde et de restauration. Cette rubrique décrit comment toobackup et restauration des Services BizTalk à l’aide de hello portail Azure classic.

Vous pouvez également sauvegarder les Services BizTalk à l’aide de hello [API REST des Services BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584). 

> [!NOTE]
> Connexions hybrides ne sont pas sauvegardées, quel que soit l’édition de hello. Vous devez recréer vos connexions hybrides.


## <a name="before-you-begin"></a>Avant de commencer
* Il se peut que les fonctionnalités de sauvegarde et de restauration ne soient pas disponibles dans toutes les éditions. Consultez [BizTalk Services : tableau comparatif des éditions](biztalk-editions-feature-chart.md).
* À l’aide de hello portail Azure classic, vous pouvez créer une sauvegarde à la demande ou créer une sauvegarde planifiée. 
* Contenu de sauvegarde peut être restaurée toohello même BizTalk Service ou tooa nouveau BizTalk Service. toorestore hello BizTalk Service à l’aide de hello même nom, hello existant du BizTalk Service doit être supprimé et hello nom doit être disponible. Après avoir supprimé un BizTalk Service, il peut prendre plus de temps que vous souhaitiez pour hello même toobe nom disponible. Si vous ne pouvez pas attendre hello même nom toobe disponible, puis restaurer tooa nouveau BizTalk Service.
* Les Services BizTalk peut être restaurée toohello même édition ou une édition supérieure. Restauration des Services BizTalk tooa version inférieure, à partir de lorsque hello sauvegarde, n’est pas pris en charge.
  
    Par exemple, une sauvegarde à l’aide de hello que édition Basic peut être restaurée toohello édition Premium. Une sauvegarde à l’aide de hello que Premium Edition ne peut pas être restaurée toohello Standard Edition.
* numéros de contrôle EDI Hello sont sauvegardées de continuité des activités toomaintain hello des numéros de contrôle. Si les messages sont traités après la dernière sauvegarde de hello, la restauration ce contenu de la sauvegarde peut entraîner des numéros de contrôle en double.
* Si un lot de messages actifs, traite le lot de hello **avant** une sauvegarde en cours d’exécution. Lors de la création d'une sauvegarde (à la demande ou planifiée), les messages contenus dans des lots ne sont jamais stockés. 
  
    **En cas de sauvegarde présentant des messages actifs dans un lot, ceux-ci ne sont pas sauvegardés et sont donc perdus.**
* Facultatif : Hello portail BizTalk Services, d’arrêter toutes les opérations de gestion.

## <a name="create-a-backup"></a>Création d'une sauvegarde
Une sauvegarde peut être effectuée à tout moment et vous la contrôlez complètement. Cette section répertorie les sauvegardes de toocreate hello étapes à l’aide de hello Azure classic portail, y compris :

[Sauvegarde à la demande](#backupnow)

[Planification d'une sauvegarde](#backupschedule)

#### <a name="backupnow"></a>Sauvegarde à la demande
1. Bonjour portail Azure classic, sélectionnez **BizTalk Services**, et puis sélectionnez hello BizTalk Service souhaité toobackup.
2. Bonjour **tableau de bord** onglet, sélectionnez **sauvegarder** bas hello de page de hello.
3. Entrez un nom de sauvegarde. Par exemple, entrez *monServiceBizTalk*BU*Date*.
4. Choisissez un compte de stockage d’objets blob et de la sauvegarde de hello sélectionnez coche toostart hello.

Une fois la sauvegarde de hello terminée, un conteneur avec le nom de la sauvegarde hello que vous entrez est créé dans le compte de stockage hello. Ce conteneur comprend la configuration de sauvegarde de votre service BizTalk.

#### <a name="backupschedule"></a>Planification d'une sauvegarde
1. Bonjour portail Azure classic, sélectionnez **BizTalk Services**, sélectionnez hello BizTalk Service nom tooschedule hello sauvegarde, puis sélectionnez hello **configurer** onglet.
2. Ensemble hello **état de la sauvegarde** trop**automatique**. 
3. Sélectionnez hello **compte de stockage** toostore hello sauvegarde, entrez hello **fréquence** toocreate hello sauvegardes et la durée pendant laquelle tookeep hello (**jours de rétention**) :
   
    ![][AutomaticBU]
   
    **Remarques**     
   
   * Dans **jours de rétention**, période de rétention hello doit être supérieure à la fréquence de sauvegarde hello.
   * Sélectionnez **conserver toujours au moins une sauvegarde**, même si elle est au-delà de la période de rétention hello.
4. Sélectionnez **Enregistrer**.

Lorsqu’une tâche de sauvegarde planifiée s’exécute, il crée un conteneur (données de sauvegarde toostore) dans le compte de stockage hello que vous avez entré. nom Hello du conteneur de hello est nommé *BizTalk Service nom-date-heure*. 

Si hello tableau de bord de BizTalk Service affiche un **n’a pas pu** état :

![Statut de la dernière sauvegarde planifiée][BackupStatus] 

Hello ouvre hello gestion des Services de journaux des opérations toohelp résoudre les problèmes. Consultez [BizTalk Services : résolution des problèmes à l'aide des journaux des opérations](http://go.microsoft.com/fwlink/p/?LinkId=391211).

## <a name="restore"></a>Restauration
Vous pouvez restaurer les sauvegardes à partir de hello portail Azure classic ou de hello [restaurer API REST du Service BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325582). Cette section répertorie les toorestore d’étapes hello à l’aide du portail classique de hello.

#### <a name="before-restoring-a-backup"></a>Avant de restaurer une sauvegarde
* De nouveaux magasins de suivi, d'archivage et de surveillance peuvent être spécifiés lors de la restauration d'un service BizTalk.
* Hello les mêmes données de Runtime de EDI sont restaurées. sauvegarde de EDI Runtime Hello stocke des numéros de contrôle hello. numéros de contrôle Hello restauré sont séquentiels hello à partir de la sauvegarde de hello. Si les messages sont traités après la dernière sauvegarde de hello, la restauration ce contenu de la sauvegarde peut entraîner des numéros de contrôle en double.

#### <a name="restore-a-backup"></a>Restauration d'une sauvegarde
1. Bonjour portail Azure classic, sélectionnez **nouveau** > **des Services d’application** > **BizTalk Service** > **restaurer** :
   
    ![Restauration d'une sauvegarde][Restore]
2. Dans **sauvegarde URL**, sélectionnez l’icône de dossier hello et développez le compte de stockage Azure hello que magasins hello sauvegarde de configuration de BizTalk Service. Développez le conteneur de hello et dans le volet droit de hello, sélectionnez hello correspondant sauvegarder le fichier .txt. 
   <br/><br/>
   Sélectionnez **Ouvrir**.
3. Sur hello **restaurer le BizTalk Service** , entrez un **nom du Service BizTalk** et vérifiez hello **URL de domaine**, **édition**et **Région** pour hello restauré BizTalk Service. **Créer une nouvelle instance de la base de données SQL** pour hello de base de données de suivi :
   
    ![][RestoreBizTalkService]
   
    Sélectionnez la flèche suivant de hello.
4. Vérifiez le nom hello de base de données SQL hello, entrez hello de serveur physique où la base de données SQL hello doit être créé et un nom d’utilisateur/mot de passe pour ce serveur.

    Si vous souhaitez l’édition de base de données SQL tooconfigure hello, de taille et d’autres propriétés, sélectionnez **configurer des paramètres avancés de base de données**. 

    Sélectionnez la flèche suivant de hello.

1. Créer un nouveau compte de stockage, ou entrez un compte de stockage existant pour hello BizTalk Service.
2. Sélectionnez hello coche toostart hello restaurer.

Une fois la restauration de hello terminée avec succès, un BizTalk Service est répertorié dans l’état suspendu sur la page des Services BizTalk hello Bonjour portail Azure classic.

### <a name="postrestore"></a>Après avoir restauré une sauvegarde
Hello BizTalk Service est toujours restauré dans un **Suspended** état. Dans cet état, vous pouvez modifier n’importe quel configuration avant que le nouvel environnement de hello est fonctionnelle, y compris :

* Si vous avez créé des applications de BizTalk Service à l’aide de hello Azure BizTalk Services SDK, vous devrez peut-être les informations d’identification de tootooupdate hello Access Control (ACS) dans ces toowork d’applications avec l’environnement de hello restaurée.
* Vous restaurez un tooreplicate de BizTalk Service un environnement de BizTalk Service existant. Dans ce cas, s’il existe des accords configurés dans le portail BizTalk Services d’origine hello qui utilisent un dossier source FTP, vous devrez peut-être tooupdate les accords de hello en hello récemment restauré environnement toouse un serveur FTP source différente. Dans le cas contraire, il peut y avoir deux contrats différents lors de la tentative toopull hello même message.
* Si vous avez restauré toohave plusieurs environnements de BizTalk Service, assurez-vous que vous ciblez l’environnement approprié de hello dans les applications Visual Studio hello, les applets de commande PowerShell, les API REST ou les API OM de gestion des partenaires commerciaux.
* Il est conseillé tooconfigure automatisée sauvegardes dans l’environnement du Service BizTalk hello qui vient d’être restaurée.

toostart hello BizTalk Service Bonjour portail Azure classic, sélectionnez hello restauré BizTalk Service et sélectionnez **reprise** dans la barre des tâches hello. 

## <a name="what-gets-backed-up"></a>Éléments sauvegardés
Lors de la création d’une sauvegarde, hello éléments suivants sont sauvegardés :

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH>Éléments sauvegardés</TH> 
</tr> 
<tr>
<td colspan="2">
 <strong>Portail Azure BizTalk Services</strong></td>
</tr> 
<tr>
<td>Configuration et exécution</td> 
<td>
<ul>
<li>Détails du partenaire et du profil</li>
<li>Contrats partenaires</li>
<li>Assemblys personnalisés déployés</li>
<li>Ponts déployés</li>
<li>Certificats</li>
<li>Transformations déployées</li>
<li>Pipelines</li>
<li>Modèles créés et enregistrés dans hello portail BizTalk Services</li>
<li>Mappages X12 ST01 et GS01</li>
<li>Numéros de contrôle (EDI)</li>
<li>Valeurs MIC des messages AS2</li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2">
 <strong>Azure BizTalk Service</strong></td>
</tr> 
<tr>
<td>Certificat SSL</td> 
<td>
<ul>
<li>Données du certificat SSL</li>
<li>Mot de passe du certificat SSL</li>
</ul>
</td>
</tr> 
<tr>
<td>Paramètres du service BizTalk</td> 
<td>
<ul>
<li>Nombre d'unités mises à l'échelle</li>
<li>Édition</li>
<li>Version du produit</li>
<li>Région/centre de données</li>
<li>Espace de noms et clé Access Control Service (ACS)</li>
<li>Chaîne de connexion à la base de données de suivi</li>
<li>Chaîne de connexion au compte de stockage d'archive</li>
<li>Chaîne de connexion au compte de stockage de surveillance</li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2">
 <strong>Autres éléments</strong></td>
</tr> 
<tr>
<td>Base de données des suivis</td> 
<td>Lorsque hello BizTalk Service est créé, les détails de base de données de suivi hello sont entrés, notamment hello serveur de base de données SQL Azure et le nom de base de données de suivi hello. Hello de base de données de suivi n’est pas automatiquement sauvegardée.
<br/><br/>
<strong>Important</strong><br/>
Si hello suivi de la base de données est supprimée et hello des besoins de base de données récupérées, une sauvegarde précédente doit exister. Si une sauvegarde n’existe pas, hello suivi de la base de données et ses données ne sont pas récupérables. Dans ce cas, créez une nouvelle base de données de suivi avec hello même nom de base de données. La géo-réplication est recommandée.</td>
</tr> 
</table>

## <a name="next"></a>Suivant
toocreate Azure BizTalk Services dans hello Azure classic, accédez trop[BizTalk Services : portail classique de configuration à l’aide Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280). toostart création d’applications, accédez trop[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>Voir aussi
* [Sauvegarde d'un service BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [Restauration d'un service BizTalk depuis une sauvegarde](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [Tableau comparatif des éditions Développeur, De base, Standard et Premium de BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [BizTalk Services : approvisionnement à l’aide du portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [Tableau comparatif des états d'approvisionnement BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [Onglets Tableau de bord, Surveiller et Mettre à l'échelle dans BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [Limitation dans BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [Nom et clé de l'émetteur dans BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [Comment puis-je démarrer à l’aide de hello SDK des Services BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

