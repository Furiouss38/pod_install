**Roles Ansible pour déployer et mettre à jour POD v2 sur 1 ou plusieurs serveurs**

Créer son inventaire à partir de inventory.template.yml  
  
Dans la section [pod] rentrer le ou les serveurs selon le modèle suivant :  
  
[pod]  
frontal1.domaine.fr state=present frontal='oui' db_host='127.0.0.1' rabbit_host='localhost' allowed_long='frontal1.domaine.fr' allowed_short='frontal1'  encodage='non' elastic_host='elastic1' elastic_ip='2.2.2.2' elastic='non'  
encode1.domaine.fr state=present encodage='oui' frontal='non' elastic='non' db_host='1.1.1.1' rabbit_host='1.1.1.1' elastic_host='frontal1' elastic_ip='2.2.2.2'  
elastic1.domaine.fr state=present elastic='oui'  
  
chaque serveur peut être plusieurs choses : frontal, elastic ou encodage ('oui' ou 'non')  
le rabbitmq est forcément installé sur 1 frontal  
la bdd est sur le frontal dans l'exemple (d'où le db_host à 127.0.0.1) mais ça pourrait être sur un autre serveur sans soucis  
là où j'ai mis des IP (1.1.1.1 ou 2.2.2.2) faut bien mettre des IP sinon ça ne fonctionne pas avec des noms DNS dans la conf de certains services.  
