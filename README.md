# EN2FR-Translation
Triptych: Un Nouvel Algorythme Protégeant les Données des Utilisateurs de Monero

Monero est conçu pour obfusquer les valeurs (montants, sortants et intrants) de chaque transaction entre tout émetteur et tout récipendiaire, avec des techniques et des technologies évolutives.
Il s’agit de presenter ici Triptych (en Français Triptyche), une technologie innovante permettant l’optimisation de la fonction obfuscante de l’émetteur, celui de l’usage de la blockchain et une rapidité supérieure d’exécution de l’ordre.

Les Signature de cercles (RingCT)

Pour assurer la confidentialité des transactions émettrices, Monero fait plus que de garder le secret des adresses. L’ensemble de la base des données de Monero existe sur sa blockchain comme des émissions denommées TXO. Tout TXO est unique, et il lui est assigné une identité unique (ID), appellee clef publique (également nommée adresse de couverture). Par simple analyse de la blockchain de Monero, une corrélation entre les clefs publiques des TXO et les adresses des portefeuilles électroniques de Monero sont impossibles.
Cela étant, les clefs publiques aussi ont besoin d’une protection. Il serait inacceptable que les flux de Monero des clefs publiques soient transparents, considérant que des techniques externes à la blockchain pourraient associer ces clefs publiques à des personnes.

Les flux de Monero des clefs publiques sont gardées confidentielles par l’usage d’un procédé de chiffrage appele Transactions Confidentielles de Cercle (RingCT). De cette façon, la clef publique d’un TXO demeure dissimulée, en se fondant dans un groupe de transaction-leurres (également nommée mixins). L’observation d’une transaction ne pourra pas permettre de déterminer si le TXO est l’original ou non.
Vous pouvez voir un exemple d’émission ou de reception de TXO en allant à la recherche d’une transaction à l’aide d’un programme d’analyse de la blockchain de Monero tel que moneroblocks.info ou xmrchain.net.

La manière dont les transaction-leurres TXO sont selectionnées à partir de la blockchain s’est améliorée au fil du temps. Au tout debut, les transaction-leurres bien que faisant partie du système, restaient facultatives. Avec le temps, le nombre de transaction-leurres grandit et devint obligatoire, pour atteindre exactement 10 transaction-leurres par ordre d’exécution aujourd’hui. Au tout début, pour tout portefeuille de Monero, les leurres etaient sélectionnés uniformément pour toutes les transactions. Le procédé statistique de sélection fut afiné au fil du temps pour lui donner plus de complexité avec le tailor random process, un algorithme base sur le procédé de selection pour l’exécution de l’ordre d’après une théorie statistique de distribution gamma particulière, que nous utilisons encore à ce jour.
Les algos du core ring signatures (signatures de cercle) ont également été améliorés. La publication de proposition originelle de CryptoNote offrait un processus de signature de cercle différent de l’actuel, optimisé parce que bâtit sur l’utilisation des Multilayered Linkable Spontaneous Anonymous Group (MLSAG) signatures. Une améloriation substantielle, nommée Compact Linkable Spontaneous Anonymous Group (CLSAG) signatures, est attendue prochainement, et promet de réduire d’environ un quart, le poids des transactions et d’un dixième leur temps de confirmation (pour une transaction de deux intrants, deux sortants).
Toutes ces améliorations offrent à Monero un puissant potentiel d’anonymat. à chaque movement de Monero, tout TXO sortant prend la forme d’une clef publique TXO de couverture, sans lien cryptographique avec l’adresse d’émission, et melée à 10 autres clefs publiques-leurres, selectionnées pour leur vraissemblance. Cela rend toute surveillance extrêmement difficile, tout en assurant rapidité et fluidite d’exécution du logiciel de Monero, et offrant une blockchain de taille et de vitesse acceptable.

Les défis

Néanmoins, la technologie obfuscant l’émetteur n’est pas optimale. Dix transactions-leurres ne sont pas toujours suffisantes parce que certains TXO aléatoires pourraient être  identifiés. Ils auraient déja pu  servir à des transactions identifiées. L’existence de listes blackboulées pourrait poser probleme et offrir à des adversaires motivés, une arme potentielle en prenant l’initiative de les ajouter à la liste de leurs portefeuilles. Et il y a d’autres astuces pour identifier les leurres, en liant les TXO aux échanges ou aux pots communs de mineurs de Monero, en estimant leur usage dans d’autres transferts et en évaluant des probabilités statistiques temporelles.
Imaginons une cohorte de personnes au poste de police, composée d’un individu faussement accusé et de 10 policiers jouant les roles de suspects. En sachant que les policiers sont identifiables aux yeux d’un faux temoin, cette stratégie ne serait d’aucun recours à l’individu injustement accusé.  Il en va de même  pour les signature de cercles de Monero: la technique de se fondre dans la foule ne peut marcher que lorsque la foule est uniforme; et contre des adversaires, des adversaires très puissants, 10 leurres choisis au hasard peuvent-être  insuffisant. Dans ce cas, pourquoi ne pas en utiliser un peu plus?
Et bien, dans le cas des algos MLSAG/CLSAG utilisés par Monero, le temps de traitement de la transaction est proportionnel à sa taille, et les deux vont croissant de façon linéaire (dans le sens de grande complexité mathématique) en fonction du nombre de leurres utilisés. L’utilisation de dix leurres, permet un niveau de privauté acceptable, compensée par le besoin d’une blockchain plus petite permettant un traitement plus expéditif. Plus de leurres offriraient une meilleure couverture de privauté, mais augmenteraient également la taille de la blockchain de Monero –déjà par de nombreuses fois plus importante que pour Bitcoin- et empêtreraient les portefeuilles électroniques lors des mises à jour. 

