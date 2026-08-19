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

## Verbund-Manifest SUITE.md — Bezugsquelle (19.08.2026)

Primärquelle für alle Verbund-Konventionen ist `SUITE.md` im EMS-Repo
(https://github.com/DG65/NRGEMS — während der EMS-Integrationsphase ist der
Branch `ems-integration` der aktuellste Stand, nicht `main`). In diesem Repo
liegt eine automatisch synchronisierte READ-ONLY-Kopie als `SUITE.md` im
Repo-Root — dort lokal grep'en/lesen. NIEMALS die Kopie hier editieren:
Änderungen gehören ins EMS-Repo; der Sync (GitHub Action `sync-suite` im
EMS-Repo) überschreibt lokale Änderungen kommentarlos.

Fallback, falls die Kopie (noch) fehlt oder veraltet wirkt:
https://raw.githubusercontent.com/DG65/NRGEMS/ems-integration/SUITE.md
