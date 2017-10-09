

## <a name="deployment-considerations"></a>Points à prendre en considération pour le déploiement
* **Abonnement Azure** – toodeploy plus de quelques instances de calcul intensif, envisagez un paiement à l’abonnement ou autres options d’achat. Si vous utilisez un [compte gratuit Azure](https://azure.microsoft.com/free/), vous pouvez seulement utiliser un nombre limité de cœurs de calcul Azure.

* **Tarification et la disponibilité** -tailles de ces machines virtuelles sont proposés uniquement dans la tarification Standard hello. Consultez [Disponibilité des produits par région] (https://azure.microsoft.com/regions/services/) pour connaître la disponibilité dans les régions Azure. 
* **Quota de cœurs** – vous devrez peut-être le quota de cœurs tooincrease hello dans votre abonnement Azure à partir de la valeur par défaut de hello. Votre abonnement peut également limiter hello nombre de cœurs, que vous pouvez déployer dans certaines familles de taille de machine virtuelle, y compris hello H-series. un quota de toorequest augmenter, [ouvrir une demande de support client en ligne](../articles/azure-supportability/how-to-create-azure-support-request.md) sans frais. (Les limites par défaut peuvent varier en fonction de la catégorie de votre abonnement.)
  
  > [!NOTE]
  > Si vous avez des besoins de capacité à grande échelle, contactez le support Azure. Les quotas d’Azure sont des limites de crédit et non des garanties de capacité. Quel que soit votre quota, vous êtes facturé uniquement pour les cœurs que vous utilisez.
  > 
  > 
* **Réseau virtuel** : Azure [réseau virtuel](https://azure.microsoft.com/documentation/services/virtual-network/) est toouse requis pas les instances de calcul intensif hello. Toutefois, pour nombreux déploiements, vous devez au moins un réseau virtuel Azure basé sur le cloud ou une connexion de site à site, si vous avez besoin de tooaccess ressources locales. Si nécessaire, créez un réseau virtuel instances de hello toodeploy. Ajout du réseau virtuel de calcul intensif machines virtuelles tooa dans un groupe d’affinités n’est pas pris en charge.
* **Redimensionnement** – en raison de leur matériel spécialisé, vous pouvez redimensionner uniquement les instances de calcul intensif dans hello même taille famille (série H ou nécessitant une série). Par exemple, vous pouvez uniquement redimensionner une machine virtuelle de série H à partir d’un tooanother de taille H-series. En outre, redimensionnement d’une taille de calcul intensif tooa nécessitant de taille n’est pas pris en charge.  