Triptych

Triptych est là pour relever le défi, il s’agit d’un nouvel algorithme destiné aux signature de cercles, qui a été développé par Sarang Noether et Brandon Goodell des Laboratoires de Recherche de Monero (MRL) avec la participation de Arthur Blue (RandomRun). Avec Triptych, la taille de la signature de cercle croît de façon logarithmique plutot que linéaire. La croissance logarithmique est très lente, et présente un choix judicieux, qui permet d’eviter de faire confiance à des tierces parties (et par la, de défaire l’anonymat comme dans le cas de Zcash). Le temps de vérification des opérations continue de croître de façon linéaire avec le nombre de leurres dans Triptych, mais les vérifications peuvent-être regroupées et assorties à l’utilisation d’algorithmes spécifiques, permettant une réponse accélérée.
Triptych parvient à faire fi de plusieurs difficultés posées par l’usage des signature de cercles avec Monero. Il permet d’établir un lien. La technique des signature de cercles de Monero doit bloquer la réutilisation de clefs publiques légitimes de façon à prévenir le double usage d’un TXO. Triptych y parvient en utilisant des étiquettes de lien (linking tags), similaires aux images cryptographiques actuelles. Triptych permet également d’obfusquer les volumes d’échanges en Monero par l’utilisation des transactions confidentielles. Des données particulières répondant au nom de “clefs d’engagement” (commitment keys), permettent de valider toutes les opérations de mouvement de Monero sans dévoiler leurs montants. Ces clefs d’engagement, avec les clefs publiques, et les étiquettes de liens, sont les trois éléments qui donnent naissance au nom de Triptych, triptyche voulant dire formé de trois parties.

Tests et autres possibilités

Triptych est rapide en pratique. Un de ses créateurs, Sarang Noether, à signalé que le code d’essai donnait une amélioration d’exécution significative. En gros, l’utilisation de 63 leurres sous Tryptich, est 10% plus rapide que l’utilisation de 10 leurres avec CLSAG. Ces performances présentent une amélioration fondamentale pour Monero, également pratique à utiliser.

Il reste du travail à faire, cependant, une inspection rigoureuse d’un nouvel algorithme tel que Triptych est nécessaire avant son inclusion dans la base de code de Monero. Bien que la publication de l’algorithme de Triptych ait été soumise à l’appréciation de chercheurs pairs (et acceptée à être  présentée lors du séminaire ESORICS CBT 2020), Triptych pourrait encore bénéficier de modifications apportées à ses algorithmes et au code d’exécution de ces algorithmes, et sa rapidité d’exécution encore plus optimisée. Le temps consacré à l’amélioration de Triptych prend sur celui qui pourrait-être  utilisé à découvrir des solutions alternatives.
Une de ces alternatives –particulièrement prometteuse- se trouve être  une version plus pointue de Triptych, elle-même  appellee Arcturus, et developée par Sarang Noether. Arcturus reduit de plus la taille des transactions, utilisant le paquet de données d’une seule signature chiffrée pour toute une transaction au lieu de une pour chaque TXO. Artcurus et Triptych ont des temps de vérifications similaires. C’est la résultante de l’utilisation d’un algorithme dans Arcturus, nécessitant des hypothèses mathématiques qui ne sont pas nécessaires à Triptych.

Conclusion

Avec Triptych, et son complément Arcturus, Monero a une technologie formidable, offrant la possibilité d’empecher une croissance linéaire de la signature de cercle (et du nombre de leurres utilisés pour cacher l’émetteur) et la remplacer par une croissance logarithmique. Si il venait à être  adopté, cela permettrait l’augmentation du nombre de leurres sans inflation de la blockchain ou d’augmentation d’usage de CPU lors de la validation des opérations. La technologie de Triptych est une manifestation de l’esprit de Monero pour rendre possible et toujours mieux protéger la privauté et la liberté de ses utilisateurs.


