# covid
COVID-19 tool development

An open collaboration between the Cleveland Clinic and SAS Institute.


# What this Code Does
This code takes a set of input parameters and uses them in infectious disease models (SIR & SEIR).  Model output is used to calculate useful metrics for each day of an epidemic, such as the number of hospitalizations.  

# Documentation
In addition to the information shared within this readme and the commenting within the code, you can also review the [documentation on the implementation of the models in SAS](./docs/seir-modeling).

For a good understanding of the SIR and SEIR model approaches, we recommend this [very well written blog post](https://triplebyte.com/blog/modeling-infectious-diseases) from the folks at TRIPLEBYTE.

# Getting Started
- **PREPARE**
    - Download `COVID_19.sas` to your SAS environment
        - Also, download the `run_scenario.csv` file for an example submission file to run many scenarios in batch
- **SETUP**
    - Edit `line 10` to a local directory you want to save datasets with model output and scenario information to
    - If you do not have SAS/ETS then edit `line 16` to 'NO'
        - This option causes the SIR/SEIR models to run with a SAS Data Step version only
        - If you are unsure then you can run `PROC PRODUCT_STATUS; run;` in SAS and view the log for this information
    - If you have the latest analytical release of SAS, 15.1, then set `line 17` to YES
        - This option swaps out `PROC MODEL` for `PROC TMODEL`
        - If you are unsure then you can run `PROC PRODUCT_STATUS; run;` in SAS and view the log for this information
- **RUN**
    - Make calls to the macro `%EasyRun`.  Example scenarios are at the end of the file.
    - Submit many scenarios in batch by using an input file.  An example file, `run_scenarios.csv`, is provided. Each row of this file will feed individual calls to the `%EasyRun` macro.
- **REVIEW**
    - All model output for each call to `%EasyRun` saves in the dataset `STORE.MODEL_FINAL`
    - All of the parameters that lead to the results in `STORE.MODEL_FINAL` save in `STORE.SCENARIOS`, and all inputs to the macro also save to `STORE.INPUTS`.  The variable `SCENARIOINDEX` links these files.
- **ADJUST inputs to your population**
    - Change the input parameters to match the population you are working with.  If their is a wide range of scenarios you want to run then use the run_scenarios.csv method to easily submit all the combinations.

# Explore the Inputs, Outputs and Details in the Wiki
[Explore the wiki](https://github.com/sassoftware/covid-19-sas/wiki/CC%3A-Home)

# Development Notes
- The current locked version of the project is in `COVID_19.sas`.
- Progress towards the next locked version is in the `/progress` folder
- the `COVID_19.sas` file is built from modular parts in `/build/parts` into the `/build/public` folder by `/build/build.py` and then copied here

# Example Scenario Visuals
With the option `plots=yes`, the `COVID_19.sas` program will create diagnostic visuals for each scenario. Some example of these visuals follow.  The output data is also available in SAS Visual Analytics with user interface to drive the running of scenarios is in the works.
| All Approaches | Fitting Approaches |
:-------------------------:|:-------------------------:
![](./examples/example-0.png)  |  ![](./examples/example-1.png)
![](./examples/example-4.png)  |  ![](./examples/example-2.png)
![](./examples/example-3.png)  |  

# Example User Interface (Coming Soon)
Our goal is to allow users to visualize and run scenarios from a user interface.  Take a look at our current prototype:

![](./examples/ui_demo.gif)