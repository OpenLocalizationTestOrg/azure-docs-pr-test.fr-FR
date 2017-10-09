>[!NOTE]
> Vous pouvez laisser des commentaires sur cette page, ou via [Azure feedback](https://feedback.azure.com/forums/216843-virtual-machines) (commentaires Azure) avec la balise #azerrormessage.

## <a name="error-response-format"></a>Format de réponse d’erreur 
Machines virtuelles Azure, utilisez hello suivant le format JSON pour la réponse d’erreur :

```json
{
  "status": "status code",
  "error": {
    "code":"Top level error code",
    "message":"Top level error message",
    "details":[
     {
      "code":"Inner evel error code",
      "message":"Inner level error message"
     }
    ]
   }
}
```

Une réponse d’erreur inclut systématiquement un code d’état et un objet d’erreur. Chaque objet d’erreur contient toujours un code d’erreur et un message. Si hello virtuel est créé avec un modèle objet d’erreur hello contient également une section de détails qui contient un niveau interne de codes d’erreur et le message. Normalement, hello la plupart des niveau interne de message d’erreur est Échec de la racine hello.


## <a name="common-virtual-machine-management-errors"></a>Erreurs courantes de gestion des machines virtuelles

Cette section répertorie hello messages d’erreur courants rencontrés lors de la gestion des machines virtuelles :

|  Code d'erreur  |  Message d’erreur  |  
|  :------| :-------------|  
|  AcquireDiskLeaseFailed  |  Échec de tooacquire bail lors de la création du disque '{0}' à l’aide d’objets blob avec {{1} de l’URI. L’objet blob est déjà utilisé.  |  
|  AllocationFailed  |  L’allocation a échoué. Essayez de réduire la taille de machine virtuelle hello ou le nombre d’ordinateurs virtuels, réessayez ultérieurement ou essayez de déployer tooa à haute disponibilité différent ou l’autre emplacement Azure.  |  
|  AllocationFailed  |  Hello allocation des machines virtuelles a échoué en raison de l’erreur interne de tooan. Veuillez réessayer plus tard ou essayez de déployer tooa autre emplacement.  |
|  ArtifactNotFound  |  Hello, extension de machine virtuelle avec le serveur de publication '{0}' et le type « {{1}' est introuvable dans l’emplacement « {{2} ».  |
|  ArtifactNotFound  |  Extension avec l’éditeur '{0}', tapez « {{1} », version du Gestionnaire de type « {{2} » est introuvable dans le référentiel d’extensions hello.  |
|  ArtifactVersionNotFound  |  Version introuvable dans le référentiel d’artefacts hello satisfaisant hello a demandé la version '{0}'.  |
|  ArtifactVersionNotFound  |  Version introuvable dans le référentiel d’artefacts hello satisfaisant hello demandé version avec le serveur de publication « {{1} » et « {{2} » de type '{0}' pour l’extension de machine virtuelle.  |
|  AttachDiskWhileBeingDetached  |  Impossible d’attacher tooVM disque '{0}' de données « {{1} », car le disque de hello est actuellement en cours de détachement. Veuillez patienter pendant que le disque de hello soit complètement détaché et réessayez.  |
|  BadRequest  |  Les groupes à haute disponibilité alignés ne sont pas encore pris en charge dans cette région.  |
|  BadRequest  |  Ajout d’une machine virtuelle avec des disques gérés gérés par toonon à haute disponibilité ou l’ajout d’une machine virtuelle avec l’objet blob en fonction toomanaged de disques à haute disponibilité n’est pas pris en charge. Créez un ensemble de disponibilité avec un jeu de propriétés « managé » dans l’ordre tooadd une machine virtuelle avec tooit de disques gérés.  |
|  BadRequest  |  Les disques gérés ne sont pas pris en charge dans cette région.  |
|  BadRequest  |  Plusieurs VMExtensions par gestionnaire non prises en charge pour le type de système d’exploitation « {0} ». VMExtension « {1} » avec le gestionnaire « {2} » déjà ajoutée ou spécifiée dans l’entrée.  |
|  BadRequest  |  L’opération « {0} » n’est pas prise en charge sur la ressource « {1} » comportant des disques gérés.  |
|  CertificateImproperlyFormatted  |  représentation sous forme de JSON du secret récupérée à partir de {0} Hello a un champ de données qui n’est pas un fichier PFX correctement mis en forme ou mot de passe hello fourni ne décode pas correctement le fichier PFX hello.  |
|  CertificateImproperlyFormatted  |  les données de salutation récupérées à partir de {0} ne sont pas désérialisables dans JSON.  |
|  Conflit  |  Redimensionnement de disque est autorisé uniquement lors de la création d’une machine virtuelle ou lorsque hello VM n’est pas libéré.  |
|  ConflictingUserInput  |  Impossible d’attacher le disque '{0}' comme disque de hello est déjà détenu par machine virtuelle « {{1} ».  |
|  ConflictingUserInput  |  Groupes de ressources source et destination sont hello même.  |
|  ConflictingUserInput  |  Les comptes de stockage source et de destination pour le disque {0} sont différents.  |
|  ContainerAlreadyOnLease  |  Il existe déjà un bail sur le conteneur de stockage hello maintenant blob hello avec l’URI {0}.  |
|  CrossSubscriptionMoveWithKeyVaultResources  |  demande de déplacement de ressources Hello contient des ressources KeyVault référencées par un ou plusieurs {0} s dans la demande hello. Pour le moment, cela n’est pas pris en charge dans le déplacement entre les abonnements. Vérifiez les détails de l’erreur hello pour hello ID de ressources KeyVault.  |
|  DiagnosticsOperationInternalError  |  Une erreur interne s’est produite pendant le traitement du profil de diagnostic de la machine virtuelle {0}.  |
|  DiskBlobAlreadyInUseByAnotherDisk  |  {0} de l’objet BLOB est déjà en cours d’utilisation par un autre disque appartenant tooVM « {{1} ». Vous pouvez examiner les métadonnées d’objets blob hello hello disque informations de référence.  |
|  DiskBlobNotFound  |  Impossible de toofind de disque dur virtuel d’objets blob avec {0} de l’URI pour le disque « {{1} ».  |
|  DiskBlobNotFound  |  Impossible de toofind de disque dur virtuel d’objets blob avec l’URI {0}.  |
|  DiskEncryptionKeySecretMissingTags  |  secret de {0} n’a pas les balises hello {{1}. Mettre à jour la version du secret hello, ajouter des balises de hello requis et recommencez.  |
|  DiskEncryptionKeySecretUnwrapFailed  |  Le désencapsulage de la valeur {0} du secret à l’aide de la clé {1} a échoué.  |
|  DiskImageNotReady  |  L’image de disque {0} est à l’état {1}. Réessayez lorsque l’image est prête.  |
|  DiskPreparationError  |  Une ou plusieurs erreurs se sont produites lors de la préparation des disques de machine virtuelle. Pour plus d’informations, consultez la vue d’instance de disque.  |
|  DiskProcessingError  |  Le traitement de disque interrompue que hello machine virtuelle a des autres disques dans des disques défaillants.  |
|  ImageBlobNotFound  |  Impossible de toofind de disque dur virtuel d’objets blob avec {0} de l’URI pour le disque « {{1} ».  |
|  ImageBlobNotFound  |  Impossible de toofind de disque dur virtuel d’objets blob avec l’URI {0}.  |
|  IncorrectDiskBlobType  |  Les objets blob de disques ne peuvent être que du type objet blob de pages. L’objet blob {0} du disque « {1} » est du type objet blob de blocs.  |
|  IncorrectDiskBlobType  |  Les objets blob de disques ne peuvent être que du type objet blob de pages. L’objet blob {0} est du type « {1} ».  |
|  IncorrectImageBlobType  |  Les objets blob de disques ne peuvent être que du type objet blob de pages. L’objet blob {0} du disque « {1} » est du type objet blob de blocs.  |
|  IncorrectImageBlobType  |  Les objets blob de disques ne peuvent être que du type objet blob de pages. L’objet blob {0} est du type « {1} ».  |
|  InternalOperationError  |  Impossible de résoudre le compte de stockage {0}. Veuillez vous assurer qu’il a été créé via hello fournisseur de ressources de stockage Bonjour même emplacement que hello la ressource de calcul.  |
|  InternalOperationError  |  Échec des tâches de recherche de valeur cible {0}.  |
|  InternalOperationError  |  Erreur lors de la validation du profil de réseau hello de machine virtuelle '{0}'.  |
|  InvalidAccountType  |  {0} de Hello AccountType n’est pas valide.  |
|  InvalidParameter  |  valeur Hello de {0} du paramètre n’est pas valide.  |
|  InvalidParameter  |  mot de passe administrateur Hello spécifié n’est pas autorisée.  |
|  InvalidParameter  |  « mot de passe hello fourni doit être comprise entre {0}-\ {1\\} caractères et doit satisfaire au moins {{2} des exigences de complexité de mot de passe depuis hello : <ol><li> Contient une majuscule.</li><li>Contient une minuscule.</li><li>Contient un chiffre.</li><li>Contient un caractère spécial.</li></ol>  |
|  InvalidParameter  |  Hello, nom d’utilisateur Admin spécifié n’est pas autorisée.  |
|  InvalidParameter  |  Impossible d’attacher un disque du système d’exploitation existant si hello machine virtuelle est créée à partir d’une image de plateforme ou d’utilisateur.  |
|  InvalidParameter  |  Le nom de conteneur {0} n’est pas valide. Les noms de conteneur doivent comporter 3 à 63 caractères, lesquels ne peuvent être que des caractères alphanumériques minuscules et un tiret. Le tiret doit être précédé et suivi d’un caractère alphanumérique.  |
|  InvalidParameter  |  Le nom de conteneur {0} indiqué dans l’URL {1} n’est pas valide. Les noms de conteneur doivent comporter 3 à 63 caractères, lesquels ne peuvent être que des caractères alphanumériques minuscules et un tiret. Le tiret doit être précédé et suivi d’un caractère alphanumérique.  |
|  InvalidParameter  |  nom d’objet blob Hello dans {0} de l’URL contient une barre oblique. Pour le moment, ce n’est pas pris en charge pour les disques.  |
|  InvalidParameter  |  {0} de Hello URI ne recherche pas toobe correct URI d’objet blob.  |
|  InvalidParameter  |  Un disque nommé '{0}' déjà utilise hello même LUN : {1}.  |
|  InvalidParameter  |  Un disque nommé « {0} » existe déjà.  |
|  InvalidParameter  |  Impossible de spécifier des remplacements d’image de l’utilisateur pour un disque déjà défini dans hello spécifié référence l’image.  |
|  InvalidParameter  |  Un disque nommé '{0}' déjà utilise hello {{1} de même URL de disque dur virtuel.  |
|  InvalidParameter  |  Bonjour {0} de compte de domaine erreur spécifiée doit être comprise dans la plage de hello {1} too\ {2\}.  |
|  InvalidParameter  |  {0} de type Hello licence n’est pas valide. Les types de licence valides sont les suivants : Windows_Client ou Windows_Server, avec respect de la casse.  |
|  InvalidParameter  |  Nom d’hôte Linux ne peut pas dépasser {0} caractères ou contenir les caractères suivants de hello : {1}.  |
|  InvalidParameter  |  Chemin d’accès de destination pour les clés publiques Ssh est {0} de valeur tooits actuellement limité par défaut échéance tooa problème dans l’agent d’approvisionnement Linux.  |
|  InvalidParameter  |  Il existe déjà un disque sur le numéro d’unité logique {0}.  |
|  InvalidParameter  |  {0} de l’abonnement de demande de hello doit correspondre à {{1} de l’abonnement hello contenue dans l’id de disque géré hello.  |
|  InvalidParameter  |  Les données personnalisées dans le profil OSProfile doivent être encodées en Base64, et leur longueur maximale doit être de {0} caractères.  |
|  InvalidParameter  |  Le nom de l’objet blob indiqué dans l’URL {0} doit se terminer par l’extension « {1} ».  |
|  InvalidParameter  |  {0} n’est pas un préfixe de nom d’objet blob VHD capturé valide. Un préfixe valide correspond à l’expression régulière « {1} ».  |
|  InvalidParameter  |  Certificats ne peuvent pas être ajoutés tooyour machine virtuelle si l’agent de machine virtuelle hello n’est pas configuré.  |
|  InvalidParameter  |  Il existe déjà un disque sur le numéro d’unité logique {0}.  |
|  InvalidParameter  |  Impossible toocreate hello VM car hello demandée {0} taille n’est pas disponible dans le cluster hello où hello à haute disponibilité est allouée actuellement. Hello les tailles disponibles sont : {1}. Pour en savoir plus sur la stratégie de redimensionnement de machine virtuelle, consultez la page https://aka.ms/azure-resizevm.  |
|  InvalidParameter  |  Hello demandé {0} taille de machine virtuelle n’est pas disponible dans la région actuelle de hello. Hello tailles disponibles dans la région actuelle de hello sont : {1}. Pour en savoir plus sur les tailles de machine virtuelle disponibles hello dans chaque région à https://aka.ms/azure-regions.  |
|  InvalidParameter  |  Hello demandé {0} taille de machine virtuelle n’est pas disponible dans la région actuelle de hello. Pour en savoir plus sur les tailles de machine virtuelle disponibles hello dans chaque région à https://aka.ms/azure-regions.  |
|  InvalidParameter  |  Nom d’utilisateur administrateur Windows ne peut pas dépasser {0} caractères long, se terminent par un point ou contient les caractères suivants de hello : {1}.  |
|  InvalidParameter  |  Nom de l’ordinateur Windows ne peut pas dépasser {0} caractères long, être entièrement numérique ou contient les caractères suivants de hello : {1}.  |
|  MissingMoveDependentResources  |  demande de déplacement de ressources Hello ne contient pas toutes les ressources dépendantes hello. Dans les détails de l’erreur, recherchez les ID des ressources manquantes.  |
|  MoveResourcesHaveInvalidState  |  demande de déplacement de ressources Hello contient des machines virtuelles qui sont associés à des comptes de stockage non valide. Dans les détails de l’erreur, recherchez les ID de ces ressources ainsi que les noms des comptes de stockage référencés.  |
|  MoveResourcesHavePendingOperations  |  demande de déplacement de ressources Hello contient des ressources pour lequel une opération est en attente. Dans les détails de l’erreur, recherchez les ID de ces ressources. Recommencez l’opération lorsque hello opérations en attente est terminée.  |
|  MoveResourcesNotFound  |  Hello déplacer des ressources de demande contient les ressources qui ne peut pas être trouvés. Dans les détails de l’erreur, recherchez les ID de ces ressources.  |
|  NetworkingInternalOperationError  |  Erreur d’allocation réseau inconnue.  |
|  NetworkingInternalOperationError  |  Erreur d’allocation réseau inconnue  |
|  NetworkingInternalOperationError  |  Une erreur interne s’est produite lors du traitement du profil de réseau de machine virtuelle de hello.  |
|  NotFound  |  {0} de la haute disponibilité Hello est introuvable.  |
|  NotFound  |  Machine virtuelle de source '{0}' spécifié dans la demande de hello n’existe pas dans cet emplacement Azure.  |
|  NotFound  |  Le client avec l’ID {0} est introuvable.  |
|  NotFound  |  Impossible de trouver le {0} de Hello Image.  |
|  NotSupported  |  type de licence Hello est {0}, mais le {{1} blob hello image n’est pas du site.  |
|  OperationNotAllowed  |  Impossible de supprimer le groupe à haute disponibilité {0}. Avant de supprimer un groupe à haute disponibilité, vérifiez qu’il ne contient aucune machine virtuelle.  |
|  OperationNotAllowed  |  Modification de disponibilité définie référence (SKU) à partir de 'Aligned' too'Classic' n’est pas autorisée.  |
|  OperationNotAllowed  |  Impossible de modifier les extensions Bonjour VM lorsque hello VM n’est pas en cours d’exécution.  |
|  OperationNotAllowed  |  Hello une action de Capture est uniquement pris en charge sur un ordinateur virtuel avec les disques de l’objet blob en fonction. Utilisez hello « Image » ressource API toocreate une Image à partir d’un ordinateur virtuel géré.  |
|  OperationNotAllowed  |  Hello ressource {0} ne peut pas être créé à partir de {{1} de l’Image jusqu'à ce que l’Image a été créée avec succès.  |
|  OperationNotAllowed  |  Mises à jour tooencryptionSettings n’est pas autorisée lors de la machine virtuelle est allouée réessayez une fois la machine virtuelle est désallouée.  |
|  OperationNotAllowed  |  Ajout d’une machine virtuelle de tooa disque géré avec des disques de l’objet blob en fonction n’est pas pris en charge.  |
|  OperationNotAllowed  |  nombre maximal de Hello de disques de données autorisée toobe jointe tooa machine virtuelle de cette taille est {0}.  |
|  OperationNotAllowed  |  Ajout d’un tooVM de disque en fonction des blob avec des disques gérés n’est pas pris en charge.  |
|  OperationNotAllowed  |  Opération '{0}' n’est pas autorisée sur l’Image « {{1} » depuis hello Qu'image est marquée pour suppression. Vous pouvez uniquement recommencez l’opération de suppression hello (ou attendre une un toocomplete en cours).  |
|  OperationNotAllowed  |  Opération '{0}' n’est pas autorisée sur la machine virtuelle « {{1} » depuis hello que cette dernière est généralisée.  |
|  OperationNotAllowed  |  L’opération « {0} » n’est pas autorisée, car la collection de points de restauration « {1} » est marquée pour suppression.  |
|  OperationNotAllowed  |  L’opération « {0} » n’est pas autorisée sur l’extension de machine virtuelle « {1} », car cette dernière est marquée pour suppression. Vous pouvez uniquement recommencez l’opération de suppression hello (ou attendre une un toocomplete en cours).  |
|  OperationNotAllowed  |  Opération '{0}' n’est pas autorisée car hello Machines virtuelles « {{1}' sont en cours d’approvisionnement à l’aide de hello Image « {{2}'.  |
|  OperationNotAllowed  |  Opération '{0}' n’est pas autorisée car hello ScaleSet d’ordinateur virtuel « {{1} » hello Image « {{2} ».  |
|  OperationNotAllowed  |  Opération '{0}' n’est pas autorisée sur la machine virtuelle « {{1} » depuis hello que machine virtuelle est marquée pour suppression. Vous pouvez uniquement recommencez l’opération de suppression hello (ou attendre une un toocomplete en cours).  |
|  OperationNotAllowed  |  Opération '{0}' n’est pas autorisée sur la machine virtuelle « {{1}', car hello machine virtuelle est désallouée ou marquée toobe désallouée.  |
|  OperationNotAllowed  |  Opération '{0}' n’est pas autorisée sur la machine virtuelle « {{1} » depuis hello que machine virtuelle est en cours d’exécution. Veuillez mettre hors tension explicitement au cas où vous arrêter hello machine virtuelle à partir à l’intérieur du système d’exploitation de hello invité.  |
|  OperationNotAllowed  |  Opération '{0}' n’est pas autorisée sur la machine virtuelle « {{1} » depuis hello que machine virtuelle n’est pas libérée.  |
|  OperationNotAllowed  |  L’opération « {0} » n’est pas autorisée sur la machine virtuelle « {1} », car l’extension « {2} » de la machine virtuelle est à l’état d’échec.  |
|  OperationNotAllowed  |  L’opération « {0} » n’est pas autorisée sur la machine virtuelle « {1} », car une autre opération est en cours.  |
|  OperationNotAllowed  |  opération de Hello '{0}' requiert hello Machine virtuelle « {{1} » toobe généralisé.  |
|  OperationNotAllowed  |  opération de Hello requiert hello toobe de machine virtuelle en cours d’exécution (ou définie toorun).  |
|  OperationNotAllowed  |  Disque avec une taille de {0} Go, qui est la taille est plus petit que hello {1}GB de disque dans l’Image, n’est pas autorisée.  |
|  OperationNotAllowed  |  Ensemble d’échelle de machine virtuelle des extensions du gestionnaire '{0}' peuvent être ajoutées uniquement au moment de hello de création de l’ensemble d’échelle de machine virtuelle.  |
|  OperationNotAllowed  |  Ensemble d’échelle de machine virtuelle des extensions du gestionnaire '{0}' peuvent être supprimées uniquement au moment de hello de suppression d’ensemble d’échelle de machine virtuelle.  |
|  OperationNotAllowed  |  La machine virtuelle « {0} » utilise déjà des disques gérés.  |
|  OperationNotAllowed  |  Machine virtuelle '{0}' appartient too'Classic' ensemble de disponibilité « {{1} ». Veuillez mise à jour hello disponibilité définir toouse « Aligné » référence (SKU), puis réessayez hello Conversion.  |
|  OperationNotAllowed  |  La machine virtuelle créée à partir d’une image ne peut pas posséder de disques basés sur des objets blob. Tous les disques ont des disques toobe géré.  |
|  OperationNotAllowed  |  Capturer opération ne peut pas aboutir car hello VM n’est pas généralisée.  |
|  OperationNotAllowed  |  Opérations de gestion sur l’ordinateur virtuel '{0}' ne sont pas autorisées, car les disques de machine virtuelle sont en cours toomanaged converti disques.  |
|  OperationNotAllowed  |  Une opération en cours change d’état d’alimentation de l’ordinateur virtuel {0} too\ {1\\}. Après un certain temps, effectuez l’opération {2}.  |
|  OperationNotAllowed  |  Impossible de tooadd ou mise à jour hello machine virtuelle. Hello demandé {0} taille de machine virtuelle n’est peut-être pas disponible dans l’unité d’allocation hello existant. Pour en savoir plus sur la stratégie de redimensionnement de machine virtuelle, consultez la page https://aka.ms/azure-resizevm.  |
|  OperationNotAllowed  |  Impossible tooresize hello VM car hello demandée {0} taille n’est pas disponible dans le cluster hello où hello à haute disponibilité est allouée actuellement. Hello les tailles disponibles sont : {1}. Pour en savoir plus sur la stratégie de redimensionnement de machine virtuelle, consultez la page https://aka.ms/azure-resizevm.  |
|  OperationNotAllowed  |  Impossible tooresize hello VM car hello demandée {0} taille n’est pas disponible dans le cluster hello où hello machine virtuelle est allouée actuellement. tooresize votre too\ de machine virtuelle {1\\} Veuillez libérer (il s’agit d’opération d’arrêt dans hello portail Azure), puis recommencez l’opération de redimensionnement hello à nouveau. Pour en savoir plus sur la stratégie de redimensionnement de machine virtuelle, consultez la page https://aka.ms/azure-resizevm.  |
|  OSProvisioningClientError  |  Échec du déploiement de système d’exploitation pour la machine virtuelle '{0}', car le système d’exploitation invité de hello est actuellement en cours d’approvisionnement.  |
|  OSProvisioningClientError  |  Échec de l’approvisionnement du système d’exploitation pour la machine virtuelle « {0} ». Détails de l’erreur : {{1} Vérifiez qu’image de hello a été correctement préparée (généralisée). <ul><li>Instructions pour Windows : https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/  </li></ul> |
|  OSProvisioningClientError  |  Échec de la génération de clé hôte SSH. Détails de l’erreur : {0}. tooresolve ce problème vérifier si l’agent Linux est correctement configuré. <ul><li>Vous pouvez vérifier les instructions hello à : https://azure.microsoft.com/documentation/articles/virtual-machines-linux-agent-user-guide/ </li></ul> |
|  OSProvisioningClientError  |  Nom d’utilisateur spécifié pour hello que VM n’est pas valide pour cette distribution de Linux. Détails de l’erreur : {0}.  |
|  OSProvisioningInternalError  |  Échec de la mise en service du système d’exploitation pour la machine virtuelle '{0}' en raison de l’erreur interne de tooan.  |
|  OSProvisioningTimedOut  |  Configuration de système d’exploitation pour la machine virtuelle '{0}' n’a pas fini Bonjour période. Hello machine virtuelle peut néanmoins se terminer avec succès. Vérifiez l’état d’approvisionnement ultérieurement.  |
|  OSProvisioningTimedOut  |  Configuration de système d’exploitation pour la machine virtuelle '{0}' n’a pas fini Bonjour période. Hello machine virtuelle peut néanmoins se terminer avec succès. Vérifiez l’état d’approvisionnement ultérieurement. Assurez-vous également que l’image de hello a été correctement préparée (généralisée).   <ul><li>Instructions pour Windows : https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Instructions pour Linux : https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OSProvisioningTimedOut  |  Configuration de système d’exploitation pour la machine virtuelle '{0}' n’a pas fini Bonjour période. Toutefois, l’agent invité d’ordinateur virtuel hello a été détecté en cours d’exécution. Par conséquent, invité hello système d’exploitation n’a pas été correctement préparée toobe utilisé comme une image de machine virtuelle (avec CreateOption = FromImage). tooresolve ce problème, soit hello utilisation disque dur virtuel à avec CreateOption = attacher ou préparer correctement pour l’utiliser en tant qu’image :   <ul><li>Instructions pour Windows : https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Instructions pour Linux : https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OverConstrainedAllocationRequest  |  Hello requises de taille de machine virtuelle n’est pas disponible actuellement dans l’emplacement de hello sélectionné.  |
|  ResourceUpdateBlockedOnPlatformUpdate  |  Ressource ne peut pas être mises à jour en raison de la mise à jour de plateforme tooongoing. Veuillez réessayer plus tard.  |
|  StorageAccountLimitation  |  Compte de stockage '{0}' ne prend pas en charge les objets BLOB de pages qui est des disques toocreate requis.  |
|  StorageAccountLimitation  |  Le compte de stockage « {0} » a dépassé son quota alloué.  |
|  StorageAccountLocationMismatch  |  Impossible de résoudre le compte de stockage {0}. Veuillez vous assurer qu’il a été créé via hello fournisseur de ressources de stockage Bonjour même emplacement que hello la ressource de calcul.  |
|  StorageAccountNotFound  |  Compte de stockage {0} introuvable. Vérifiez le compte de stockage n’est pas supprimé et appartient toohello même emplacement que celui de hello machine virtuelle.  |
|  StorageAccountNotRecognized  |  Utilisez un compte de stockage géré par le fournisseur de ressources de stockage. L’utilisation de « {0} » n’est pas prise en charge.  |
|  StorageAccountOperationInternalError  |  Une erreur interne s’est produite lors de l’accès au compte de stockage {0}.  |
|  StorageAccountSubscriptionMismatch  |  {0} du compte de stockage n’appartient pas {{1} toosubscription.  |
|  StorageAccountTooBusy  |  Le compte de stockage « {0} » est actuellement trop occupé. Pensez à utiliser un autre compte.  |
|  StorageAccountTypeNotSupported  |  Le disque {0} utilise {1} qui est un compte de stockage d’objets blob. Réessayez avec un compte de stockage à usage général.  |
|  StorageAccountTypeNotSupported  |  Le compte de stockage {0} est de type {1}. La fonctionnalité Diagnostics de démarrage prend en charge {2} types de compte de stockage.  |
|  SubscriptionNotAuthorizedForImage  |  abonnement de Hello n’est pas autorisé.  |
|  TargetDiskBlobAlreadyExists  |  L’objet blob {0} existe déjà. Veuillez fournir un toocreate d’URI de différents objets blob une nouvelle données vierge disque « {{1}'.  |
|  TargetDiskBlobAlreadyExists  |  Capture Impossible de continuer l’opération, car le {0} blob cible image existe déjà et objets BLOB de hello indicateur toooverwrite disque dur virtuel n’est pas défini. Soit supprimer l’objet blob de hello ou définir des objets BLOB de disque dur virtuel toooverwrite indicateur de hello et recommencez.  |
|  TargetDiskBlobAlreadyExists  |  L’opération de capture ne peut pas continuer, car un bail est actif sur l’objet blob d’image cible {0}.   |
|  TargetDiskBlobAlreadyExists  |  L’objet blob {0} existe déjà. Spécifiez un autre URI d’objet blob comme cible pour le disque « {1} ».  |
|  TooManyVMRedeploymentRequests  |  Trop de demandes de redéploiement reçues pour la machine virtuelle '{0}' ou machines virtuelles hello hello availabilityset même avec cet ordinateur virtuel. Veuillez réessayer ultérieurement.  |
|  VHDSizeInvalid  |  Hello spécifié la valeur de taille de disque de {0} pour « {{1}' avec {{2} de l’objet blob de disque n’est pas valide. La taille de disque doit être comprise entre {3} et {4}.  |
|  VMAgentStatusCommunicationError  |  La machine virtuelle « {0} » n’a pas signalé d’état pour l’agent ou les extensions de machine virtuelle. Veuillez vérifier hello machine virtuelle dispose d’un agent de machine virtuelle en cours d’exécution et peut établir stockage tooAzure de connexions sortantes.  |
|  VMArtifactRepositoryInternalError  |  Une erreur s’est produite lors de la communication avec les détails de l’artefact hello artefact référentiel tooretrieve machine virtuelle.  |
|  VMArtifactRepositoryInternalError  |  Une erreur interne s’est produite lors de la récupération des données d’artefact hello machine virtuelle à partir du référentiel d’artefacts hello.  |
|  VMExtensionHandlerNonTransientError  |  Le gestionnaire « {0} » a signalé un problème au niveau de l’extension de machine virtuelle « {1} » avec le code d’erreur de terminal « {2} » et le message d’erreur : « {3} »  |
|  VMExtensionManagementInternalError  |  Une erreur interne s’est produite lors du traitement de l’extension de machine virtuelle « {0} ».  |
|  VMExtensionManagementInternalError  |  Plusieurs erreurs se sont produites lors de la préparation des extensions de machine virtuelle hello. Pour plus d’informations, consultez la vue d’instance de l’extension de machine virtuelle.  |
|  VMExtensionProvisioningError  |  La machine virtuelle a signalé un échec lors du traitement de l’extension « {0} ». Message d’erreur : « {1} ».  |
|  VMExtensionProvisioningError  |  Échec de plusieurs extensions de machine virtuelle toobe configuré sur la machine virtuelle de hello. Consultez la vue d’instance hello VM extension pour plus d’informations.  |
|  VMExtensionProvisioningTimeout  |  Le délai d’attente d’approvisionnement de l’extension de machine virtuelle « {0} » est arrivé à expiration. L’installation de l’extension prend peut-être trop de temps ou l’état de l’extension n’a pas pu être obtenu.  |
|  VMMarketplaceInvalidInput  |  Création d’un ordinateur virtuel à partir d’une image non-Marketplace ne doivent envisagez pas d’informations, veuillez supprimer hello informations de Plan dans la demande hello. Le nom du disque du système d’exploitation est {0}.  |
|  VMMarketplaceInvalidInput  |  informations d’achat Hello ne correspondent pas. Toodeploy impossible à partir d’une image Marketplace hello. Le nom du disque du système d’exploitation est {0}.  |
|  VMMarketplaceInvalidInput  |  Création d’un ordinateur virtuel à partir d’une image Marketplace nécessite des informations de Plan dans la demande hello. Le nom du disque du système d’exploitation est {0}.  |
|  VMNotFound  |  Hello machine virtuelle '{0}' est introuvable.  |
|  VMRedeploymentFailed  |  Redéploiement de la machine virtuelle '{0}' a échoué en raison de l’erreur interne de tooan. Veuillez réessayer ultérieurement.  |
|  VMRedeploymentTimedOut  |  Redéploiement de la machine virtuelle '{0}' n’a pas terminé dans la période de hello. Il peut se terminer correctement dans un certain temps. Sinon, vous pouvez retenter la demande de hello.  |
|  VMStartTimedOut  |  Machine virtuelle '{0}' n’a pas démarré dans la période de hello. Hello machine virtuelle peut néanmoins démarrer correctement. Veuillez vérifier état d’alimentation hello plus tard.  |


## <a name="next-steps"></a>Étapes suivantes
Si vous avez besoin d’aide, vous pouvez contacter hello experts Azure sur [hello forums MSDN Azure et le débordement de pile](https://azure.microsoft.com/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de support technique Azure](https://azure.microsoft.com/support/options/) et sélectionnez **obtenir prend en charge**.
