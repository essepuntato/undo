# Iteration 1: formal competency questions


## Question 1

What are all the documents that refer to the UN resolution A/RES/47/180 of 22 December 1992.

    PREFIX : <https://w3id.org/akn/data/undo/>
    PREFIX undo: <https://w3id.org/akn/ontology/undo/>
    
    SELECT DISTINCT ?document
    WHERE {
        ?document undo:mentions :a-res-47-180-1992-12-22 .
    }


## Question 2

What are all the entities referred by the UN resolution A/RES/50/100 of 2 February 1996?

    PREFIX : <https://w3id.org/akn/data/undo/>
    PREFIX undo: <https://w3id.org/akn/ontology/undo/>
    PREFIX owl: <http://www.w3.org/2002/07/owl#>
    
    SELECT DISTINCT ?entity ?type
    WHERE {
        :a-res-50-100-1996-02-02 undo:mentions ?entity .
        ?entity a ?type .
        FILTER (?type != owl:NamedIndividual)
    }


## Question 3

What are the documents that describes the General Assembly recalling the resolution A/RES/47/180 of 22 December 1992?

    PREFIX : <https://w3id.org/akn/data/undo/>
    PREFIX undo: <https://w3id.org/akn/ontology/undo/>
    
    SELECT DISTINCT ?document
    WHERE {
        ?rel a undo:Relation ;
            undo:hasProponent :general-assembly ;
            undo:hasSemantics :recall ;
            undo:hasReceiver :a-res-47-180-1992-12-22 .
        
        ?ann a undo:Annotation ;
            undo:hasBody ?rel ;
            undo:hasTarget ?document
    }


## Question 4

What are all the terms that actually refer to with the concept of taking a decision, and in which documents have been used?

    PREFIX : <https://w3id.org/akn/data/undo/>
    PREFIX undo: <https://w3id.org/akn/ontology/undo/>
    
    SELECT DISTINCT ?term ?document
    WHERE {
        ?term a undo:Term ;
            undo:hasRelatedConcept :taking-a-decision .
           
        ?ann a undo:Annotation ;
            undo:hasBody ?term ;
            undo:hasTarget ?document
    }