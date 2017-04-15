# Iteration 2: formal competency questions


## Question 1

What are the current roles of all the agents?

    PREFIX : <https://w3id.org/akn/data/undo/>
    PREFIX undo: <https://w3id.org/akn/ontology/undo/>
    
    SELECT DISTINCT ?agent ?role ?context
    WHERE {
        ?agent a undo:Agent ;
            undo:holdsValue ?value .
            
        ?value a undo:ValueInTimeAndContext ; 
            undo:withValue ?role ;
            undo:hasContext ?context .
        
        FILTER NOT EXISTS {
            ?value undo:atTime/undo:endsAt ?time
        }
            
        ?role a undo:Role .
    }


## Question 2

What roles have been held by Sergio Mattarella during his life?

    PREFIX : <https://w3id.org/akn/data/undo/>
    PREFIX undo: <https://w3id.org/akn/ontology/undo/>
    PREFIX owl: <http://www.w3.org/2002/07/owl#>
    
    SELECT DISTINCT ?role ?context ?start ?end
    WHERE {
        :sergio-mattarella undo:holdsValue ?value .
        
        ?value a undo:ValueInTimeAndContext ; 
            undo:withValue ?role ;
            undo:hasContext ?context ;
            undo:atTime ?time .
        
        ?time a undo:Interval ;
            undo:startsAt ?start .
         
        OPTIONAL {
            ?time undo:endsAt ?end
        }
        
        ?role a undo:Role .
    }


## Question 3

How many times an agent has been assigned to a specific role?

    PREFIX : <https://w3id.org/akn/data/undo/>
    PREFIX undo: <https://w3id.org/akn/ontology/undo/>
    
    SELECT DISTINCT ?agent ?role ?context (count(?agent) AS ?count)
    WHERE {
        ?agent a undo:Agent ;
            undo:holdsValue ?value .
        
        ?value a undo:ValueInTimeAndContext ; 
            undo:withValue ?role ;
            undo:hasContext ?context .
        
        ?role a undo:Role .
    }
    GROUP BY ?agent ?role ?context


## Question 4

Which roles are involved in particular contexts?

    PREFIX : <https://w3id.org/akn/data/undo/>
    PREFIX undo: <https://w3id.org/akn/ontology/undo/>
    
    SELECT DISTINCT ?context ?role
    WHERE {
        ?value a undo:ValueInTimeAndContext ;
            undo:withValue ?role ;
            undo:hasContext ?context .
            
        ?role a undo:Role .
    }
    

## Question 5

What are all the statuses that have been associated to all the documents?

    PREFIX : <https://w3id.org/akn/data/undo/>
    PREFIX undo: <https://w3id.org/akn/ontology/undo/>
    
    SELECT DISTINCT ?document ?status ?start ?end
    WHERE {
        ?document a undo:Document ;
            undo:holdsValue ?value .
        
        ?value a undo:ValueInTimeAndContext ;
            undo:withValue ?status ;
            undo:atTime ?time .
        
        ?time a undo:Interval ;
            undo:startsAt ?start .
        
        OPTIONAL {
            ?time undo:endsAt ?end
        }
            
        ?status a undo:Status .
    }
    