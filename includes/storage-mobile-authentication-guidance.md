## <a name="configure-your-application-tooaccess-azure-storage"></a>Configurer votre tooaccess application Azure Storage
Il existe deux façons tooauthenticate votre tooaccess application services de stockage :

* Clé partagée : utilisez la clé partagée aux fins de test uniquement
* Signature d’accès partagé (SAP) : utilisez la signature d’accès partagé pour les applications de production

### <a name="shared-key"></a>Clé partagée
L’authentification de clé partagée signifie que votre application utilise votre nom de compte et tooaccess clé de compte de services de stockage. Pour des raisons de hello afficher rapidement comment toouse cette bibliothèque, nous allons utiliser l’authentification de clé partagée dans cette mise en route.

> [!WARNING] 
> **Utilisez uniquement l’authentification par clé partagée à des fins de test !** Votre nom de compte et votre clé de compte, donnant toohello d’accès en lecture/écriture intégral compte de stockage associé, personne tooevery distribuée qui télécharge de votre application. Ce n’est **pas** une bonne pratique car votre clé risque d’être compromise par des clients non approuvés.
> 
> 

Lorsque vous utilisez une authentification par clé partagée, vous créez une [chaîne de connexion](../articles/storage/common/storage-configure-connection-string.md). chaîne de connexion Hello se compose de :  

* Hello **DefaultEndpointsProtocol** -vous pouvez choisir de HTTP ou HTTPS. Toutefois, l’utilisation du protocole HTTPS est fortement recommandée.
* Hello **nom de compte** hello - nom de votre compte de stockage
* Hello **clé de compte** - sur hello [Azure Portal](https://portal.azure.com), accédez de compte de stockage tooyour, puis cliquez sur hello **clés** icône toofind ces informations.
* (Facultatif) **EndpointSuffix** : utilisé pour les services de stockage dans les régions avec des suffixes de point de terminaison différents, comme Azure China ou Azure Governance.

Voici un exemple de chaîne de connexion utilisant l’authentification par clé partagée :

`"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here"`

### <a name="shared-access-signatures-sas"></a>Signatures d’accès partagé (SAP)
Pour une application mobile, hello recommandé de méthode d’authentification d’une demande par un client contre hello service de stockage Azure est à l’aide d’une Signature d’accès partagé (SAS). Associations de sécurité vous permettant de toogrant une ressource de tooa d’accès client pour une période de temps, avec un jeu d’autorisations spécifié.
En tant que propriétaire du compte de stockage hello, vous devez toogenerate un SAS pour votre tooconsume de clients mobiles. toogenerate hello SAS, vous souhaiterez probablement toowrite un service séparé qui génère hello SAS toobe distributed tooyour clients. À des fins de test, vous pouvez utiliser hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) ou hello [Azure Portal](https://portal.azure.com) toogenerate une SAP. Lorsque vous créez hello SAS, vous pouvez spécifier l’intervalle de temps hello pendant le hello SAS est valide et autorisations hello hello SAP accorde toohello client.

Bonjour à l’exemple suivant montre comment toouse hello toogenerate de Microsoft Azure Storage Explorer une SAP.

1. Si vous n’avez pas déjà fait, [hello d’installer Microsoft Azure Storage Explorer](http://storageexplorer.com)
2. Se connecter tooyour abonnement.
3. Cliquez sur votre compte de stockage et cliquez sur l’onglet de hello « Actions » en hello en bas à gauche. Cliquez sur « Obtenir Signature d’accès partagé » toogenerate une chaîne de connexion « » de votre SAS.
4. Voici un exemple de chaîne de connexion SAS qu’accorde des autorisations de lecture et écriture au service de hello, conteneur et du niveau de l’objet de service d’objets blob hello hello du compte de stockage.
   
   `"SharedAccessSignature=sv=2015-04-05&ss=b&srt=sco&sp=rw&se=2016-07-21T18%3A00%3A00Z&sig=3ABdLOJZosCp0o491T%2BqZGKIhafF1nlM3MzESDDD3Gg%3D;BlobEndpoint=https://youraccount.blob.core.windows.net"`

Comme vous pouvez le voir, lorsque vous utilisez une SAP, vous n’exposez pas votre clé de compte dans votre application. Plus d’informations sur SAS et les meilleures pratiques pour utiliser des associations de sécurité en consultant [Signatures d’accès partagé : modèle de présentation hello SAP](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md).

