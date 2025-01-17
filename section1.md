# Section 1 - Éléments d'un système de communication




Dans le domaine des télécommunications, la transmission efficace et
fiable des données est essentielle. Chaque système de communication vise
à transmettre des informations d'une source à une destination via
diverses étapes de traitement et un support physique. Comprendre ces
étapes et leurs rôles dans l'optimisation des performances est
fondamental pour concevoir des systèmes modernes. **ELE3701A - Éléments
de télécommunications**, explore ces concepts en profondeur. Cette
première section présente le contenu du cours et donne des définitions
étayées par des exemples pratiques.

Un système de communication établit le pont de communication entre
l'émetteur et le récepteur. Pour établir ce pont de communication entre
l'émetteur et le récepteur, il faut d'abord avoir un message à envoyer. Ce
message provient de la source d'information, et vise à être récupéré à
la destination. L'objectif de cette section est d'identifier  des éléments fondamentaux d'un lien de communication
    point à point  (**O1**).
Un système de communication se compose de cinq éléments
(sous-systèmes) fondamentaux :

1.  la source

2.  l'émetteur

3.  le multiplexeur

4.  le canal

5. le démultiplexeur

6.  le récepteur

7.  la destination

```{figure} images/system.png
:label: system1
:align: center
Éléments fondamentaux d'un modèle de système de communication point à point

```

Notez que chaque élément possède des signaux d'entrée et de sortie,
comme l'indique la figure. Chaque élément peut être considéré comme un
système distinct. Vous trouverez ci-dessous les explications détaillées
de chaque élément.

:::{warning} Attention
Dans les systèmes de communication, certains termes sont
utilisés pour exprimer des concepts différents en fonction du contexte
(comme le codage et la modulation). Il est important de faire les
distinctions en fonction de l'application particulière.
:::

### Source
(def-source)=
Définition: Source
: *En télécommunications, une source est l'origine des
signaux de message à transmettre, tels que des données numériques, de
la voix, des images ou des vidéos.*
: -   **entrée :** Aucune
: -   **sortie :** Signal de message

La nature de ces signaux détermine leur traitement initial. Le signal de
message à la sortie de la source peut être analogique ou numérique. Une
**source continue** (*continous source*) génère des signaux de messages
analogiques, c'est-à-dire que le signal à la sortie prend des valeurs
continues en amplitude et dans le temps. Une **source discrète**
(*discrete source*) génère des signaux numériques, qui prend des valeurs
continues en amplitude et est discrète dans le temps.



:::{important} Exemple pratique
* **Source continue** : La voix captée en temps réel par un micro-phone est un signal analogique.

* **Source discrète** : Cette voix, après échantillonnage et quantification, devient une suite de valeurs numériques discrètes (fichier WAV ou MP3).
:::

### Émetteur (*Transmitter*)
(def-tx)=
Définition: Émetteur
: *L'émetteur est un composant essentiel qui prépare les données de la source pour les transmettre via un canal. Selon la nature des signaux de message et le type de communication, un émetteur peut être classé en deux types principaux; **communications analogiques** et **communications numériques**.*
: -   **entrée :** Signal de message
: -   **sortie :** Signal émis

(def-tx-a)=
Définition: Émetteur pour communications analogiques
: *Un **émetteur pour communications analogiques** traite des signaux continus, 
tels que des signaux électriques, acoustiques ou lumineux, qui varient de manière continue dans le temps et l’amplitude. La fonction fondamentale est 
**modulation analogique**.
Avec modulations les signaux générés  par une source analogique (par exemple, un microphone) sont convertis en signaux modulés analogiques pour être transmis.*
: - **entrée :** Signal de message (analogique)
: - **sortie :** Signal émis (analogique)

(def-tx-d)=
Définition: Émetteur pour communications numériques
: *Un émetteur pour communications numériques traite des signaux discrets
où les données sont codées sous forme de bits (0 et 1). Ces bits sont
ensuite modifiés pour être adaptés à la transmission. Les fonctions sont
le **codage de source** (pour la compréhension), le **codage de canal**
(pour aider à récupérer les erreurs qui seront induites par le canal) et
la **modulation numérique** (pour aider à transférer les signaux sur de
longues distances).*
: - **entrée :** Signal de message (numérique)
: - **sortie :** Signal émis (numérique)

(def-source-coder)=
Définition: Codage de source
: *Le **codage de source** (*source coding*) est utilisé
pour compresser les données dans le plus petit nombre de bits. Elle
supprime les bits inutiles. L'objectif est d'utiliser un nombre réduit
de bits pour représenter le même message.*
: - **entrée :** Signal de message (numériques, binaires)
: - **sortie :** Signal de message compressé (numériques, binaires)
:::{warning} Attention
Au cours de notre discussion, l'entrée et la
sortie du codeur de source sont binaires.
:::

