## Key Finding: ViT vs KG Generalisation

The ViT-based anomaly detector (VideoMAE + MIL ranking head), trained and validated on 
UCF-Crime, achieved strong in-domain performance (AUC 0.81-0.90 across Vandalism, 
Stealing, Robbery, Burglary, Shoplifting).

However, when tested on out-of-domain footage (a self-recorded staged theft scenario, 
different camera angle/lighting/setting from UCF-Crime), the ViT anomaly score dropped 
sharply (0.17, well below the alert threshold) despite the scenario matching a real theft 
pattern.

The knowledge-graph rule layer (YOLO detection + tracking + zone/proximity reasoning), 
by contrast, correctly flagged the same clip (near_shelf=True, object_contact=True), 
since it reasons over detected entities/relations rather than learned visual patterns 
tied to UCF-Crime's specific footage style.

This validates the core premise of the hybrid neuro-symbolic design: the KG layer 
provides robustness to domain shift that a purely learned anomaly detector lacks, 
at the cost of being coarser and more manually specified.
