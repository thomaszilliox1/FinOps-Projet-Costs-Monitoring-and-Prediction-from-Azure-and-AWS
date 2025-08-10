# Projet FinOps Azure et AWS – Dashboard prédictif & intelligent  

## Objectif du projet  

Ce projet a pour but de fournir aux décideurs cloud un outil d’aide à la décision fondé sur les données réelles de consommation Azure. Il répond à 3 besoins essentiels :  

•	🔮 Prévoir les coûts sur les 3 prochains mois  
•	🚨 Détecter automatiquement des anomalies (hausses ou baisses inattendues)  
•	💡 Fournir des recommandations d’optimisation simples, basées sur des règles FinOps concrètes  


Le tout est intégré dans un dashboard Power BI interactif, lisible par des profils non techniques (DSI, FinOps, DevOps…).  
 
## Données utilisées  
•	Source : Export Azure Cost Management (CSV ou API)  
•	Colonnes principales :  

o	UsageDate (date de consommation)  
o	ServiceName (ex: VM, Storage, App Gateway…)  
o	CostUSD ou Cost  
o	ResourceGroup (si disponible)  
o	Tags (ex: environnement, équipe…)  
 
# Préparation des données  
Traitements réalisés :  

•	Mise en place d’une table de correspondance pour les valeurs de noms de service, afin d’associer les services provenant de Azure ainsi que de AWS aux mêmes catégories de famille basées sur la norme FOCUS  
•	Normalisation des dates (YYYY-MM-DD)  
•	Conversion des coûts en float  
•	Suppression des colonnes non-nécessaires pour le projet  
•	Ajout de colonnes dérivées :  
o	Pourcentage d’évolution d’un mois sur l’autre  
o	Classement des services par coût  

🔧 Outils : Power Query   
 
# Détection d’anomalies (approche statistique simple)  
Méthode utilisée :  

•	Calcul de la différence de coûts entre le mois actuel par rapport au mois précédent pour chaque service du cloud  

Exemple de règle :  
Si coût du mois actuel > coût du mois précédent multiplié par 2,5, alors anomalie  

Résultat : affichage dans Power BI sous forme de badge rouge ou graphe d’alerte.  
 
# Prédiction des coûts  

Option 1 – No-code (Power BI)   
•	Utilisation de la fonction native "Prévision" dans les graphes temporels.  
•	Activation via clic droit > "Ajouter prévision"  
•	Paramètres personnalisables : période, intervalle de confiance  

Option 2 – Python (modèle plus robuste)   
•	Librairie utilisée : Prophet  
•	Modèle entraîné sur les coûts agrégés par service ou par famille  
•	Réimport dans Power BI via fichier CSV ou base de données intermédiaire  

Avantage : meilleure précision, gestion des tendances longues et effets saisonniers.  
 
# Recommandations FinOps  

Méthodologie :  

Basée sur des règles métiers interprétables par les équipes opérationnelles.  

Exemples :  

Condition détectée	Recommandation  
VM > 500 €/mois sans tag "prod"	Recommander un shutdown ou resize  
Service avec coût en hausse de +100%	Proposer un audit de consommation  
Storage peu utilisé mais cher	Changement de SKU ou suppression  
 
# Structure du Dashboard Power BI  
 
🏠 Page 1	Vue d’ensemble des coûts (totaux, par service, par famille, par RG)  
📈 Page 2	Prédictions des coûts avec intervalles de confiance  
🚨 Page 3	Anomalies détectées (graphiques + tableaux dynamiques)  
💡 Page 4	Recommandations FinOps avec KPIs et alertes visuelles  
 
# Technologies utilisées  

•	Power BI Desktop (visualisation)  
•	Python (prétraitement, Prophet)  
•	Pandas / Numpy (manipulation)  
•	Prophet (Meta) (modèle de prédiction)  
•	Excel / CSV / API Azure (données brutes)  
 
✅ Prochaines évolutions possibles  

•	Connexion directe à l’API Azure Cost Management  
•	**Ajout d’un agent IA** FinOps pour répondre à des requêtes en langage naturel (via LangChain ou copilote Power BI)  
•	Intégration plus fine des tags FinOps pour filtrage avancé  
 
📌 Auteur  
Thomas Zilliox – Data Analyst / FinOps Explorer
Projet personnel de portfolio, réalisé en 2025 dans le cadre d’une préparation au conseil IA/Data chez Artefact.
 

<img width="470" height="644" alt="image" src="https://github.com/user-attachments/assets/b273a392-f50b-48d3-8a12-145c7b2d6021" />

