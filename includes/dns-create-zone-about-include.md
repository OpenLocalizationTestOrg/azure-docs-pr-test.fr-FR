Une zone DNS est toohost utilisé hello les enregistrements DNS pour un domaine particulier. toostart hébergeant votre domaine dans le système DNS Azure, vous devez toocreate une zone DNS pour ce nom de domaine. Chaque enregistrement DNS pour votre domaine est ensuite créé à l’intérieur de cette zone DNS.

Par exemple, hello domaine « contoso.com » peut contenir plusieurs enregistrements DNS, tels que « mail.contoso.com » (pour un serveur de messagerie) et « www.contoso.com » (pour un site web).

Lorsque vous créez une zone DNS dans Azure DNS :

* nom Hello de zone de hello doit être unique dans le groupe de ressources hello et zone de hello ne doit pas déjà exister. Dans le cas contraire, hello échoue.
* Hello nom de la même zone peut être réutilisée dans un autre groupe de ressources ou un autre abonnement Azure.
* Où plusieurs zones partager hello même nom, chaque instance est assigné adresses de serveur de nom différent. Qu’un seul ensemble d’adresses peut être configuré avec un enregistrement de domaines hello.

> [!NOTE]
> Vous n’avez pas tooown un toocreate de nom de domaine une zone DNS avec ce nom de domaine dans Azure DNS. En revanche, vous devez tooown hello domaine tooconfigure hello Azure serveurs DNS comme hello des serveurs de noms correct pour le nom de domaine hello avec l’enregistrement de domaines hello.
> 
> Pour plus d’informations, consultez [déléguer un tooAzure de domaine DNS](../articles/dns/dns-domain-delegation.md).
