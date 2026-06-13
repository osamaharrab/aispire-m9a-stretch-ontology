# Sample SPARQL Queries

## 1. Subclass-aware board-game query

This query finds every game whose direct class is `:BoardGame` or any subclass of `:BoardGame`.

```sparql
PREFIX : <https://example.org/aispire/boardgames#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>

SELECT ?game ?label ?gameClass
WHERE {
  ?game rdf:type ?gameClass ;
        skos:prefLabel ?label .
  ?gameClass rdfs:subClassOf* :BoardGame .
}
ORDER BY ?label
```

## 2. SKOS-disambiguated label search

This query matches a user search term against either the preferred label or an alternate label.

```sparql
PREFIX : <https://example.org/aispire/boardgames#>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>

SELECT ?resource ?matchedLabel
WHERE {
  VALUES ?searchTerm { "The Crew" }
  ?resource (skos:prefLabel|skos:altLabel) ?matchedLabel .
  FILTER(LCASE(STR(?matchedLabel)) = LCASE(?searchTerm))
}
```

## 3. Games grouped by mechanic

This query shows which games share the same mechanic.

```sparql
PREFIX : <https://example.org/aispire/boardgames#>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>

SELECT ?mechanicLabel ?gameLabel
WHERE {
  ?game :usesMechanic ?mechanic ;
        skos:prefLabel ?gameLabel .
  ?mechanic skos:prefLabel ?mechanicLabel .
}
ORDER BY ?mechanicLabel ?gameLabel
```
