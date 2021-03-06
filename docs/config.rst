Pipeline YAML Files
===================

The list of which steps to run in a pipeline, the overall inputs for it, execution information, and directories for output, are all defined in a configuration file in the YAML format.

Here is an example, from test/test.yml:


.. code-block:: yaml

    # Python modules that are imported to find 
    # stage classes.  Any stages imported in these 
    # modules are automatically detected and their names can 
    # be used below
    modules: ceci_example_lib

    # The list of stages to run and the number of processors
    # to use for each.
    stages:
        - name: WLGCSummaryStatistic
          nprocess: 1
        - name: SysMapMaker
          nprocess: 1
        - name: shearMeasurementPipe
          nprocess: 1
        - name: PZEstimationPipe
          nprocess: 1
        - name: WLGCRandoms
          nprocess: 1
        - name: WLGCSelector
          nprocess: 1
        - name: SourceSummarizer
          nprocess: 1
        - name: WLGCTwoPoint
          nprocess: 1
        - name: WLGCCov
          nprocess: 1

    # Definitions of where to find inputs for the overall pipeline.
    # Any input required by a pipeline stage that is not generated by
    # a previous stage must be defined here.  They are listed by tag.
    inputs:
        DM: ./test/inputs/dm.txt
        fiducial_cosmology: ./test/inputs/fiducial_cosmology.txt

    # If all the outputs for a stage already exist then do not re-run that stage
    resume: True

    # Put all the output files in this directory:
    output_dir: ./test/outputs

    # Put the logs from the individual stages in this directory:
    log_dir: ./test/logs

    # Put the log for the overall pipeline infrastructure in this file:
    pipeline_log: log.txt

     # Information describing the "Launcher" that parsl will use to run jobs.
     # For now don't change this -
     # it is part of parsl.
    launcher:
        globals: {lazyErrors: true}
        sites:
          # Name
          # Can put SSH info here to launch remotely
        - auth: {channel: null}
          # Execution system
          execution: {
            executor: threads, 
            maxThreads: 4, 
            provider: null
        }
          site: Local_Threads



