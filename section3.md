# Section 3 - Numérisation 

Cette section explore les bases de la numérisation des signaux, une étape clé dans les systèmes de communication modernes. Elle introduit tout d’abord les principes fondamentaux de l’échantillonnage, qui permettent de convertir un signal continu en une série d’échantillons discrets, garantissant ainsi une représentation fidèle selon le théorème de Nyquist-Shannon. Les applications pratiques de l’échantillonnage, notamment le calcul du débit maximal d’information et les modulations analogiques d’impulsions, y sont abordées.

Ensuite, la section s’intéresse à la modulation par impulsions codées (MIC), un processus crucial pour la transmission numérique des signaux. Les concepts de codage et de quantification sont détaillés pour expliquer comment les niveaux d’amplitude sont discrétisés en valeurs numériques.

Enfin, la section conclut par une étude du multiplexage temporel, une technique permettant de partager efficacement un canal de communication entre plusieurs utilisateurs. Les principes de base et le format des trames sont explorés pour illustrer son importance dans les systèmes à grande échelle.

Ensemble, ces notions établissent une base solide pour comprendre la numérisation et son rôle central dans les télécommunications modernes.

## Échantillonnage et quantification

La **numérisation** implique la transformation d'un signal du temps continu au temps discret (échantillonnage), puis en valeurs discrètes (quantification).


(def-)=
Définition: Échantillonnage  
: L’**échantillonnage** est la lecture d’un signal, $m(t)$ à intervalles réguliers, $T_E$ seconds. Donc on utilise une fréquence d'échantionnage de $f_E$ Hz. La problématique principale liée à l’échantillonnage **sans perdre d’information**.  Cela nous permet d'utiliser l'interpolation et de reconstituer le signal original. Nous représenterons le signal échantillonné comme $m_E(t)$ 

 
(def-quantification)=
Définition: Quantification
: La **quantification** est la lecture d'un signal  avec une précision finie. Une conséquence importante de ce processus est l'ajout du  bruit de quantification.

