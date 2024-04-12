# Red
Red: an intelligent, rapid, accurate tool for detecting repeats de-novo on the genomic scale. 

This fork of the original at https://github.com/BioinformaticsToolsmith/Red adds usability information and allows compilation with g++9 (eg on Ubuntu 2004)


## Compiling the source code

Requirement: GNU gcc8.2 or higher. Please change the name (CXX) of the compiler in the Makefile. 

```
# get the code
git clone https://github.com/brunocontrerasmoreira/Red

cd Red && cd src_2.0

# The following command makes the required directories: 
make bin

# The following command makes the binary that is located under the ``bin'' directory:
make -j 4

# To find the binary:
cd ../bin

# Run the binary
./Red
```

## Example command

# only genomes in .fa format are detected properly 
ln -s genome.fasta input.fa

# out dirs must all exist else core dump
mkdir -p out_mask output

# Run Red with an input.fa in the current dir . 
Red -gnm . -msk out_mask -rpt output



## Full usage

```
This is Red (REpeat Detector) designed and developed by Hani Zakaria Girgis, PhD.

Version: 2.0

Argument pairs of the form: -flag value are required.
Valid argument pairs:
        -gnm input genome directory, required.
                Files with ".fa" extension in this directory are used for completing the table of the adjusted counts.
                These Files are scanned for repeats.
        -dir directory including additional input sequences, optional.
                Files with ".fa" extension in this directory are NOT used for completing the table.
                These Files MUST have different names from those in the genome directory.
                These Files are scanned for repeats.
        -len word length equals k defining the k-mer. The default is floor(log_4(genome size)).
        -ord order of the background Markov chain. The default is floor(k/2)-1.
        -gau half width of the mask. The default is based on the GC content.
                20 if the GC content > 33% and < 67%, 40 otherwise.
        -thr the threshold score of the low adjusted scores of non-repeats. The default is 2.
        -min the minimum number of the observed k-mers. The default is 3.
        -tbl file where the table of the adjusted counts is written, optional.
        -sco directory where scores are saved, optional.
                Score files have the ".scr" extension.
        -cnd directory where candidate regions are saved, optional.
                Candidates files have the ".cnd" extension.
        -rpt directory where repeats locations are saved, optional.
                Repeats files have the ".rpt" extension.
        -msk directory where masked sequences are saved, optional.
                Masked sequences files have the ".msk" extension.
        -frm the format of the output: 1 (chrName:start-end), 
             2 (chrName start   end) or 3 (chrName      start   end).
                Output formats 1 & 2 are zero-based, end exclusive.
                Output format 3 is one-based, end inclusive (Ensembl).
        -hmo file where the HMM is saved, optional.
        -cor integer of the number of threads, optional.
                The more threads, the higher the memory requirement.
                The defaul is the number of cores - 1, or 1 if single core is found.

Examples:
        The following command runs Red with the defaults and generates the masked sequences.
        Red -gnm genome_directory -msk output_directory

        The following command runs Red with the defaults and generates the masked sequences and the locations of repeats.
        Red -gnm genome_directory -msk output_directory -rpt output_directory
```


Please cite the following paper:

Girgis, H.Z. (2015) Red: an intelligent, rapid, accurate tool for
detecting repeats de-novo on the genomic scale. BMC Bioinformatics,
16, 227.

Original Repo 

https://github.com/BioinformaticsToolsmith/Red