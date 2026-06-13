# Module 9 Week A Stretch: Board-Game Ontology

## Domain

This ontology models a small board-game catalog. I chose this domain because games have natural categories, creators, and mechanics, but the data can stay small enough to inspect by hand.

## Entity Types and Relationships

- `:BoardGame` is the general class for cataloged games.
- `:CooperativeGame` and `:CompetitiveGame` are subclasses of `:BoardGame`.
- `:Designer` represents a person who designed a game.
- `:Mechanic` represents a repeated gameplay pattern.
- Games connect to designers with `:designedBy`.
- Games connect to mechanics with `:usesMechanic`.
- Games store their supported range with `:playerCount`.
- `:hasSoloMode` is optional: only games that are known to support solo play include it.

## Modeling Decision

I modeled `:CooperativeGame` and `:CompetitiveGame` as subclasses instead of using a simple `:playStyle` string. That lets a SPARQL query ask for all `:BoardGame` instances with `rdfs:subClassOf*`, while still preserving the more specific category for each game.

## Required Features

The subclass hierarchy appears in `ontology.ttl` where `:CooperativeGame rdfs:subClassOf :BoardGame` and `:CompetitiveGame rdfs:subClassOf :BoardGame`. This enables subclass-aware queries that retrieve both cooperative and competitive games as board games.

SKOS labels appear on several resources. The clearest disambiguation examples are `:BoardGame`, which has `skos:prefLabel "Board game"` and `skos:altLabel "Tabletop game"`, and `:TheCrew`, which has the full preferred title plus the shorter alternate label `"The Crew"`.

The optional-style property is `:hasSoloMode`. `:Pandemic` includes it, while the other games omit it. This mirrors real catalog data where some facts are available for only part of the dataset.

## Sample Queries

The required SPARQL examples are in [queries.md](queries.md).
