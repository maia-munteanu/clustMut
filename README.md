clustMut <img src="clustmut_logo.png" align="right" />
========================================================

The goal of clustMut is to call clustered mutations in sets of somatic mutations.
A clustered mutation is defined as the result of a local _hyper_-mutation event.

This package uses XXX different statistics to compute and detect those events.

* Chromosomic distance - Need a randomized version of the sample that you can generate using [randommut](http://fsupeksvr.irbbarcelona.pcb.ub.es/gitlab/dmas/randommut).
* Allele Frequency
* Edit distance between mutations

## Installation

**Using devtools**

Install the package using the following command. Note that is needed to install genomicHelpersDMP manually from its repository [here](http://fsupeksvr.irbbarcelona.pcb.ub.es/gitlab/dmas/genomicHelpersDMP)

```bash
install.packages(c("devtools","getPass"))
devtools::install_git(
  "http://fsupeksvr.irbbarcelona.pcb.ub.es/gitlab/dmas/clustMut.git", 
  credentials = git2r::cred_user_pass("dmas", getPass::getPass()),
  branch = "dev"
)
```

Then, move the script to run to your `bin` or to a folder available in your `$PATH`.
This is a one time only action, when you update your package the new version will be available from the same script.

**Cloning the repository**

First, clone the repository and builod the package

```bash
git clone gitlab@fsupeksvr.irbbarcelona.pcb.ub.es:dmas/clustMut.git
cd clustMt
R CMD INSTALL --no-multiarch --with-keep.source .
```

Then link the clustMut executable (bash script) to a folder in your path.

```bash
ln -s clustmut ~/bin/
```

### Dependencies

R packages should be installed when instaling the package. No other packages are needed for the package. Bash and UNIX is required to run the shell script. 

## Usage

You can use clustmut to obtain kataegis events, clusters based on VAF or clustered mutations based on the Edit distance.
Run it with the appropiate mode command.

### distance

```bash
clustmut distance -i /home/dmas/data/TCGA_MUTS/RNDmut/ \
                --glob "*randomized.tsv" \
                --recursive \
                -o test_omichili \
                -N 1 \
                -Vlwtvu
```

### Boosting

A file with the following information has to be provied as the `{rndmut_file_name}_stratification`. This file needs to be a list of this level.

```
chr:pos:sample:ref:alt_{group}
```

where group is a set of mutations that will be grouped together.

NOTE: Samples will allways be included in the group as default.


## Troubleshooting


| Error code | Situation                                                                                                                                                | Solution                           |
|------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------|
| 123        | When the sample (or multiple samples) doesn't have any valid mutation. This means all mutations mutations have been excluded because of the filters used | Remove that sample or the filters. |
|            |                                                                                                                                                          |                                    |
