| Ressource | Limite par défaut | Limite maximale |
| --- | --- | --- |
| Machines virtuelles par [abonnement](../articles/billing-buy-sign-up-azure-subscription.md) |10 000<sup>1</sup> par région |10 000 par région |
| Nombre total de cœurs de machine virtuelle par [abonnement](../articles/billing-buy-sign-up-azure-subscription.md) |20<sup>1</sup> par région | Contacter le support technique |
| Nombre de cœurs de gamme de machine virtuelle (Dv2, F, etc.) par [abonnement](../articles/billing-buy-sign-up-azure-subscription.md) |20<sup>1</sup> par région | Contacter le support technique |
| [Coadministrateurs](../articles/billing-add-change-azure-subscription-administrator.md) par abonnement |Illimité |Illimité |
| [Comptes de stockage](../articles/storage/common/storage-create-storage-account.md) par abonnement |200 |200<sup>2</sup> |
| [Groupes de ressources](../articles/azure-resource-manager/resource-group-overview.md) par abonnement |800 |800 |
| [Groupes à haute disponibilité](../articles/virtual-machines/windows/manage-availability.md#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) par abonnement |2 000 par région |2 000 par région |
| Lectures API Resource Manager |15 000 par heure |15 000 par heure |
| Écritures API Resource Manager |1 200 par heure |1 200 par heure |
| Taille de la demande d’API Resource Manager |4 194 304 octets |4 194 304 octets |
| Balises par abonnement<sup>3</sup> |illimitée |illimitée |
| Calculs de balise unique par abonnement<sup>3</sup> | 10 000 | 10 000 |
| [Services cloud](../articles/cloud-services/cloud-services-choose-me.md) par abonnement |Non applicable<sup>4</sup> |Non applicable<sup>4</sup> |
| [Groupes d'affinités](../articles/virtual-network/virtual-networks-migrate-to-regional-vnet.md) par abonnement |Non applicable<sup>4</sup> |Non applicable<sup>4</sup> |

<sup>1</sup>Les limites par défaut varient selon le type de catégorie d’offre, comme Essai gratuit ou Paiement à l’utilisation, et selon la gamme (Dv2, F, G, etc.).

<sup>2</sup>Cela inclut à la fois les comptes de stockage Standard et Premium. Si vous avez besoin de plus de 200 comptes de stockage, sollicitez le [Support Azure](https://azure.microsoft.com/support/faq/)pour obtenir une assistance. équipe du stockage Azure Hello Examinez vos cas et peut approuver les comptes de stockage too250.

<sup>3</sup>Vous pouvez appliquer un nombre illimité de balises par abonnement. nombre de Hello de balises par ressource ou un groupe de ressources est limitée too15. Le Gestionnaire de ressources retourne uniquement un [liste de valeurs et le nom de balise unique](/rest/api/resources/tags#Tags_List) dans l’abonnement hello lorsque nombre hello de balises est inférieur ou égal à 10 000. Toutefois, vous pouvez toujours trouver une ressource par balise lorsque le nombre de hello est supérieur à 10 000.  

<sup>4</sup>ces fonctionnalités ne sont plus nécessaires avec des groupes de ressources Azure et hello Azure Resource Manager.

> [!NOTE]
> Il est important tooemphasize qui cœurs de l’ordinateur virtuel ont une limite totale régionale ainsi un régionales par limite de série (Dv2, F, etc.) qui sont appliquées séparément.  Par exemple, considérons un abonnement dont le nombre total limite de cœurs de machine virtuelle est de 30 pour la région Est, de 30 pour la gamme A et de 30 pour la gamme D.  Cet abonnement serait autorisé toodeploy 30, A1 machines virtuelles, ou 30 ordinateurs virtuels de D1, ou une combinaison de hello deux pas tooexceed un total de 30 cœurs (par exemple, 10 machines virtuelles de A1 et 20 ordinateurs virtuels de D1).  
> <!-- -->
> 
> 

