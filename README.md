## Roles Ansible pour déployer et mettre à jour POD v2 sur 1 ou plusieurs serveurs

### Créer son inventaire à partir de inventory.template.yml  
  
Dans la section [pod] rentrer le ou les serveurs selon le modèle suivant :  
  
[pod]  
**frontal1.domaine.fr** state=present frontal='oui' db_host='127.0.0.1' rabbit_host='localhost' allowed_long='frontal1.domaine.fr' allowed_short='frontal1'  encodage='non' elastic_host='elastic1' elastic_ip='2.2.2.2' elastic='non'  
**encode1.domaine.fr** state=present encodage='oui' frontal='non' elastic='non' db_host='1.1.1.1' rabbit_host='1.1.1.1' elastic_host='frontal1' elastic_ip='2.2.2.2'  
**elastic1.domaine.fr** state=present elastic='oui'  
  
Chaque serveur peut être plusieurs choses : frontal, elastic ou encodage ('oui' ou 'non')  

Le rabbitmq est forcément installé sur 1 frontal  

La bdd est sur le frontal dans l'exemple (d'où le db_host à 127.0.0.1) mais ça pourrait être sur un autre serveur sans soucis (le role ansible n'installe pas mysql et ne crée pas la base vide que le create_database.sh de pod rempli il faut que ça soit installer avant)  

Là où j'ai mis des IP (1.1.1.1 ou 2.2.2.2) faut bien mettre des IP sinon ça ne fonctionne pas avec des noms DNS dans la conf de certains services.  

Le createsuperuser est à faire à la main après depuis un frontal

**/!\  pour le repertoire media partagé entre le/les frontaux et le/les encodeurs il faut aller le faire à la main après /!\  
  
/!\ les scripts sont prévus pour fonctionner dans une infra qui accéde à internet avec un proxy, je n'ai pas encore rendu ce paramètre optionel faute de temps /!\**  

### Lancer une install :

/usr/local/bin/ansible-playbook  -i inventory.yml -e serveurs=pod pod_install.yml

### Lancer une update :

/usr/local/bin/ansible-playbook  -i inventory.yml -e serveurs=pod pod_update.yml
