# Iteration 3: formal competency questions


## Question 1

In which step of all the workflows the first version of a document has been produced?

    PREFIX : <https://w3id.org/un/data/undo/>
    PREFIX undo: <https://w3id.org/un/ontology/undo/>
    
    SELECT ?doc ?step 
    WHERE {
        ?step a undo:Step ;
            undo:produces ?doc .
        FILTER NOT EXISTS {
            ?another_step a undo:Step ;
                undo:produces ?prev_version .
            ?prev_version undo:hasRevision+ ?doc
        }
    }


## Question 2

How many steps (on average) are used in each workflow?

    PREFIX : <https://w3id.org/un/data/undo/>
    PREFIX undo: <https://w3id.org/un/ontology/undo/>
    PREFIX owl: <http://www.w3.org/2002/07/owl#>
    
    SELECT (avg(?n_step) as ?average)
    WHERE {
        {
            SELECT ?workflow (count(?step) as ?n_step)
            {
                ?workflow a undo:Workflow ;
                    undo:hasStep ?step .
            } GROUP BY ?workflow
        }
    } GROUP BY ?workflow


## Question 3

How much did it take to executing each step in each workflow execution?

    PREFIX : <https://w3id.org/un/data/undo/>
    PREFIX undo: <https://w3id.org/un/ontology/undo/>
    
    SELECT ?execution ?step (round(?end - ?start) as ?minutes)
    WHERE {
        {
            SELECT ?execution ?step (min(?s_date) as ?start) (max(?e_date) as ?end) {
                ?execution a undo:WorkflowExecution ;
                    undo:includesAction ?action .
                ?action a undo:Action ;
                    undo:addresses ?step ;
                    undo:atTime ?time .
                ?time a undo:Interval ;
                    undo:startsAt ?s_date ;
                    undo:endsAt ?e_date .
            } GROUP BY ?execution ?step
        }
    }


## Question 4

What was the last entities produced by all the workflow executions?

    PREFIX : <https://w3id.org/un/data/undo/>
    PREFIX undo: <https://w3id.org/un/ontology/undo/>
    
    SELECT ?execution ?entity {
        ?execution a undo:WorkflowExecution ;
            undo:includesAction/undo:addresses ?step .
        ?step a undo:Step ;
            undo:produces ?entity .
        FILTER NOT EXISTS {
            ?step undo:hasFollowingStep ?another_step .
        }
    }