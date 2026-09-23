```mermaid
usecase-beta
direction LR

actor Demandeur("Demandeur") <<abstrait>>
actor Client("Client")
actor Agent("Agent de voyage")
actor Recep("Réceptionniste")
actor Serveur("Serveur restaurant/bar")
actor Gerant("Gérant")
actor Temps("Temps") <<temps>>
actor Paiement("Service de paiement externe") <<système externe>>

systemBoundary SYS["Logiciel de gestion hôtelière"]
  UC_Dispo("Consulter les disponibilités")
  UC_Res("Réserver une chambre")
  UC_Arrhes("Verser des arrhes")
  UC_Annul("Annuler une réservation")
  UC_Remb("Rembourser selon le délai")
  UC_AutoAnnul("Annuler automatiquement les réservations non confirmées")
  UC_Arrivee("Enregistrer l'arrivée")
  UC_Conso("Enregistrer une consommation")
  UC_Fact("Facturer le départ")
  UC_Enc("Encaisser un paiement")
  UC_ListeArr("Éditer les arrivées prévues")
  UC_Taux("Consulter le taux d'occupation")
  UC_AdmHotel("Administrer hôtels et catégories")
  UC_AdmCh("Administrer chambres")
  UC_AdmTarif("Administrer tarifs")
end

Client --|> Demandeur
Agent --|> Demandeur

Demandeur --> UC_Dispo
Demandeur --> UC_Res
Demandeur --> UC_Annul

Recep --> UC_Arrivee
Recep --> UC_Conso
Recep --> UC_Fact
Recep --> UC_ListeArr
Serveur --> UC_Conso

Gerant --> UC_Taux
Gerant --> UC_AdmHotel
Gerant --> UC_AdmCh
Gerant --> UC_AdmTarif

Temps --> UC_AutoAnnul
Temps --> UC_ListeArr

UC_Enc -- Paiement
UC_Remb -- Paiement

UC_Res ..> : include UC_Dispo
UC_Arrhes ..> : extend UC_Res
UC_Arrhes ..> : include UC_Enc
UC_Fact ..> : include UC_Enc
UC_Remb ..> : extend UC_Annul
UC_AutoAnnul ..> : include UC_Remb

note for UC_Arrhes "Point d'extension : réservation faite plus de 8 jours avant l'arrivée"
note for UC_Remb "Uniquement si des arrhes ont été versées"

```
