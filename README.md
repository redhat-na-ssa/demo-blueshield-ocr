# demo-blueshield-ocr
This project contains the configurations to provide infrasctructure, on OpenShift, that supports ML and AI workloads for a blueshield demo.  The demo involves gathering unstructured pdfs and using labelstudio (with tesseract) to structure data from the pdfs into structured data.  Structured data will be stored in a vector DB (postgres).  Data will be pulled by a pipeline from an ARO cloud configuration.  

The demo demonstrates the value of using OpenShift (onPrem) to gather/curate onPrem data which is then used by the ARO cloud instance for model training.
