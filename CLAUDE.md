# GleitenderMittelwert (RollingAverage) — Hinweise für die Arbeit an diesem Repository

## Rolle im NRG-Stack

**Hilfsmodul, kein Verbund-Vertrag.** Berechnet gleitende Mittelwerte
beliebiger Variablen ohne Archiv-Abhängigkeit (Live-Sampling in einen
versteckten JSON-Ringpuffer). Stabil im Store (1.7.1, `main`) — Änderungen
hier betreffen echte Store-Nutzer, entsprechend konservativ vorgehen.

## Referenz-Status im Verbund

Dieses Modul ist zweifache Muster-Referenz (siehe SUITE.md):

1. **`NRG.*`-Profil-Idempotenz**: `IPS_VariableProfileExists()` prüfen, nur
   bei Fehlen anlegen — wer zuerst startet, erzeugt es; kein Eigentümer-Modul.
2. **Klassische Variablenprofile** (Gegenstück zum Presentation-System):
   `NRG.*`-Scope-Klärung nennt dieses Modul ausdrücklich als Referenz.

## Technische Eckpunkte

- Ein Abtastintervall pro Instanz, Kanäle als Liste; je Kanal optional zweite
  Quelle (+/−-Verknüpfung, Invertieren) — erst verrechnen, dann mitteln.
- Methoden: arithmetisch, zeitgewichtet (robust gegen verpasste Ticks),
  Median. Alle arbeiten auf demselben Ringpuffer.
- Bewusst KEIN `AC_GetLoggedValues` — Unabhängigkeit vom Archiv ist ein
  Kernfeature, nicht als „Vereinfachung" wegrefactoren.

## Branch-Modell

Store-Modul mit `main` als Auslieferungsstand; `ems-integration` existiert
für Verbund-Anpassungen. Nutzersichtbares deutsch.

## Verbund-Manifest SUITE.md — Bezugsquelle (geändert 31.08.2026)

SUITE.md liegt seit 31.08.2026 NICHT mehr in einem GitHub-Repo (die
Modul-Repos sind öffentlich, SUITE.md enthält das komplette Architektur-/
Debugging-Know-how des Verbunds — Dietmars Entscheidung). Primärquelle ist
ausschließlich die lokale Datei `/Users/dietmar/Nextcloud/Claude/SUITE.md`
auf Dietmars Maschine, versioniert in einem eigenen lokalen Git-Repo ohne
Remote. Frühere Kopien dieses Dokuments wurden zusätzlich aus der Historie
aller Modul-Repos entfernt (`git filter-repo` + Force-Push). Kein
Fallback-Link mehr — ohne lokalen Zugriff auf Dietmars Maschine ist SUITE.md
nicht einsehbar.
