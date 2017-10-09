<!--author=SharS last changed: 9/17/15-->

### <a name="upgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-storsomple-adapter-for-sharepoint"></a>Mise à niveau de SharePoint 2010 tooSharePoint 2013, puis installez hello StorSomple adaptateur pour SharePoint
> [!IMPORTANT]
> Tous les fichiers qui ont été préalablement déplacés de stockage tooexternal via RBS ne seront pas disponible jusqu'à la fin de la mise à niveau hello et hello fonctionnalité RBS est activé. toolimit utilisateur impact, toute mise à niveau ou la réinstallation pendant une fenêtre de maintenance planifiée.
> 
> 

#### <a name="tooupgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-adapter"></a>tooupgrade SharePoint 2010 tooSharePoint 2013, puis installer l’adaptateur hello
1. Dans la batterie de serveurs SharePoint 2010 de hello, Remarque hello BLOB stocker le chemin d’accès pour hello externalisées des objets BLOB et les bases de données de contenu hello pour lesquelles RBS est activé. 
2. Installez et configurez la batterie de serveurs SharePoint 2013 hello. 
3. Déplacer les bases de données, des applications et des collections de sites à partir de SharePoint 2010 de hello batterie toohello nouvelle batterie SharePoint 2013. Pour obtenir des instructions, consultez trop[vue d’ensemble de la mise à niveau de hello tooSharePoint 2013](https://technet.microsoft.com/library/cc262483.aspx).
4. Installez hello adaptateur StorSimple pour SharePoint sur la batterie de serveurs hello. Accédez trop[hello d’installation de l’adaptateur StorSimple pour SharePoint](#install-the-storsimple-adapter-for-sharepoint) pour les procédures.
5. À l’aide des informations de hello que vous avez noté à l’étape 1, pour activer RBS pour hello même ensemble de bases de données et fournir hello même objet BLOB stocker le chemin d’accès qui a été utilisé dans l’installation de hello SharePoint 2010. Accédez trop[RBS de configurer](#configure-rbs) pour les procédures. Après avoir effectué cette étape, les fichiers externalisés précédemment doivent être accessibles à partir de la batterie de serveurs hello. 

### <a name="upgrade-hello-storsimple-adapter-for-sharepoint"></a>Hello mise à niveau de l’adaptateur StorSimple pour SharePoint
> [!IMPORTANT]
> Vous devez planifier cette mise à niveau toooccur pendant une fenêtre de maintenance planifiée pour hello suivant raisons :
> 
> * Précédemment externalisé contenu ne sera pas disponible jusqu'à ce que l’adaptateur hello est réinstallé.
> * Tout le contenu téléchargé toohello site lorsque vous désinstallez la version précédente de hello Hello adaptateur StorSimple pour SharePoint, mais avant l’installation de la nouvelle version de hello, sont stockés dans la base de données de contenu hello. Vous devez toomove périphérique StorSimple toohello contenu après avoir installé le nouvel adaptateur de hello. Vous pouvez utiliser hello Microsoft` RBS Migrate()` incluse avec le contenu de hello toomigrate SharePoint de l’applet de commande PowerShell. Pour plus d'informations, consultez [Migration du contenu vers ou à partir de RBS](https://technet.microsoft.com/library/ff628255.aspx). 
> 
> 

#### <a name="tooupgrade-hello-storsimple-adapter-for-sharepoint"></a>tooupgrade hello adaptateur StorSimple pour SharePoint
1. Désinstallez la version précédente de hello de l’adaptateur StorSimple pour SharePoint.
   
   > [!NOTE]
   > Cela désactive automatiquement RBS sur les bases de données de contenu hello. Toutefois, les objets BLOB existants resteront sur l’appareil StorSimple hello. RBS est désactivé et hello BLOB n’ont pas été migrés toohello arrière les bases de données de contenu, les demandes de ces objets BLOB échouera. 
   > 
   > 
2. Installation Bonjour nouvel adaptateur StorSimple pour SharePoint. nouvelle carte de Hello reconnaîtra automatiquement hello bases de données qui étaient auparavant activées ou désactivées pour RBS et utilisera les paramètres précédents hello.

