# Demo HiC-Bench ChIP-Seq Pipeline

designed for use in NYU Langone Medical Center

This demo will walk you through the setup for a ChIP-Seq analysis. See more docs for this pipeline [here](https://github.com/NYU-BFX/hic-bench/tree/master/pipelines/chipseq-standard).

# Installation

## HiC-Bench

Make sure you've got [HiC-Bench](https://github.com/NYU-BFX/hic-bench) installed. This is typically installed in your home directory. 

```sh
cd
git clone https://github.com/NYU-BFX/hic-bench.git
```

If you're working on the phoenix server at NYU, make sure you have your `data` directory linked to Aris's. This contains the reference data needed for the pipeline.

```sh
cd hic-bench
ln -s /ifs/home/at570/disk1/Resources/Code/pipeline-master/data data
```

NOTE: you might have to delete the broken `data` symlink before you can reset it.

Compile binaries.

```sh
cd code/src
make
```

This should produce various `gtools*` and `tools*` binaries in `code/bin`.

## This Demo

Clone this demo repository, and change to its directory

```sh
git clone https://github.com/NYU-BFX/hic-bench-demo.git
cd hic-bench-demo
```

# Usage

From within this directory, create a new project (which creates a new directory) for the analysis.

```sh
~/hic-bench/code/code.main/pipeline-new-analysis chipseq-standard sample-project
```

Change to the project directory.

```sh
cd sample-project
```

Set input files.

```sh
./code/setup-sample-files.sh ../source_data/
```

Create sample sheet template from samples, supplying genome version and fragment size.

```sh
cd inputs/
./code/create-sample-sheet.tcsh hg19 200
```

Manually open the `inputs/sample-sheet.tsv` file (e.g. in Excel, etc.) and match up the Input samples with the experimental samples. Refer to the [samplesheet](https://github.com/NYU-BFX/hic-bench-demo/tree/master/example_samplesheet) provided with this repository for an example of what it should look like. 

Clean up the sample sheet.

```sh
mac2unix sample-sheet.tsv
sed -i 's/"//g' sample-sheet.tsv
```

Run the pipeline.

```sh
# need to be in the parent analysis dir
cd ..
code.main/pipeline-execute sample-project yourname@nyumc.org
```

Monitor progress.

```sh
watch qstat
```
