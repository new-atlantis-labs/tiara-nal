# [Tiara](https://ibe-uw.github.io/tiara/)

Deep-learning-based approach for identification of eukaryotic sequences in the metagenomic data powered by [PyTorch](https://pytorch.org).  [Modified by [Josh L. Espinoza](https://github.com/jolespin) for Python 3.9+ and stdin support]

The sequences are classified in two stages:

- In the first stage, the sequences are classified to classes: 
      archaea, bacteria, prokarya, eukarya, organelle and unknown.
- In the second stage, the sequences labeled as organelle in the first stage 
      are classified to either mitochondria, plastid or unknown.

For more information, please refer to our paper:
[*Tiara: Deep learning-based classification system for eukaryotic sequences*](https://doi.org/10.1093/bioinformatics/btab672).

[Supplementary data](https://academic.oup.com/bioinformatics/advance-article/doi/10.1093/bioinformatics/btab672/6375939#supplementary-data)

[Supplementary sequences](data/Supplementary_sequences)

## Requirements

- `Python >= 3.7,<3.10`
- `numpy, biopython, torch, skorch, tqdm, joblib, numba`

## Installation

More detailed installation instructions can be found [here](docs/detailed-installation.md).

#### Using `pip`

```bash
pip install -U https://github.com/jolespin/tiara-nal/releases/download/1.0.4rc2/tiara-1.0.4rc2.tar.gz
```

#### Testing the installation

After the installation, run `tiara-test` to see if the installation was successful.

## Usage

#### Basic usage:
```bash
tiara -i input.fasta -o out.tsv

cat input.fasta.gz | gzip -d | tiara -o out.tsv
```

The sequences in the fasta file should be at least 3000 bases long (default value). We do not recommend classify sequences that are shorter than 1000 base pairs.

It creates two files: 

 - out.txt, a tab-separated file with header `sequence id, first stage classification result, second stage classification result`.
 - log_out.txt, containing model parameters and classification summary.

#### Advanced:

```bash
tiara -i input.fasta -o out.tsv --tf mit pla pro -t 4 -p 0.65 0.60 --probabilities
```

In addition to creating the files above, it creates, in the folder where `tiara` is run,
three files containing sequences from `input.fasta` classified as 
mitochondria, plastid and prokarya (`--tf mit pla pro` option).

The number of threads is set to 4 (`-t 4`) and probability cutoffs 
in the first and second stage of classification are set to 0.65 and 0.6, respectively.

The probabilities of belonging to individual classes are also written to 
`out.tsv`, thanks to `--probabilities` option.

For more usage examples, go [here](docs/usage.md).

## Citation 

Micha?? Karlicki, Stanis??aw Antonowicz, Anna Karnkowska, Tiara: deep learning-based classification system for eukaryotic sequences, Bioinformatics, Volume 38, Issue 2, 15 January 2022, Pages 344???350, https://doi.org/10.1093/bioinformatics/btab672

## License

Tiara is released under an open-source MIT license 












