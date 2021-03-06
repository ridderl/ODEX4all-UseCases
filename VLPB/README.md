# Tomato [SGN](https://solgenomics.net/) Linked Data deployment

**1. Build a [Docker](https://www.docker.com/) container with [Virtuoso Universal Server](http://virtuoso.openlinksw.com/) (open source edition).**

```
cd src
docker build -t vos .
```

**2. Start the Virtuoso server.**

`docker run --name vlpb -v $PWD:/tmp/share -p 8890:8890 -d vos`

**3. Prepare & ingest RDF data.**

```
tar xvzf ../data/sgn-ld.tar.gz -C ../data
mv ../data/rdf/* .
docker exec vlpb make all # check virtuoso.log for potential errors
```
(other `make` rules: `install-pkgs`, `import-rdf`, `update-rdf`, `post-install`, `clean`)
 
**4. [Login](http://localhost:8890/conductor) to running Virtuoso instance for admin tasks.**

Use `dba` for both account name and password.

**5. Run queries via Virtuoso [SPARQL endpoint](http://localhost:8890/sparql) or browse data via [Faceted Browser](http://localhost:8890/fct/) (no login required).**

RDF graphs:IRIs (_A-Box_)
  * SGN:
    * `http://solgenomics.net/genome/Solanum_lycopersicum`
    * `http://solgenomics.net/genome/Solanum_pennellii`
  * Ensembl: `http://plants.ensembl.org/Solanum_lycopersicum`
  * UniProt: `http://www.uniprot.org/proteomes/Solanum_lycopersicum`
  * QTLs: `http://europepmc.org/articles`

RDF graphs:IRIs (_T-Box_)
  * FALDO: `http://biohackathon.org/resource/faldo.rdf`
  * SO[FA]: `http://purl.obolibrary.org/obo/so.owl`
  * SIO: `http://semanticscience.org/ontology/sio.owl`
  * RO: `http://purl.obolibrary.org/obo/ro.owl`
  * GO: `http://purl.obolibrary.org/obo/go.owl`
  * UniProt Core: `http://purl.uniprot.org/core/`
  * PO: `http://purl.obolibrary.org/obo/po.owl`
  * TO: `http://purl.obolibrary.org/obo/to.owl`
  * SPTO: `http://purl.bioontology.org/ontology/SPTO`
  * PATO: `http://purl.obolibrary.org/obo/pato.owl`

For further details visit the [wiki](https://github.com/DTL-FAIRData/ODEX4all-UseCases/wiki/VLPB) page.
