# Password Policy Resilience Pentest Lab - OBJECTIVE

The goal of this project is to test password policy resilience using automated wordlist generation and hash-cracking techniques.
All operations were performed on a single machine (Ubuntu). Goal is to use PassGAN/PassGPT.
Instead of TheHarvester, we used a custom script (osint_cli_generator.py) to simulate OSINT activities, generating synthetic profiles and data for wordlist enrichment.
For password candidate generation, we used PassGPT (an AI generative model), both in its basic version and with synthetic OSINT data.
Recently, the classic rockyou wordlist was also included for benchmarking and comparative purposes.

## Warning:
During the research of PassGAN//PassGPT we found that most sources are old/obsolete. This is the reason we made a python tool to accomplish the endpoint of w working project.