(def-channel-coder)=
Définition: Code de canal
: *Le **codage de canal** (*channel coding*) est utilisé
pour la détection ou la correction des erreurs de bit. Dans un codeur de
canal, nous ajoutons des bits au signal à transmettre. Ces bits sont les
bits de correction d'erreurs et sont inclus selon un code particulier
qui détermine ses règles de calcul. En utilisant ces bits
supplémentaires, le récepteur peut être en mesure de corriger l'erreur
de bit.* 
: - **entrée :** Signal de message (numériques, binaires)
: - **sortie :** Signal de message doté de parités (numériques, binaires)
:::{warning} Attention
Au cours de notre discussion, l'entrée et la
sortie de codeur de canal sont binaires.
:::

(def-mod-dig)=
Definition: Modulation numérique
: *Ensuite, les bits à la sortie du codeur de canal seront
modulés par le modulateur. Ce système est nommé **modulation
numérique** (digital modulation).* 

Ici, le signal à transmettre est modulé par **une onde
porteuse** (*carrier wave, a.k.a. carrier*). Une onde porteuse est
utilisée pour la transmission efficace de données sur de longues
distances. Les signaux cosinus sont utilisés comme ondes porteuses.
Les signaux cosinus sont
utilisés comme ondes porteuses. Les ondes cosinus et sinus sont des fonctions
propres de syst`èmes linéaires invariants dans le temps. Les messages peuvent
être inclus dans l’amplitude, la phase ou la fréquence de l’onde porteuse.

Si la source est discrète, nous pouvons directement utiliser un codeur
de source. Si la source génère des signaux analogiques, il faut utiliser
un **convertisseur analogique-numérique** (*Analog to digital
converter*; A/N) avant d'utiliser un codeur de source. 

Définition: Convertisseur analogique-numérique
: *Un A/N convertit un signal analogique continu en un signal numérique
discret, pour qu'il soit traité et transmis efficacement (exemple:
lorsqu'un son est enregistré pour un podcast, il est transformé en
signal numérique).*
: - **entrée :** Signal de message (analogique)
: - **sortie :** Signal de message (numérique)

:::{important} Exemple pratique
* Émetteur pour Communications Analogiques
  * Radio analogique (AM, FM).
  * Télévision analogique.
  * Téléphonie fixe classique (PSTN).

* Émetteur pour Communications Numériques:
  * Téléphonie mobile (4G, 5G).
  * Wi-Fi, Bluetooth.
  * Télévision numérique (DVB-T).
:::

### Multiplexeur (*Multiplexer*) 
Définition: Multiplexeur
: *Le **multiplexeur** (MUX) permet de combiner les signaux de
plusieurs utilisateurs en un seul signal pour une transmission efficace sur un
canal commun. Il joue un rôle crucial dans l’optimisation de l’utilisation des
ressources*
: - entrée : Signaux émis de plusieurs utilisateurs
: - sortie : Un seul signal émis (combiné)
:::{important} Exemple pratique
- Communications par fibre optique utilisant le multiplexage en
longueur d’onde (WDM; Wavelength Division Multiplexing).
- Les réseaux sans fil (Wi-Fi, 4G/5G) et les transmissions
numériques (DVB, DAB) utilisent multiplexage par division de
fréquence orthogonale (OFDM; Orthogonal Frequency Division
Multiplexing)
:::

### Canal (*Channel*)

Définition: Canal
: *Le **canal** (channel) est le support physique par lequel le signal est transmis entre l'émetteur et le récepteur. Il peut introduire du bruit et des distorsions affectant la qualité de la transmission.*
: - **entrée :** Signal émis
: - **sortie :** Signal reçu

:::{important} Exemple pratique
* Une fibre optique pour Internet haut débit (faible atténuation et capacité élevée).
* Les ondes radio pour les communications sans fil, comme le Wi-Fi ou les réseaux cellulaires.
:::

### Démultiplexeur
Définition: Démultiplexeur
: *Le **démultiplexeur** (DEMUX) sépare un signal combiné provenant
de plusieurs utilisateurs en plusieurs flux individuels. Il est utilisé en complément
du multiplexeur pour reconstituer les signaux d’origine une fois la transmission
terminée.*
: - **entrée :** Un seul signal reçu
: - **sortie :** Signaux reçus de plusieurs utilisateurs

### Récepteur (*Receiver*)

Définition: Récepteur
: *Le **récepteur** (receiver) récupère et traite le signal reçu pour
restaurer les informations originales. Il joue alors un rôle clé en
récupérant le signal, en corrigeant les erreurs et en reconstruisant les
messages originaux.*
: -   **entrée :** Signal reçu
: -   **sortie :** Signal de message estimé

Au récepteur, les fonctions d'émetteur sont répétées dans l'ordre
inverse. Il doit donc être configuré en fonction de l'émetteur
analogique ou numérique sélectionné. L'objectif est de reproduire le
plus correctement possible le signal du message à la destination (donc
nous voulons : Signal de message estimé $\approx$ Signal de message )



### Destination

Définition: Destination
: *La **destination** est le point final où les
informations sont utilisées. Cela peut être un utilisateur humain ou un
autre système.*

:::{important} Exemple pratique
* Une personne regardant une vidéo sur YouTube.
* Un serveur recevant un requête HTTP d'un navigateur Web.
:::

## Ressources de communication : Puissance (*Power*) et Largeur de Bande (*Bandwith*)

Dans les systèmes de communication, la **puissance** et la **largeur de
bande** sont deux **ressources fondamentales** nécessaires à la
transmission et à la réception des informations. Une gestion efficace de
ces ressources est essentielle pour garantir la fiabilité, la capacité
et la qualité des communications. Une utilisation efficace de la
puissance et de la largeur de bande permet de minimiser les pertes et de
réduire l'empreinte carbone pour une conception durable.

:::{hint} Attention
L'objectif du système de communication est de minimiser
les erreurs de transmission tout en minimisant l'utilisation des
ressources.
:::

### Puissance

Définition: Puissance
: *La **puissance** d'un signal est nécessaire pour
transmettre des signaux à travers un canal de communication. Elle est
cruciale pour surmonter l'atténuation, le bruit et d'autres dégradations
dans le canal.* 

Une puissance de transmission suffisante permet au
signal de se propager jusqu'au récepteur sans être complètement dégradé
par le bruit ou l'atténuation.

Une puissance plus élevée améliore le **rapport signal-bruit**
(*Signal-to-noise-ratio*; SNR), ce qui entraine une meilleure qualité du
signal et un taux d'erreurs réduit. En plus, une puissance accrue permet
aux systèmes de communication, comme les tours cellulaires ou les
satellites, de couvrir de plus grandes zones.

:::{important} Exemple pratique
* Dans les réseaux cellulaires, les stations de base nécessitent une puissance importante pour maintenir la connectivité avec les utilisateurs éloignés de l'antenne.
* Les satellites en orbite géostationnaire utilisent une forte puissance pour transmettre des signaux sur de longues distances jusqu'à la Terre, tout en surmontant les pertes atmosphériques.
* L’efficacité énergétique est cruciale pour les dispositifs alimentés par batterie, comme les capteurs, qui doivent transmettre des données sur de longues périodes sans recharge fréquente.
:::

:::{warning} Attention
 Une consommation de puissance élevée peut entrainer des
coûts opérationnels importants et un impact environnemental accru. De
plus, les appareils alimentés par batterie nécessitent une gestion
rigoureuse de l'énergie pour prolonger leur durée de vie.
:::

### Largeur de bande

Définition: Largeur de bande
: *La **largeur de bande** correspond à l'étendue des
fréquences disponibles pour la transmission d'un signal.*

Elle détermine le débit maximal que peut atteindre un système de
communication numérique. Une plus grande largeur de bande permet un
débit de données plus élevé. Une largeur de bande suffisante garantit
que le signal transmis n'est pas déformé ou limité par une allocation de
fréquence insuffisante.

:::{important} Exemple pratique
* Une largeur de bande accrue permet des transmissions de données rapides, soutenant des applications comme le streaming, la réalité virtuelle et les véhicules autonomes.
* Une grande largeur de bande est essentielle pour transmettre plusieurs chaines TV ou des services Internet à haut débit via satellite.
* Les systèmes téléphoniques PSTN allouent une largeur de bande d’environ 4 kHz pour assurer l'intelligibilité de la voix.
:::

:::{warning} Attention
 La largeur de bande est une ressource limitée et cout
élevé, et l'attribution du spectre doit équilibrer les besoins de
différents services (radio, télévision, mobile). Une demande accrue de
bande passante peut entrainer une congestion dans les bandes de
fréquences très utilisées.
:::

:::{warning} Attention
 Il y a un équilibre entre puissance et largeur de bande.
La puissance et la largeur de bande sont interconnectées dans les
systèmes de communication, et leur allocation nécessite des compromis.
Une augmentation de la puissance permet une transmission fiable avec une
largeur de bande réduite. Une augmentation de la largeur de bande réduit
la puissance nécessaire pour atteindre un débit de données spécifique.
:::

## Résumé

En résumé, les systèmes de communication modernes reposent sur des
éléments bien définis, allant de la source à la destination et protégés
par des mécanismes de correction des erreurs. Chacune de ces étapes est
essentielle pour assurer une communication efficace et fiable, malgré
les contraintes imposées par les caractéristiques physiques des canaux
et les besoins en ressources limitées. Ces bases permettent d'aborder
les défis plus complexes liés à la conception de réseaux et de systèmes
avancés.
