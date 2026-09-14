## Competency Questions

DEO can be used for answering several questions related to rethorical elements used in documents.
In the following subsections, some of them are introduced together with their respective SPARQL queries. 

The prefixes that are used in all the SPARQL queries provided below are defined as follows:

    PREFIX deo: <http://purl.org/spar/deo/>
    PREFIX cito: <http://purl.org/spar/cito/>
    PREFIX c4o: <http://purl.org/spar/c4o/>
    PREFIX doco: <http://purl.org/spar/doco/>
    PREFIX dcterms: <http://purl.org/dc/terms/>

### CQ1

What are the structural sections of a paper and their specific discourse roles?

    SELECT ?paper ?section ?title ?role
    WHERE {
        ?paper dcterms:hasPart ?section .
        ?section a doco:Section, ?role .
        FILTER(?role != doco:Section)
        OPTIONAL { ?section dcterms:title ?title . }
    }

### CQ2

Which internal discourse models or components extend external works?

    SELECT ?element ?citedWork ?content
    WHERE {
        ?element a deo:Model ;
            cito:extends ?citedWork .
        OPTIONAL { ?element c4o:hasContent ?content . }
    }

### CQ3

What is the future work outlined in the conclusion of a document?

    SELECT ?conclusionSection ?futureWorkElement ?futureWorkContent
    WHERE {
    ?conclusionSection a deo:Conclusion ;
        dcterms:hasPart ?futureWorkElement .
    ?futureWorkElement a deo:FutureWork ;
        c4o:hasContent ?futureWorkContent .
    }