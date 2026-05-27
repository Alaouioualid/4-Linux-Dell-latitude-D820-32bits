# Dell-latitude-D820-
## Installation de Debian 11 sur un Dell Latitude D820 (32 bits)

Pour ce projet, j’ai utilisé un vieux Dell Latitude D820 en 32 bits avec seulement 2GB de RAM.
Le premier problème, c’est qu’il n’avait même plus de disque dur. En plus de ça, j’avais jeté le caddie HDD sans faire exprès quelque temps avant.

Au début, je voulais simplement récupérer des données depuis un ancien disque dur 3.5" de 80GB provenant d’une vieille tour fixe que j'avais acheter il y  a très longtemps. J’ai donc acheté un adaptateur SATA 2.5"/3.5". Mon idée était de récupérer les fichiers, nettoyer le disque puis l’utiliser temporairement comme stockage externe avant d’acheter un vrai HDD 2.5" avec son caddie adapté au Dell.

Le problème, c’est que le caddie coûtait plus cher qu’un adaptateur qui remplace le lecteur CD. J’ai donc choisi cette solution. Finalement, cet adaptateur ne me servira pratiquement à rien par la suite.

Quand j’ai branché le HDD 3.5", je me suis vite rendu compte qu’il était dans un très mauvais état. Le disque était extrêmement instable : certains fichiers étaient récupérables, d’autres non. J’ai réussi à sauver quelques données importantes avant de tout supprimer complètement pour repartir sur quelque chose de propre.

Une fois cette étape terminée, je suis passé à la création de la clé USB bootable pour installer Debian 11 en 32 bits (i386).

C’est là que les vrais problèmes ont commencé.

Déjà, Rufus refusait de se lancer correctement sur mon HP.
Balena Etcher ne fonctionnait pas non plus.
Comme j’avais déjà installé Debian sur un autre PC auparavant, j’ai décidé de tout faire directement via le terminal Linux.

Après quelques recherches, j’ai choisi Debian 11 i386 car :

- le Dell D820 est limité au 32 bits
- mes autres machines tournent déjà sous Debian
- Debian reste légère et très stable pour ce type de vieux matériel.

J’ai donc téléchargé l’ISO puis utilisé la commande dd pour rendre la clé USB bootable.
En théorie, cette méthode fonctionne très bien. Mais dans mon cas, le BIOS du Dell était tellement ancien qu’il ne détectait pas correctement la clé USB ou affichait directement :
No boot sector.

J’ai ensuite tenté une méthode plus avancée avec Syslinux :

- formatage de la clé en FAT32
- création d’une table de partition MBR
- installation de Syslinux
- copie manuelle des fichiers Debian.

L’objectif était de rendre la clé compatible avec un ancien BIOS Legacy. Malgré ça, impossible d’obtenir un boot stable.

J’ai aussi testé UNetbootin ainsi que plusieurs formats et configurations différentes, mais le résultat restait toujours le même.
Le problème ne venait pas de la clé USB : c’était simplement le BIOS du Dell qui était trop vieux.

Plusieurs personnes m’ont conseillé de passer directement par un CD/DVD, car sur ce genre de machine c’est souvent la solution la plus fiable. Malheureusement, je n’avais aucun CD disponible à ce moment-là. J’ai donc essayé de trouver une autre méthode.

C’est là que j’ai eu l’idée d’utiliser un SSD M.2 de 128GB avec un adaptateur USB.

Au début, je pensais que ça ne fonctionnerait jamais, surtout que même ChatGPT me disait qu’un SSD M.2 moderne pouvait poser problème sur un ordinateur aussi ancien.

J’ai d’abord branché le SSD directement sur le Dell pour tester.
À ma surprise, le PC arrivait à démarrer dessus. Un message d’erreur apparaissait ensuite en disant que le processeur ne supportait pas le 64 bits. C’était normal, car le SSD contenait volontairement un ancien Windows 10 64 bits uniquement pour vérifier si le BIOS arrivait au moins à lire le disque.

Voyant que le SSD était détecté, j’ai alors branché celui-ci sur mon HP afin de préparer correctement Debian dessus.

Depuis mon HP, j’ai :

- supprimé complètement Windows
- créé une nouvelle partition
- formaté le SSD en ext4
- installé GRUB.

Ensuite, j’ai monté l’ISO Debian puis copié tous les fichiers directement sur le SSD.
J’ai aussi copié l’ISO elle-même, car Debian en avait besoin pendant l’installation.

Une fois toutes les opérations terminées, j’ai remis le SSD dans le Dell Latitude.

Le PC a alors démarré directement sur GRUB, puis Debian a commencé à se lancer.

Au début, l’installation ne trouvait pas correctement l’ISO Debian. Après plusieurs tentatives ratées, j’ai eu l’idée de brancher en même temps la clé USB et le SSD avant de relancer le PC.

Et contre toute attente… ça a fonctionné.

## Résultat final

Après toutes les tentatives et les différents problèmes rencontrés, j’ai finalement réussi à installer Debian 11 en 32 bits avec l’environnement graphique LXDE.

J’ai choisi LXDE car c’est un environnement très léger, parfaitement adapté à une machine ancienne avec seulement 2GB de RAM. L’objectif n’était pas d’avoir quelque chose de moderne visuellement, mais plutôt un système stable, rapide et utilisable au quotidien.

Au final, le Dell Latitude D820 fonctionne étonnamment bien malgré son âge.
Le système démarre correctement, la navigation dans les menus reste fluide et les tâches basiques fonctionnent sans problème.

Ce projet m’a surtout permis de mieux comprendre :

- le fonctionnement du boot Linux sur un ancien BIOS
- les limites du matériel 32 bits
- la création manuelle de supports bootables
- l’installation de GRUB
- et les différentes méthodes possibles pour installer Linux sur une machine ancienne.

Même si l’installation a demandé énormément de tests et plusieurs heures de recherche, le résultat final reste très satisfaisant pour une machine aussi vieille.

## Conclusion

Ce projet m’a permis de mieux comprendre plusieurs points importants autour de l’installation de Linux sur du vieux matériel :

- les limitations des anciens BIOS
- les différences entre plusieurs méthodes de création de supports bootables
- le fonctionnement du boot Linux en mode Legacy
- surtout l’importance d’adapter sa méthode en fonction du matériel disponible.

J’ai également appris qu’une installation Linux ne se résume pas uniquement à “mettre une ISO sur une clé USB”. Sur des machines anciennes, chaque détail peut devenir un problème : le BIOS, le type de partition, le bootloader ou même le support utilisé.

Malgré toutes les difficultés rencontrées, j’ai finalement réussi à transformer un vieux Dell Latitude D820 en une machine Linux totalement fonctionnelle et fluide sous Debian 11 avec LXDE.

Ce projet m’a aussi permis de développer ma logique de recherche, ma patience et ma capacité à trouver des solutions alternatives lorsque les méthodes classiques ne fonctionnent pas.



https://github.com/user-attachments/assets/1a756248-efdd-4de1-ab57-4aecee876e91

