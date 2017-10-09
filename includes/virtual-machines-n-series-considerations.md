## <a name="deployment-considerations"></a>Points à prendre en considération pour le déploiement

* Pour connaître la disponibilité des machines virtuelles, consultez [Disponibilité des produits par région](https://azure.microsoft.com/en-us/regions/services/).

* Machines virtuelles de série N peuvent uniquement être déployés dans le modèle de déploiement du Gestionnaire de ressources hello.

* Lorsque la création d’un à l’aide de la machine virtuelle de série N hello portail Azure, sur hello **notions de base** panneau, sélectionnez un **type de disque de machine virtuelle** de **HDD**. taille de toochoose une série de N disponible, sur hello **taille** panneau, cliquez sur **afficher toutes les**.

* Les machines virtuelles de série N ne prennent pas en charge les disques de machines virtuelles sauvegardés par le stockage Premium Azure.

* Si vous souhaitez toodeploy plusieurs machines virtuelles de série N, envisagez un paiement à l’abonnement ou autres options d’achat. Si vous utilisez un [compte gratuit Azure](https://azure.microsoft.com/free/), vous pouvez seulement utiliser un nombre limité de cœurs de calcul Azure.

* Vous avez besoin de quota de cœurs tooincrease hello (par région) dans votre abonnement Azure et augmenter le quota de distinct hello pour CN ou NV cœurs. un quota de toorequest augmenter, [ouvrir une demande de support client en ligne](../articles/azure-supportability/how-to-create-azure-support-request.md) sans frais. Les limites par défaut peuvent varier en fonction de la catégorie de votre abonnement.

* Une image de machine virtuelle que vous pouvez déployer sur des machines virtuelles de série N est hello [une Machine virtuelle pour la science des données Azure](../articles/machine-learning/machine-learning-data-science-virtual-machine-overview.md). Hello Machine virtuelle de science des données préinstalle et configure les nombreux science des données populaires et approfondie outils d’apprentissage. Des pilotes NVIDIA Tesla GPU sont également préinstallés pour les instances NC.





