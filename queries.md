- Now
  - ```
    #+BEGIN_QUERY
    {:title ""
     :query [:find (pull ?b [*])
             :where [?b :block/marker ?marker]
            	    [(contains? #{"NOW" "DOING"} ?marker)]]
     :collapsed? false}
    #+END_QUERY 
    ```
- Scheduled
    - ```
      #+BEGIN_QUERY
      {:title ""
       :query [:find (pull ?b [*])
               :in $ ?today
               :where [?b :block/marker ?marker]
                      [(contains? #{"NOW" "LATER" "TODO"} ?marker)]
                      [?b :block/ref-pages ?p]
                      [?p :block/journal? true]
                      [?p :block/journal-day ?d]
                      [(>= ?d ?today)]]
       :inputs [:today]
       :collapsed? false}
      #+END_QUERY
      ```
- Overdue
    - ```
      #+BEGIN_QUERY
      {:title ""
       :query [:find (pull ?b [*])
               :in $ ?today
               :where
               [?b :block/marker ?marker]
               [(contains? #{"NOW" "LATER" "TODO"} ?marker)]
               [?b :block/ref-pages ?p]
               [?p :block/journal? true]
               [?p :block/journal-day ?d]
               [(< ?d ?today)]]
       :inputs [:today]
       :collapsed? false}
      #+END_QUERY
      ```
- Done
    - ```
      #+BEGIN_QUERY
      {:title ""
       :query [:find (pull ?b [*])
              :where
              [?b :block/marker ?marker]
              [(contains? #{"DONE" "CANCELED"} ?marker)]]
       :collapsed? false}
      #+END_QUERY
      ```
- Backlog
    - ```
      #+BEGIN_QUERY
      {:title ""
       :query [:find (pull ?b [*])
               :where [?b :block/marker ?marker]
                      [(contains? #{"LATER" "TODO"} ?marker)]
                      (not [?b :block/ref-pages ?p] 
                           [?p :block/journal? true])]
       :collapsed? false}
      #+END_QUERY
      ```
