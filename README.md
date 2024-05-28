# regression-analysis
A place to record all my work that will be part of it


### Working Notes
1. Simulate the scenario that was given to me for E2E CPT SetUp.
2. Typically requires the following things ...

    1. QE Job triggers the Performance job, upon successful QE job triggers Regression analysis job
    2. Regression Analysis Pipeline job should be saved in the performance repo

        1. Should accept one parameter, ${PERFORMANCE_PIPELINE_JOB_ID}.
        2. Should perform the regression analysis by defining the limits/threshold using Normal Distribution.
        3. Should create a Table Chart and Line Chart using ${PLACE_HOLDER_OF_THE_GRAPHING_LIBRARY} and save it in a HTML file for distribution.
        4. Should provide summary at the end along with a link that is pointing to the HTML file that is created for distribution.


### To-Do
1. Lot of simulation

    1. Create a separate pipeline for regression analysis.
    2. Generate a HTML file that holds the regression analysis data.
    3. How to handle the regression analysis data ? Should we index it in OpenSearch ??
    4. How do you want to visualize the regression analysis data ? Schema pattern ??
    5. ...
