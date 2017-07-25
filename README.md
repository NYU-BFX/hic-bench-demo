# Demo HiC-Bench ChIP-Seq Pipeline

designed for use in NYU Langone Medical Center

This demo will walk you through the setup for a ChIP-Seq analysis. See more docs for this pipeline [here](https://github.com/NYU-BFX/hic-bench/tree/master/pipelines/chipseq-standard).

# Installation

## HiC-Bench

Make sure you've got [HiC-Bench](https://github.com/NYU-BFX/hic-bench) installed. This is typically installed in your home directory. 

```
cd
git clone https://github.com/NYU-BFX/hic-bench.git
```

If you're working on the phoenix server at NYU, make sure you have your `data` directory linked to Aris's. This contains the reference data needed for the pipeline.

```
cd hic-bench
ln -s /ifs/home/at570/disk1/Resources/Code/pipeline-master/data data
```

NOTE: you might have to delete the broken `data` symlink before you can reset it.

## This Demo

Clone this demo repository, and change to its directory

```
git clone https://github.com/stevekm/hic-bench-demo.git
cd hic-bench-demo
```

# Usage

From within this directory, make a new directory for the analysis, and start a new HiC-Bench analysis there:

```
mkdir sample-project
~/hic-bench/code/code.main/pipeline-new-analysis chipseq-standard sample-project
```

Change to that directory:

```
cd sample-project
```

and finish pipeline setup; 

- set input files

```
code/setup-sample-files.sh ../source_data/
```

- create sample sheet template from samples, supplying genome version and fragment size

```
cd inputs/
code/create-sample-sheet.tcsh hg19 400
```

- __MANUALLY__ open the `inputs/sample-sheet.tsv` file (e.g. in Excel, etc.) and match up the Input samples with the experimental samples. Refer to the [samplesheet](https://github.com/stevekm/hic-bench-demo/tree/master/example_samplesheet) provided with this repository for an example of what it should look like. 

- run the pipeline

```
# need to be in the parent analysis dir
cd ..
code.main/pipeline-execute sample-project yourname@emailaddress.org
```
