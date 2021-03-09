# UniRPG-Bot

Dieser Bot soll eine Engine für textbasiere mmo-Rollenspiele auf discord sein. Dabei soll den World buildern und admins möglichst viel Arbeit abgenommen werden und möglichst viel der Assets soll generiert werden um Urheberrechtsprobleme zu vermeiden.

## Geplante Features

Zuerst möchte ich alle Features kurz nennen und danach erklären, was ich damit meine. Dabei werde ich in Beispielen Charakternamen verwenden, die ich mir ausgedacht habe.

1. Charaktererstellung durch beschreibung
2. Automatisches generieren von Karten und Beschreibungen basierend auf dem Charakter
3. "Standalone"-NPCs
4. Metagaming schutz by design
5. Multi server support
6. Automatische chronik
7. Scenarios
8. Makros
9. Scripts
10. Dynaisches Questsystem
11. Ingame Welt Dokumentation
12. Multi Charakter support
13. Clan/Gilden support
14. Handwerkssystem
15. Dynamische Städte
16. Raids

### Charaktererstellung durch beschreibung

Man soll auf Wunsch entweder einen geführten Dialog mit dem Bot in den PMs haben, wo man die Werte eines Charakters direkt eingibt, oder eine Beschreibung des Charakters an den Bot senden damit dieser die Werte und Eigenschaften passend zu der Beschreibung bestimmt.  
Bestenfalls soll der Bot nachfragen, oder Man kann die Beschreibung bearbeiten, wenn das ergebnis dem Spieler nicht gefällt.

### Automatisches generieren von Karten und Beschreibungen basierend auf dem Charakter

Der bot hat eine für ihn lesbare Beschreibung der Karte und der Welt und generiert automaisch Beschreibungstexte oder Kartenbilder für den aktuellen Charakter. Dabei werden die Werte und das Wissen des Charakters automatisch mit einbezogen.

Sollte ein Charakter zum Beispiel sehr scharfe Sinne haben, wird er natürlich viel mehr Details wahrnehmen ohne sich direkt auf etwas konzentrieren zu müssen. Der Bot soll dabei wenn angemessen automatisch erklärungen aus der Lore einfließen lassen.

### "Standalone"-NPCs

Jeder NPC soll einen eigenen Agenten bekommen und begrenzt eigenständig entscheiden oder handeln können ohne dass viel gescriptet werden muss. Allerdings wird es wahrscheinlich auch Agenten geben, die zum Beispiel ein ganzes Dorf darstellt, damit nicht unendlich viele Agenten erstellt werden müssen.

Als Beispiel könnte man jetzt einen fahrenden Händler nehmen, der der eine Route von Dorf zu Dorf reist und mit den Dorfbewohnern handel treibt. Wenn er dabei einen Spieler trifft, kann dieser mit ihm handeln und Items verkaufen. Items die nicht zu den normalen Handelswaren des Händlers gehören verschwinden nicht, sondern werden vom NPC mindestens eine gewisse zeit weiter mitgeführt und zum Verkauf angeboten, bevor er sie in einer größeren Siedlung an einen anderen NPC verkauft, die dann wie eine Art sammelstelle funktionieren.

Sollte ein Server funktionen bei einem NPC benötigen, die nicht durch die Archetypen die der Bot mitbringt abgedeckt werden, soll man einfach einen Eigenen Agenten schreiben können, den man selbst hostet.

### Metagaming schutz by design

Der Bot soll so funktionieren, dass Metagaming von unerfahrenen Spielern so schwer wie möglich gemacht wird.  
Damit meine ich hauptsächlich, dass nur die Informationen offensichtlich sein sollen, die auch für den Charakter offensichtlich wären.

Als Beispiel nehme ich mal einen Spion:  
Ein Spion wird einer Fraktion - sagen wir der Einfachheit mal einem Clan - angehören und sich zum Schein einem anderen Clan anschließen. Gehen wir mal davon aus, dass die Zugehörigkeit eines Clans durch eine Rolle auf dem Server geregelt wird. Eine naive implementierung des Systems wäre, dass der User danach zwei Clan-Rollen besitzt und man beide sehen kann.  
Ein unerfahrener Spieler würde das sehen und relativ schnell drauf kommen, dass der Charakter ein Spion ist.

