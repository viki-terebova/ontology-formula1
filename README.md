# Formula 1 Ontology

## Overview
- Base IRI: `http://example.org/formula1`
- Prefix used in files: `f1` (e.g., `f1:Season`, `f1:hasRound`)
- Entry point: `f1.owl` (imports all core modules)
- Scope: F1 entities (people, teams, vehicles), events (seasons, rounds, sessions), competition outcomes, and sample data (countries, circuits, constructors, seasons, standings)

## Ontology modules and files
- `f1.owl`: top-level ontology; imports all domain modules and adds global restrictions.
- `f1-core.owl`: core classes and top-level taxonomy for people, organizations, locations, events, assets, characteristics.
- `f1-events.owl`: events and sessions; weather and flag status classes.
- `f1-competition.owl`: competition outcomes, championships, race details, penalties, finish statuses.
- `f1-vehicle.owl`: cars, components, power unit parts, tyre compounds.
- `f1-properties.owl`: object and datatype properties (domains/ranges).
- `f1-teams.owl`: team/entry module (imports only).
- `f1-individuals.owl`: imports for data modules (countries, circuits, constructors, seasons).
- `f1db-countries.owl`: country individuals.
- `f1db-circuits.owl`: circuit individuals and metadata (location, length, etc.).
- `f1db-constructors.owl`: constructor individuals and stats.
- `f1db-seasons.owl`: seasons, team entries, and driver assignments.
- `f1db-results-standings.owl`: standings rows for a season.
- `catalog.xml`, `catalog-v001.xml`: OWL catalog mappings for local resolution.

## Class hierarchy (subClassOf)
Top-level disjoint classes (from `f1-core.owl`): `Person`, `Organization`, `Location`, `CompetitionAsset`, `EventThing`, `Characteristics`.

### People and organizations
- `Organization`
  - `Team`
    - `Constructor`
  - `GoverningBody`
  - `Supplier`
    - `TyreSupplier`
    - `FuelSupplier`
    - `PowerUnitSupplier`
  - `TyreManufacturer`
- `Person`
  - `Driver`
    - `MainDriver`
    - `ReserveDriver`
    - `TestDriver`
  - `TeamPrincipal`
  - `RaceEngineer`
  - `Mechanic`
  - `Steward`
  - `RaceDirector`

### Events and competition
- `EventThing`
  - `CompetitionThing`
    - `Championship`
      - `DriversChampionship`
      - `ConstructorsChampionship`
    - `PointsSystem`
    - `Regulation`
    - `Constraint`
  - `TeamEntry`
    - `SeasonEntry`
  - `Season`
  - `Round`
  - `GrandPrix`
    - `GrandPrixEvent`
  - `Session`
    - `PracticeSession`
      - `FP1`, `FP2`, `FP3`
    - `QualifyingSession`
    - `QualifyingSegment`
      - `Q1`, `Q2`, `Q3`
    - `SprintSession`
    - `SprintShootoutSession`
    - `RaceSession`
  - `Participation`
  - `Penalty`
  - `OutcomeThing`
    - `Result`
    - `Standing`
    - `StandingRow`
  - `RaceDetailThing`
    - `Lap`
    - `PitStop`
    - `TyreStint`
  - `Incident`

### Assets and vehicle
- `CompetitionAsset`
  - `Car`
  - `Component`
    - `TyreSet`
    - `Brakes`
    - `Suspension`
    - `PowerUnit`
    - `Chassis`
    - `Gearbox`
    - `AeroPackage`
    - `PowerUnitPart`
      - `EnergyRecoverySystem`
      - `InternalCombustionEngine`
      - `Turbo`

### Locations and characteristics
- `Location`
  - `Country`
  - `Circuit`
- `Characteristics`
  - `WeatherCondition`
    - `DryWeather`, `WetWeather`
  - `FlagStatus`
    - `GreenFlag`, `YellowFlag`, `RedFlag`, `BlueFlag`, `BlackFlag`, `BlackAndWhiteFlag`
  - `FinishStatus`
    - `Finished`, `DNF`, `DNS`, `DSQ`
  - `TyreCompound`
    - `SoftCompound`, `MediumCompound`, `HardCompound`, `IntermediateCompound`, `WetCompound`

## Object properties
`appliesToSeason`, `basedInCountry`, `builtByConstructor`, `carOfEntry`, `competesInSeason`, `compound`,
`defines`, `drivesForEntry`, `drivesForTeam`, `enteredBy`, `entryInSeason`, `hasChampionship`,
`hasChassis`, `hasCircuit`, `hasComponent`, `hasEntry`, `hasEvent`, `hasFinishStatus`, `hasFlagStatus`,
`hasGearbox`, `hasGrandPrix`, `hasIncident`, `hasMainDriver`, `hasNationality`, `hasPowerUnit`,
`hasPowerUnitPart`, `hasResult`, `hasRound`, `hasSession`, `hasStanding`, `hasStandingRow`,
`hasTestDriver`, `hasWeather`, `heldAtCircuit`, `hostsAtCircuit`, `inCar`, `incursPenalty`,
`involvesDriver`, `issuedInSession`, `issuedToDriver`, `lapByDriver`, `lapOfSession`,
`locatedInCountry`, `occurredInSession`, `partOfEvent`, `partOfRound`, `partOfSeason`,
`participatesInSeason`, `participationForEntry`, `participationInSession`, `participationOfDriver`,
`pitStopByDriver`, `pitStopForEntry`, `pitStopLap`, `puManufacturer`, `resultForDriver`,
`resultForEntry`, `resultOfSession`, `rowForDriver`, `rowForEntry`, `sessionOfEvent`,
`standingAfterRound`, `standingOfChampionship`, `stintByDriver`, `usedTyreManufacturer`,
`usedTyreSet`, `usesTyreCompound`

