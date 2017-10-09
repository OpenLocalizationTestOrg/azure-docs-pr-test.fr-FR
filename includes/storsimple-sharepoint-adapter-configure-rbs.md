<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> Quand vous apportez des modifications toohello l’adaptateur StorSimple pour la configuration de SharePoint RBS, vous devez être connecté avec un compte d’utilisateur auquel appartient le groupe Admins du domaine de toohello. En outre, vous devez accéder page de configuration hello à partir d’un navigateur en cours d’exécution sur le même hôte que l’Administration centrale de hello.
> 
> 

#### <a name="tooconfigure-rbs"></a>tooconfigure RBS
1. Ouvrez la page d’Administration centrale de SharePoint hello et parcourir trop**paramètres système**. 
2. Bonjour **Azure StorSimple** , cliquez sur **configurer l’adaptateur StorSimple**.
   
    ![Configurer hello l’adaptateur StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. Sur hello **configurer l’adaptateur StorSimple** page :
   
   1. Vérifiez que hello **activer le chemin de l’édition** case à cocher est activée.
   2. Dans la zone de texte hello, tapez le chemin de Universal Naming Convention (UNC) de hello du magasin d’objets BLOB hello.
      
      > [!NOTE]
      > volume du magasin d’objets BLOB Hello doit être hébergé sur un volume iSCSI configuré sur l’appareil StorSimple hello.

   3. Cliquez sur hello **activer** situé sous chacune des bases de données contenu hello que vous souhaitez tooconfigure pour le stockage étendu.
      
      > [!NOTE]
      > magasin d’objets BLOB Hello doit être partagé par tous les serveurs web frontaux (WFE) et le compte d’utilisateur hello est configuré pour la batterie de serveurs SharePoint hello doit avoir accès toohello partagé.
      
      ![Activer le fournisseur RBS hello](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      Lorsque vous activez ou désactivez RBS, vous verrez également hello message suivant.
      
      ![Désactivation activation Configuration de l’adaptateur StorSimple](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. Cliquez sur hello **mise à jour** configuration hello tooapply du bouton. Lorsque vous cliquez sur hello **mise à jour** bouton, hello état RBS de la configuration sera mise à jour sur tous les serveurs Web frontaux et ensemble de la batterie hello sera activée pour RBS. Hello message suivant s’affiche.
      
      ![Message de configuration de l’adaptateur](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > Si vous configurez RBS pour une batterie de serveurs SharePoint avec un très grand nombre de bases de données (plus de 200), la page web de l’Administration centrale de SharePoint hello peut expirer. Si cela se produit, actualisez la page de hello. Cela n’affecte pas le processus de configuration hello.

4. Vérifier la configuration de hello :
   
   1. Ouvrez une session sur le site Web d’Administration centrale de SharePoint toohello et parcourir toohello **configurer l’adaptateur StorSimple** page.
   2. Vérifiez hello configuration détails toomake assurer qu’ils correspondent aux paramètres hello que vous avez entré. 
5. Vérifiez que RBS fonctionne correctement :
   
   1. Télécharger un document tooSharePoint. 
   2. Parcourir le chemin d’accès UNC toohello que vous avez configuré. Assurez-vous que la structure de répertoire RBS hello a été créé et qu’il contient l’objet de hello téléchargé.
6. (Facultatif) Vous pouvez utiliser hello Microsoft RBS `Migrate()` inclus avec SharePoint toomigrate BLOB contenu toohello StorSimple unité de l’applet de commande PowerShell. Pour plus d’informations, consultez [migrer le contenu dans ou hors de RBS dans SharePoint 2013] [ 6] ou [migrer le contenu dans ou hors de RBS (SharePoint Foundation 2010)] [7].
7. (Facultatif) Sur les installations de test, vous pouvez vérifier que hello BLOB ont été déplacés en dehors de la base de données de contenu hello comme suit : 
   
   1. Démarrez SQL Management Studio.
   2. Exécutez la requête ListBlobsInDB_2010.sql ou ListBlobsInDB_2013.sql de hello, comme suit.
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      Si RBS est correctement configuré, une valeur NULL doit apparaître dans la colonne de SizeOfContentInDB hello pour tout objet qui a été téléchargé et effectivement externalisé avec RBS.
8. (Facultatif) Après avoir configuré RBS et déplacer tous les objets BLOB de toohello contenu appareil StorSimple, vous pouvez déplacer l’appareil de toohello hello contenu de la base de données. Si vous choisissez la base de données de contenu de hello toomove, nous vous recommandons de configurer stockage de base de données de contenu hello sur périphérique hello comme volume principal. Ensuite, utilisez établie SQL Server de meilleures pratiques pour l’appareil StorSimple toohello toomigrate hello contenu de la base de données. 
   
   > [!NOTE]
   > Déplacement hello contenu de la base de données toohello est uniquement pris en charge pour la série de hello StorSimple 8000 (il n’est pas compatible avec la série de hello 5000 ou 7000).
   
   Si vous stockez des objets BLOB et base de données de contenu hello dans des volumes distincts sur l’appareil StorSimple hello, nous vous recommandons de configurer les Bonjour même conteneur de volume. Cela garantit qu’ils seront sauvegardés ensemble.
   
   > [!WARNING]
   > Si vous n’avez pas activé RBS, il est déconseillé de déplacement de l’appareil StorSimple hello contenu de la base de données toohello. Il s'agit d'une configuration non testée.
   
9. Étape suivante de toohello accédez : [configurer le garbage collection](#configure-garbage-collection).

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