Um solche Vorkommnisse zu vermeiden soll es möglich sein Dinge zu versteken - auch wenn das relativ viel Verwaltungsaufwand im Hintergrund bedeutet.

### Multi server support

Es soll möglich sein mehrere Server mit der selben Welt zu betreiben und charktere begrenzt zwischen den Servern zu übertragen.

Als Beispiel könnte man annehmen es gibt einen Jugendfreien Server auf dem ausführliche beschreibung von Gewalt und anderen nicht jugendfreien Themen verboten ist und einen, wo das erlaubt ist.

Dann soll es möglich sein, dass man den selben Charakter auf beiden Servern spielt und eventuell nötige Anpassungen vom Bot automatisch vorgenommen werden dürfen - natürlich nur unter Bestätigung des Spielers.

### Automatische chronik

Der Bot soll eine Art "Log" von Ereignissen vorhalten, aus denen er eine Chronik schreiben kann. Bisher bin ich mir nicht sicher, ob es sinnvoll ist jedem Spieler zu erlauben eine eigene Chronik zu bekommen, die Geschehnisse aus seiner Sicht schildert, oder ob es nur eine Serverglobale geben soll.

### Scenarios

Es soll möglich sein größere Abläufe in ein Scenario zu verpacken und wartend als harmlose Questreihe irgendwo in der Welt zu platzieren. Wenn ein Spieler (oder eine Bestimmte Klasse/Rasse) die Quest annimmt wird das Scenario dann in Bewegung gesetzt. Alternativ soll das auslösen nach Zeit oder Datum auch möglich sein.

### Makros

Spieler sollen mehrere Bot-Befehle - welche sie fast immer in Kombination miteinander ausführen zu einem zusammenfassen können.  
Als Beispiel könnte ein Barbar folgendes Makro haben um den Kampf zu eröffnen:

```
.battle
  !enter combat
  !draw Mace
  !enter Rage
  !trigger storm
```

Der Barbar nimmt am Kampf teil, zieht seinen Streitkolben und versetzt sich in den Kampfrausch, bevor er ein Script auslöst dass automatisch den nächsten Gegner mit einem Sturmangriff attakiert.

### Scripts

Spieler sollen in der Lage sein eine Art script zu schreiben um den Charakter automatisch entscheidungen Fällen zu lassen. Am nützlichsten ist dieses Feature wahrscheinlich für support Klassen. Das wird ein Beispiel verdeutlichen:

Grace ist eine Schamanin, die als Heilerin spielt. Wenn sie auf einem Raid immer den Tank mit den wenigsten Lebenspunkten zuerst heilen wollte, bevor sie die anderen heilt, müsste sie zuerst für jeden Tank die Lebenspunkte abfragen, den mit den wenigsten suchen und auf ihn einen Heilgeist beschwören. Wenn gerade alle Tanks ausreichend Leben haben, müsste sie für alle anderen Mitglieder der Gruppe die Lebenspunkte abfragen und aus einer langen Liste den mit den geringsten heraussuchen, bevor sie ihren Heilzauber absetzt.

Im besten Fall braucht sie also zwei Befehle und im Schlechtesten braucht sie vier. Ich persönlich fände das Spielen ohne solche scripte relativ anstrengend und langsam, weswegen ich zumindest für die, die genauso denken gerne eine möglichekeit zur automatisierung bereitstellen würde.

### Dynaisches Questsystem

Ich finde nicht nur NPCs sollten Quests vergeben können. Am besten fände ich es, wenn theoretisch jeder - oder jeder mit einem Titel - eine Quest ausgeben könnte.

Deshalb möchte ich einen Dialog mit dem Bot haben um eine Quest zu erstellen, deren Abschluss sich automatisch prüfen lässt und wo automatische die Belohnung übergeben wird. Dazu passend wäre ein schwarzes Brett sinnvoll.  
Ein Beispiel:

