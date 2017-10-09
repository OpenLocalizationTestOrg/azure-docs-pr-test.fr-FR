<!--author=SharS last changed: 9/17/15-->

Dans cette procédure, vous allez :

1. [Préparer le fichier exécutable chargé de maintenance de hello toorun](#to-prepare-to-run-the-maintainer) .
2. [Préparer la base de données de contenu hello et la Corbeille pour la suppression immédiate d’objets BLOB orphelins](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).
3. [exécuter Maintainer.exe](#to-run-the-maintainer);
4. [Rétablir la base de données de contenu hello et les paramètres de la Corbeille](#to-revert-the-content-database-and-recycle-bin-settings).

#### <a name="tooprepare-toorun-hello-maintainer"></a>tooprepare toorun hello chargé de maintenance
1. Sur hello serveur Web frontal, ouvrez hello SharePoint 2013 Management Shell en tant qu’administrateur.
2. Exploration du dossier de toohello *lecteur de démarrage*: \Program Files\Microsoft 10.50\Maintainer de stockage d’objets Blob distants SQL\.
3. Renommer **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** trop**web.config**.
4. Utilisez `aspnet_regiis -pdf connectionStrings` fichier web.config de hello toodecrypt.
5. Dans fichier hello web.config déchiffrée, hello `connectionStrings` nœud, ajoutez la chaîne de connexion hello pour votre instance SQL server et hello du nom de la base de données de contenu. Consultez hello l’exemple suivant.
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. Utilisez `aspnet_regiis –pef connectionStrings` toore-chiffrer le fichier web.config de hello. 
7. Renommez tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config de web.config. 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a>base de données tooprepare hello et la Corbeille tooimmediately suppriment des objets BLOB orphelins
1. Sur hello SQL Server, dans SQL Management Studio, exécutez hello des requêtes de mise à jour pour la base de données contenu hello cible suivantes : 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. Sur hello serveur web frontal, sous **Administration centrale**, modifier hello **les paramètres généraux de l’Application Web** pour hello souhaité disable hello la Corbeille de contenu de la base de données tootemporarily. Cette action va également hello vide la Corbeille pour toutes les collections de sites connexes. toodo, cliquez sur **Administration centrale** -> **gestion des applications** -> **les Applications Web (gérer les applications web)**  ->  **SharePoint - 80** -> **les paramètres généraux de l’Application**. Ensemble hello **état de la Corbeille** trop**OFF**.
   
    ![Paramètres généraux de l'application Web](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a>toorun hello chargé de maintenance
* Sur le serveur frontal de web hello, Bonjour SharePoint 2013 Management Shell, exécutez hello chargé de maintenance comme suit :
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > Hello uniquement `GarbageCollection` est prise en charge pour StorSimple pour l’instant. Notez également que les paramètres de hello émises pour Microsoft.Data.SqlRemoteBlobs.Maintainer.exe respectent la casse. 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a>base de données contenu toorevert hello et les paramètres de la Corbeille
1. Sur hello SQL Server, dans SQL Management Studio, exécutez hello des requêtes de mise à jour pour la base de données contenu hello cible suivantes :
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. Sur le serveur frontal de web hello, dans **Administration centrale**, modifier hello **les paramètres généraux de l’Application Web** pour hello souhaité hello toore-enable de contenu de la base de données la Corbeille. toodo, cliquez sur **Administration centrale** -> **gestion des applications** -> **les Applications Web (gérer les applications web)**  ->  **SharePoint - 80** -> **les paramètres généraux de l’Application**. Définir hello état de la Corbeille trop**ON**.

