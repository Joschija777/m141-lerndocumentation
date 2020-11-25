# Prepared-Statements 

## Was ist das?
Ein Prepared Statement ist eine sogenannte vorbereitete Anweisung für ein Datenbanksystem. Im Gegensatz zu gewöhnlichen Statements enthält es noch keine Parameterwerte. Stattdessen werden dem Datenbanksystem Platzhalter übergeben.

## Wofür braucht man das?
Der entscheidende Grund dafür, in Datenbankmanagementsystemen wie MySQL mit Prepared Statements zu arbeiten, ist der Aspekt Sicherheit. Das wohl größte Problem an standardmäßigen Zugriffen auf Datenbanken mit SQL-Sprachhintergrund ist nämlich die Tatsache, dass diese sich leicht manipulieren lassen. Man spricht in diesem Fall von einer SQL-Injection, bei der Code hinzugefügt oder angepasst wird, um an sensible Daten zu gelangen oder gar gänzlich die Kontrolle über das Datenbanksystem zu erlangen. 