Grace ist wieder eine Schamanin und braucht für ein Ritual unbedingt zutaten, die nicht ohne weiteres zu bekommen sind.  
Damit sie nicht ewig damit beschäftigt ist die Zutaten zu suchen, schreibt sie für jede Zutat oder Teiler von Zutaten quests aus und stellt diese aufs schwarze Brett.

Frank ist ein Botaniker und besitzt zufällig genug von einer Zutat, die er in seinem Garten anbaut um Grace zu helfen.  
Frank kann jetzt also die Quest annehmen 10 Kräuter zu beschaffen und Grace zu bringen. Dafür darf er bei dem Ritual zugegen sein und bekommt ebenfalls die Buffs des Rituals.

### Ingame Welt Dokumentation

Wenn man etwas über die Welt nicht weiß, beibt einem normalerweise nur im Wiki oder anderer externer Dokumentation zu suchen. Ich finde allerdings, dass das ein wenig die Imersion sprengt, weswegen ich eine ingame Dokumentation bauen möchte.

Man soll zu alltäglischen Themen NPCs befragen können und wenn man spezielleres Wissen sucht, soll man in eine Bibliothek gehen können um das Wissen aus einem Buch zu erfahren. Gegebenenfalls denke ich sollte es auch möglich sein über distanz mit einem Bibliothekar zu kommunizieren, der die information für den Spieler

### Multi Charakter support

Es soll möglich sein auf dem selben Server mehrere Charaktere zu spielen und zwischen ihnen zu wechseln. Dabei finde ich sollte es eine art cooldown geben, um zu verhindern dass Spieler absichlich mehrere Charaktere erstellen um einen Spion zu spielen, der nicht entdeckt werden kann. Hauptsächlich ist dieses Feature für Admins gedacht, die einen Charakter in ihrer Rolle als Spieler haben und einen in ihrer Rolle als Administrativer PC (Ich nenne die hier mal Herold).

### Clan/Gilden support

Ich möchte es den Spielern ermöglichen sich in einer Gruppe zusammenzuschließen und ihre eigene Hierachie aufzubauen. Dafür Wären Clans/Gilden ideal geeignet. Wichtig ist hier, dass Clans etwas dauerhafteres sein sollen und deswegen würde ich gerne Anforderungen an das erstellen eines Clans erheben.

Beispielsweise soll jeder Clan mindestens einen eigenen internen channel bekommen und eine eigene Rolle. Da für diese Operationen realtiv viele Anfragen an die discord Api notwendeig sind, möchte ich das erstellen eines solchen entweder an eine Gebür oder das Approval eines Herolds binden. Alternativ auch gerne beides.

### Handwerkssystem

Dass es möglich ist Gegenstände selbst herzustellen, oder zu reparieren ist in den meisten Spielen heute mehr oder weniger selbstverständlich.

Deshalb möchte ich ein Creafting system einführen, das die Eigenschaften des hergestellten oder reparierten Gegenstands selstständig nach Regeln ermittelt, damit es nicht notwendig ist unmengen an Items zu definieren. Ich würde vorschlagen, dass man für jede Klasse von Gegenständen nur die Grenzen ihrer Eigenschaften angegeben werden müssen.

### Dynamische Städte

Wahrscheinlich wollen Spieler Rückzugsorte, oder Hauptquartiere, oder Labore haben, weswegen es möglich sein sollte, dass Spieler Grundstücke in der Spielwelt "kaufen" und sich dort ein Haus bauen oder sich einfach Räume mieten können.

Ideal wäre, wenn es auch "unendliche Gebäude" gibt. Zur Verdeutlichung was ich meine hier ein Beispiel:

Es gibt eine Drachenbank, wo jeder Spieler ein kleineres oder größeres Verlies im Hort eines Drachen mieten kann um seine Schätze dort zu verwahren. Niemand ausßer dem Charakter oder einem Charakter, der von dem Charakter eingeladen wurde darf das Verlies betreten. Außerdem wird immer noch genau ein Verlies frei sein. Das verhindert das Aufkommen von dutzenden kleinen Banken die von Spielern betrieben werden.

### Raids

