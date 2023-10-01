# Audit.Bot_IP
APE capstone: IP_PainAudit from PAR output; VBA from launch template

Use Case: a painfully manual inpatient compliance audit process, wherein expensive RN hours (approx 10-12/month) are invested in a stare-and-compare exercise to determine the 'relative rates' (scare quotes...) of compliance with pain-assessment policy. Scare quotes because the process involves sampling a fixed number of charts per shift, so no denominator information considered whatsoever - the only information generated will be a sampling-rate which is ultimately luck of the draw.

Why did they do this, for years?
Because the raw data lives in multiple tables that are not completely mapped to Business Objects, so valuable field data is out of bounds, and...
The number of logical conditions is daunting:

  Records (events) are each of a Class, with each having a Type and a Category that is dynamic in relation to its sequence in chain with other records
  
  Example: A single Score could be considered both the Pre-PRN assessment for next Medication event AND the follow-up assessment for the previous 
  Medication event AND also be associated with enhanced analgesia protocol events in addition to the PRN records.
  
    - Differing event contexts confer rules for completeness of multirow assessments (partial vs complete)
    
    - There is no limit to the number of duplicate DTA rows that can appear within an assessment
    
    - Not every DTA row is considered mandatory for a complete assessment, and there needs to be an argument in the algo to allow the users to change the DTA's they require (there's a bunch of them,
      and they need to be passable as parameters)
      
    - The quant value of the Score itself controls the prerequisites for Partial vs Complete event parameters
    
    - The relative frequency and sequencing of the events is totally random (can have x assessments in a row, or x PRN events, or a single event with x DTA's, and there is so pattern by which to 
      predict what came before or will come next - lookup keys need to be dynamic and able to search stacks in both directions

OK - so from a logical algo perspective, this is a thorny problem - what is different about this particular solve?

- After brute forcing the algo and tuning it, I then set about automating the 100-200 steps required to clean/organize the raw data, apply the voluminous calculations, use calc results to apply flagging, and distribute the flagged records back to a trusted user in Inpatient for manual review of flagged records (some flags are manually removed after consideration of comments/notes that are unavailable to Business Objects raw data reports.
- I am a VBA tourist; I can read the code and infer intent, but I'm hardly fluent in writing solid syntax from scratch
- ChatGPT writes 'ok' VBA, albeit with tons of mistakes and red-herrings thrown in
- The end game was to take a highly specialized bit of process knowledge, and turn it into a one-click sharable solution that any analyst at any of our sites could clone-to-own
- My dialogs with Chat got a little testy at times; we lost patience with each other. We got snarky. It was somewhat Adversarial -- not a love-fest by any means
- Prompt engineering with adversarial themes produced more timely redirection and fewer wasted queries than uber-friendly did - I caught more flies with vinegar in this case
- The primary modules will be copied down to Git, as an example of the work produced by the APE partnership, and an example of the scale of ROI waiting to be mined from previous investments...
