# Comment bloquer les crawlers sur apache2: 
### Crawler signifie littéralement « scanner ». Autrement dit, il s’agit d’extraire un maximum d’informations possibles d’un site web. Cette analyse permet ainsi de connaître parfaitement la structure d’un site et de résoudre ses problèmes éventuels. Par exemple, une arborescence mal construite, un maillage interne inadéquat ou encore des balises meta dupliquées.
Les commandes à suivre pour bloquer les crawlers sur apache2 sont ci-dessous étapes par étapes

##### se connecter en tant que super utilisateur 
    su

##### ouvrir le doossier log Apache2 aprés avoir installer Apache2
    cd /var/log/apache2

##### créer un chifier pour bloquer les crawlers dans log Apache2
    nano bloque.sh

##### puis dans ce fichier on éxecute les commandes suivantes :
    #!/bin/sh

###### -pour prendre les erreurs '404' on a le commande : 
    sed -n '/404$/p'

###### -on utilise ce script pour bloquer les crawlers : 
    awk '($9 ~ /404/)' /var/log/apache2/access.log | awk '{print $9,$7}' | sort | sed -n '/404$/p'|\ awk '{print $1} |tail -f |iptables -A INPUT -s $1 -j DROP  ;
###### -enfin pour bloquer les utilisateurs on éxecute : 
    crontab -r 

##### pour exécuter à la fin le fichier bloque.sh :
    ./blocking.sh