Ich denke zum Konzept von Raids muss ich nicht mehr viel erzählen. Das sollte hinreichend bekannt sein. Allerdings würde ich gerne ein Paar worte verlieren, wie die Organisation von Raids funktionieren soll.  
Dazu ein Beispiel:

"Hulk der Kleine" ist ein Barbar und möchte die "Gruft der Schreken" raiden. Er erstellt einen Raid, dem andere Spieler beitreten können. Er kennt "Grace" die Schamanin und sendet ihr eine Einladung. "Grace" akzeptiert und sendet eine Einladung an "Viktorius", der ein Paladin ist und viel Erfahung damit hat einen Raid zu koordinieren. Gleichzeitig hat "Hulk der Kleine" den Raid auf dem Schwarzen Brett geteilt und einige Krieger melden sich, die auch teilnehmen wollen.

"Viktorius" schreibt "Hulk der Kleine" an um zu bitten, dass er zum Strategen ernannt wird, damit er die Gruppe mit Spielern aus seinem Clan auffüllen kann.

Bevor es losgeht wird noch eine art Kommandostruktur festgelegt, die folgendermaßen aussieht:

```
Anführer: Hulk der Kleine
  Stratege: Viktorius
    Kommandant der Paladine: Theresia
    Kommandant der Barbaren: Herkules
    Kommandant der Krieger: Sagnix
    ...
```

Es wird sich darauf geeinigt, dass die gesammelte Beute gleichmäßig verteilt wird. Das Geld wird gerecht aufgeteilt, wobei jeweils die Anteile aller Spieler aus einem Clan zusammengelegt werden und sich der Clan intern einigen darf. Außerdem werden alle items, die eindeutig nur einem Spieler besondere Vorteile bringen automatisch an diesen Spieler verteilt.

Hier als beispiel sei "Grace" die einzige Schamanin und es wurde ein Geisterfokus gefunden, mit dem allein sie etwas anfangen kann, dann bekommt sie den automatisch.

Bei allen anderen Items könnte es verscheidene Verfahen geben um diese zu verteilen. Zufall oder claimen und abstimmen.

Nach dem die Beute veteilt ist, löst sich der Raid auf und alle können wieder ihrer Wege gehen.

## Gedanken zur Umsetzung

### Worker

Für Aufgaben, die potentiell eine längere zeit brauchen könnten ist wahrscheinlich das sinnvollste, dass irgendwie ein workerprozess im Bot gespawnt wird, der unabhängig vom eigentlichen Bot läuft und seine Aufgabe erfüllt.

### Agents

NPCs die eine besondere Funktion haben sollen, bekommen ein eigenständiges Programm, das man ungefähr mit einem Agenten in einem Multiagentensystem vergleichen kann. Es kann gegebenenfalls eigenständig Dinge tun und die Spielwelt wahrnehmen. Ich würde vorschlagen als einfach begreifbares Konzept verschachtelte Statemachines wie eine Art Entscheidungsbaum zu verwenden.

### Welt

Die Welt an sich soll aus Segmenten bestehen und ist wahrscheinlich am besten einem Weltmodell nachzuempfinden, wie es in der Robotertechnik verwendet wird.

Genauere Vorstellungen wie das aussehen könnte habe ich noch nicht, da mir auf diesem Gebiet bisher erfahrungen fehlen.

### Karte

Die Kart könnte ähnlich aufgebaut sein, wie man sie für ein Rougelike Spiel modellieren würde aus Räumen, die nur durch ihre Eckpunkte und Durchgänge beschrieben werden und entweder eine Liste fest platzierter Gegenstände besitzen, oder eine Liste an Gegenständen, die automatisch verteilt werden, wenn ein Charakter den Raum betritt. Natürlich geht auch eine Mischung aus beidem.

Wahrscheinlich ist es vorteilhaft für die Planung von Wegen die Verbindugnen zwischen Räumen als einen Graphen zu modellieren.

### Wissensbasis

Das Wissen aller NPCs oder direkt das ganze Wissen über die Welt ist wahrscheinlich am einfachsten über einen Graphen zu modellieren.
