## Function points

### Use cases

#### Manage levels

- EI
    - FTR: (levels, prompt_templates) #2
    - DET: (name, difficulty, root, password, component_ordering, component_text) #6
    - Weighting factor => Average

    - Create level
    - Modify level
    - Delete level
    - Create prompt component
    - Modify component
    - Delete prompt component
    - Move prompt component
    - => 7
- EO
    - None
- EQ
    - FTR: (levels, prompt_templates) #2
    - DET: (name, difficulty, root, password, component_ordering, component_text) #6
    - Weighting factor => Average

    - Get levels
    - Get prompt components
    - Validate login
    - => 3
- ILF
    - RET: (levels, prompt_templates) #2
    - DET: (name, difficulty, root, password, component_ordering, component_text) #6
    - Weighting factor => Low

    - Levels
    - Prompt components
    - => 2
- EIF
    - RET: (moderators) #1
    - DET: (name, password, email) #3
    - Weighting factor => Low

    - Moderator accounts
    - => 1

===> 38.35 FP

#### Chat with gatekeeper
- EI
    - FTR: (session, levels, prompt_templates) #3
    - DET: (session_id, level_id, username, message) #4
    - Weighting factor => Average

    - Send message
    - => 1
- EO
    - None
- EQ
    - None
- ILF
    - RET: (session, levels) #2
    - DET: (session_id, level_id, username, message, level_name, component_ordering, component_text) #6
    - Weighting factor => Low

    - Session
    - Levels
    - Prompt components
    - => 3
- EIF
    - None

===> 16.25 FP

#### Validate password
- EI
    - None
- EO
    - None
- EQ
    - FTR: (levels) #1
    - DET: (level_id, password) #2
    - Weighting factor => Low

    - Validate password
    - => 1
- ILF
    - RET: (levels) #1
    - DET: (level_id, password) #2
    - Weighting factor => Low

    - Levels
    - => 1
- EIF
    - None

===> 6.5 FP

To see whether the function points actually correlate with the time we really spent on the usecase, we created a scatterplot:
![fp-time-plot](./assets/fp-time-plot.svg)
