Il existe deux types de comptes de stockage :

### <a name="general-purpose-storage-accounts"></a>Comptes de stockage à usage général
Un stockage à usage général compte vous donne accès tooAzure des services de stockage tels que Tables, files d’attente, fichiers, objets BLOB Azure disques des machines virtuelles sous un compte unique. Ce type de compte de stockage offre deux niveaux de performances :

* Un niveau de performances de stockage standard qui vous permet de toostore Tables, files d’attente, les fichiers, objets BLOB et Azure disques de machine virtuelle.
* Un niveau de performances de stockage premium qui prend actuellement en charge les disques de machine virtuelle Azure uniquement. Pour une présentation détaillée de Premium Storage, consultez [Premium Storage : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../articles/storage/common/storage-premium-storage.md) .

### <a name="blob-storage-accounts"></a>Comptes de stockage d’objets blob
Un compte de stockage d’objets blob est un compte de stockage spécialisé pour le stockage des données non structurées en tant qu’objets blob dans Azure Storage. Comptes de stockage d’objets BLOB sont similaires tooyour des comptes de stockage à usage général existants et de partagent tous les hello durabilité, disponibilité, évolutivité et performances fonctionnalités que vous utilisez aujourd'hui notamment la cohérence des API de 100 % pour les objets BLOB de blocs et objets BLOB d’ajout. Pour les applications qui requièrent uniquement le stockage d’objets blob de blocs ou d’objets blob d’ajout, nous recommandons d’utiliser des comptes de stockage d’objets blob.

> [!NOTE]
> Les comptes de stockage d’objets blob prennent en charge uniquement les objets blob de blocs et d’ajout, mais pas les objets blob de pages.
> 
> 

Comptes de stockage d’objets BLOB exposent hello **couche d’accès aux** attribut qui peut être spécifié lors de la création du compte et modifié par la suite en fonction des besoins. Il existe deux types de niveaux d’accès qui peuvent être spécifiés en fonction de votre modèle d’accès aux données :

* A **à chaud** niveau d’accès qui indique que les objets hello hello compte de stockage seront accessible plus fréquemment. Ainsi, vous toostore données à un coût de l’accès.
* A **froid** niveau d’accès qui indique que les objets hello hello compte de stockage seront accessible moins fréquemment. Cela vous permet de toostore données à un coût de stockage de données.

S’il existe une modification dans le modèle d’utilisation hello de vos données, vous pouvez également basculer entre ces niveaux d’accès à tout moment. Couche d’accès aux variables hello peut entraîner des frais supplémentaires. Consultez [Comptes de stockage d’objets blob - Tarification et facturation](../articles/storage/blobs/storage-blob-storage-tiers.md#pricing-and-billing) pour plus de détails.

Pour plus d’informations sur les comptes de stockage d’objets blob, voir [Stockage d’objets blob Azure : niveaux froid et chaud](../articles/storage/blobs/storage-blob-storage-tiers.md)

Avant de pouvoir créer un compte de stockage, vous devez disposer d’un abonnement Azure, qui est un plan qui permet d’accéder à divers services Azure tooa. Pour la prise en main d’Azure, vous pouvez bénéficier d’un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/). Une fois que vous décidez de toopurchase un plan d’abonnement, vous pouvez choisir parmi diverses [options d’achat](https://azure.microsoft.com/pricing/purchase-options/). Si vous êtes [abonné à MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), vous bénéficiez de crédits mensuels gratuits que vous pouvez utiliser avec les services Azure, y compris Azure Storage. Pour plus d’informations sur la tarification des licences en volume, consultez la page [Prix appliqués à Azure Storage ](https://azure.microsoft.com/pricing/details/storage/) .

toolearn toocreate un compte de stockage, voir [créer un compte de stockage](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account) pour plus d’informations. Vous pouvez créer jusqu'à too200 nommés de manière unique les comptes de stockage avec un seul abonnement. Pour plus d’informations sur les limites du compte de stockage, consultez la page [Objectifs de performance et évolutivité d’Azure Storage](../articles/storage/common/storage-scalability-targets.md) .

