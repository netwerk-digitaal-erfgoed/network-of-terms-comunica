Prototype: [Network of Terms](https://www.netwerkdigitaalerfgoed.nl/en/knowledge-services/usable-digital-heritage/network-of-terms/) and [Comunica](https://comunica.linkeddatafragments.org/)
==============================

This experimental application is published for examination and evaluation. It is not an official implementation.

## Build image

    docker-compose build --no-cache

## Logon to container

    docker-compose run --rm node /bin/bash

## List queryable dataset distributions

This command reads the catalog information in file `configs/catalog.ttl`.

    ./bin/run distributions:list

## Query one or more dataset distributions

```bash
# Cultuurhistorische Thesaurus: query SPARQL endpoint
./bin/run distributions:query --identifiers cht-sparql --search-terms fiets

# Cultuurhistorische Thesaurus: query (local) HDT file (slow)
./bin/run distributions:query --identifiers cht-hdt --search-terms fiets

# RKDartists: query SPARQL endpoint
./bin/run distributions:query --identifiers rkdartists-sparql --search-terms Gogh

# RKDartists: query TPF endpoint (slow)
./bin/run distributions:query --identifiers rkdartists-fragments --search-terms Gogh

# RKDartists: query (local) HDT file (slow)
./bin/run distributions:query --identifiers rkdartists-hdt --search-terms Gogh

# RKDartists: query SPARQL endpoint, TPF endpoint and HDT file simultaneously (slow)
./bin/run distributions:query --identifiers rkdartists-sparql,rkdartists-fragments,rkdartists-hdt --search-terms Gogh

# DBpedia: query TPF endpoint (slow)
./bin/run distributions:query --identifiers dbpedia-astronomers-fragments --search-terms Anton

# NTA: query SPARQL endpoint
./bin/run distributions:query --identifiers nta-sparql --search-terms Wieringa
./bin/run distributions:query --identifiers nta-sparql --search-terms "'Wier*'"
./bin/run distributions:query --identifiers nta-sparql --search-terms "Wieringa OR Mulisch"
./bin/run distributions:query --identifiers nta-sparql --search-terms "Jan AND Vries"

# NMvW: query SPARQL endpoint
./bin/run distributions:query --identifiers nmvw-sparql --search-terms eiland

# AAT: query SPARQL endpoint
./bin/run distributions:query --identifiers aat-sparql --search-terms schilderij
./bin/run distributions:query --identifiers aat-sparql --search-terms "schil*"
./bin/run distributions:query --identifiers aat-sparql --search-terms "schilderij OR tekening"
./bin/run distributions:query --identifiers aat-sparql --search-terms "cartoon* AND prent*"

# Wikidata Entities: query SPARQL endpoint
./bin/run distributions:query --identifiers wikidata-entities-sparql --search-terms Rembrandt
```

Add `--loglevel` to the commands to see what's going on underneath. For example:

    ./bin/run distributions:query --identifiers cht-sparql --search-terms fiets --loglevel info

Search results - in Turtle - are piped to stdout. Redirect these elsewhere for further analysis. For example:

    ./bin/run distributions:query --identifiers cht-sparql --search-terms fiets > cht.ttl

## Use Comunica directly

```bash
npx comunica-sparql \
    sparql@https://api.data.netwerkdigitaalerfgoed.nl/datasets/rkd/rkdartists/services/rkdartists/sparql \
    -q "SELECT * WHERE { ?uri schema:name ?label . ?label <bif:contains> 'gogh' } LIMIT 10"
```
