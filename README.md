# vitohack
Hier beschreibe ich meine Versuche, unserer Viessmann
Vitodens das furchtbare Takten auszutreiben.

Die Heizung startet bei Temperaturen über dem
Gefrierpunkt ca. alle 3-4 Minuten und schaltet
nach ca. 30 Sekunden wieder ab.

So kommen am Tag etwa 200 Startvorgänge zu Stande.
Das kann nicht gut für die Anlage sein und effizient
ist es mit Sicherheit auch nicht.

Ursache: Die Heizung startet mit 60% Brennerleistung
und fährt nach einpaar Sekunden auf 16% zurück. Allein
steigt in diesem kurzen Zeitraum die Kesseltemperatur
so stark an, dass die Heizung abschaltet. Dann erst
spült die Pumpe kälteres Wasser aus dem Kreislauf nach
und die Temperatur im Kessel fällt zügig ab. Nach 3-4
Minuten ist es dann so kalt, dass das ganze Spiel von 
vorn los geht.

Versuche, die Vorlauftemperatur abzusenken oder anzuheben,
sind ohne Erfolg.

Die Steuerung der Heizungssteuerung erkennt in der Startphase eine
hohe Kesseltemperatur und schaltet sofort ab. Laut sind 
dies wohl 8 K über Soll Vorlauftemperatur.

Meine Idee war daher:

Die optische Schnittstelle der Heizung nutzen, um da
irgendwie gegen zu steuern.

Gesagt, getan. Elemente sind:

* Ein D1 Mini (ESP8266)
* Einige Bauteile
* Die Bibliothek VitoWiFi

Und ein selbstcodierter endloser Zustandsautomat, der
den Brenner überwacht und gezielt die Soll-Raumtemperatur
manipuliert. 

So dreht der ESP nun beim Erkennen des Brennerstarts die 
Soll-RT für 1 Minute auf 37°C. Das "hilft" dem Brenner
über die starke Hitzeentwicklung beim Anfahren zu kommen.
Nach 1 Minute setzt er die Soll-RT wieder auf normal. Aktuell
hier 22 Grad. Der Brenner läuft nun je nach Abnahme gute 5-20
am Stück durch.

Geht der Brenner aus, wird die Soll-RT auf 18 Grad
gesetzt, damit der Brenner nicht zu früh wieder angeht.

Nach 25 Minuten wird die Soll-RT dann aber auf den normalen
Wert hochgesetzt, damit nicht alles zu lange auskühlt.

Bei ausreichender Abnahme geht der Brenner dann meist
sofort an. Ansonsten dauert es einige Zeit.

So startet der Brenner nur noch 2 mal pro Stunde und
nicht mehr 12-15 mal und läuft auch mal ein paar Minuten durch.

Details folgen...



