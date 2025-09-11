Summary 

The ATP Claims solution is developing a single source of truth for the claims enterprise model. The current approach is to do analysis of the COBOL code for APRA datasets, then do gap analysis between GL and HCM data to find the differences between the claims information. After this is complete we provide an options paper on enterprise modelling approach. 

New ask:  

Re-use the Lift & Shift solution as our enterprise layer, to include APRA and GL requirements. 

Current HCM solution in BDP4 

The silver and gold layers developed by the HCM Lift and Shift migration does not following silver enterprise layer standards. The slv_migrated_hcm schema has 25 DIMs , 4 facts and 2 reference tables, the way they are currently built cannot be leveraged as a point to lift for enterprise layer. 

Example 1 

There is a DIM_MEMBER table with policy information and member PII data, this is not compliant with silver modelling standards. The PII information should be stored in the hi_insured_person table within the customer schema and the rest in the hi_policy table within the policy schema. 

If we need to unpick this build and reapply this to the silver layer need to understand: 

What are the source tables driving the development of DIM_MEMBER? 

What business filters have been applied on this dimension? 

Downstream impact, how is this table being used further down in the chain? 

After these questions are answered, we can provide an effort of FTE days what it would take to convert this into enterprise ready solution. 

Example 2 

There are 4 different facts for claims; fact_episodes, fact_ancillary_claim, fact_hospital_claims, fact_medical_claim. It is still not determined whether we can put claims into one schema within silver, that is what our current Q4 objective is. If we continue to use this model there will be tech debt from SAS system in BDP4. 

Actions 

ATP team to do gap analysis for the claim type to understand the option in combining the definitions in the silver layer 

HCM team to provide detail on the source tables driving the facts? 

HCM team to provide filter conditions applied to the tables 

 

Open Questions 

Is current code base close to enterprise model? 

High light what points are missing from engineering perspective? 

Have they got the from and to date in the primary key? There is no history stitching 

Have the silver tables being tested for ATP use cases 

Bottom Line Need to go into the detail and re-engineer it 

Why we can’t re-use the current hcm model as it is? AP is this something we can only decide after gap analysis is complete  

Approach? 