## Datatype properties
`bestChampionshipPosition`, `bestRaceResult`, `bestStartingGridPosition`, `carNumber`, `chassisCode`,
`circuitType`, `classificationStatus`, `constructorFullName`, `constructorName`, `eventEndDate`,
`eventStartDate`, `fastestLapRank`, `fastestLapTime`, `gridPosition`, `incidentType`, `lapNumber`,
`lapTime`, `latitude`, `lengthKm`, `longitude`, `penaltyReason`, `penaltyType`, `pitStopTime`,
`placeName`, `podiumsCount`, `points`, `pointsForPosition`, `position`, `puSpec`, `rank`,
`regulationYear`, `roundNumber`, `sessionDate`, `sessionStartTime`, `sessionTime`, `sessionType`,
`shortName`, `stintEndLap`, `stintStartLap`, `timeGap`, `total1And2Finishes`,
`totalChampionshipPoints`, `totalChampionshipWins`, `totalFastestLaps`, `totalPodiumRaces`,
`totalPodiums`, `totalPoints`, `totalPolePositions`, `totalRaceEntries`, `totalRaceLaps`,
`totalRaceStarts`, `totalRaceWins`, `totalRacesHeld`, `totalTime`, `turnCount`, `winsCount`, `worksFor`

## Key axioms and constraints
### Cardinality restrictions
- `TeamEntry` must have exactly 2 `MainDriver` via `hasMainDriver`.
- `Person` must have exactly 1 `Organization` via `worksFor`.
- `Season` must have at least 1 `Round` via `hasRound`.
- `Round` has at most 1 `Season` via `partOfSeason`.
- `Round` has at most 1 `EventThing` via `hasEvent`.
- `GrandPrixEvent` has at most 1 `Circuit` via `heldAtCircuit`.
- `GrandPrixEvent` has at least 1 `Session` via `hasSession`.
- `Session` has at most 1 `EventThing` via `partOfEvent`.
- `Result` has at most 1 `Driver` via `resultForDriver`.
- `Result` has at most 1 `Session` via `resultOfSession`.
- `Result` has at most 1 `SessionEntry` via `resultForEntry`.
- `Result` has at most 1 value each for `position`, `gridPosition`, `points`.

### Disjointness
- Core: `Person`, `Organization`, `Location`, `CompetitionAsset`, `EventThing`, `Characteristics`.
- Events: `PracticeSession`, `QualifyingSession`, `SprintSession`, `RaceSession`.
- Weather: `DryWeather`, `WetWeather`.
- Flags: `GreenFlag`, `RedFlag`, `YellowFlag`, `BlueFlag`, `BlackFlag`, `BlackAndWhiteFlag`.
- Vehicle components: `TyreSet`, `Brakes`, `Suspension`, `PowerUnit`, `Chassis`, `Gearbox`, `AeroPackage`.
- Tyre compounds: `SoftCompound`, `MediumCompound`, `HardCompound`, `IntermediateCompound`, `WetCompound`.
- Finish status: `Finished`, `DNF`, `DNS`, `DSQ`.

### Example assertions
- Circuits use `locatedInCountry`, `shortName`, `lengthKm`, `turnCount`.
- Constructors use `basedInCountry`, `constructorName`, `totalRaceWins`, `totalPoints`, etc.
- Season entries link to seasons (`entryInSeason`) and constructors (`enteredBy`).
- Drivers use `hasNationality`.
- Standings link to seasons (`partOfSeason`) and rows (`hasStandingRow`).

## Getting started (after clone)
Prereqs:
- Docker Desktop (includes Docker Compose)
- Python 3 (only if you want the optional static web UI)

Clone and enter the repo:
```
git clone <repo-url>
cd ontology-formula1
```

Set a Fuseki admin password (required by `docker-compose.yml`).
Option A: create a `.env` file in `f1-viewer`:
```
cd f1-viewer
echo FUSEKI_ADMIN_PASSWORD=change-me > .env
```

Option B: set an environment variable for your shell:
```
$env:FUSEKI_ADMIN_PASSWORD="change-me"
```

Start Fuseki:
```
cd f1-viewer
docker compose up -d
```

Access:
- Fuseki UI: http://localhost:3030/#/
- Fuseki base: http://localhost:3030/
- Dataset name: `formula1`
- SPARQL endpoint: http://localhost:3030/formula1/sparql
- Query endpoint: http://localhost:3030/formula1/query
- Update endpoint: http://localhost:3030/formula1/update

Optional: serve the static web UI.

From `f1-viewer/web`:
```
python -m http.server 8000
```

Or from `f1-viewer`:
```
python -m http.server 8000 --directory web
```

Open: http://localhost:8000/catalog.html

Stop:
```
cd f1-viewer
docker compose down
```