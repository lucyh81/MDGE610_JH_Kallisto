# MDGE 610: kallisto EM Assignment

Assignment materials for Session 5 of MDGE 610: Foundations of Bioinformatics.

## Overview

In this assignment, students investigate the Expectation-Maximization (EM) algorithm as implemented in kallisto, a tool for RNA-seq transcript quantification. Students will examine convergence criteria and empirically test their effect on estimation accuracy.

## Getting Started

### Prerequisites

- **Git LFS**: This repository uses Git Large File Storage for the kallisto index file. Install Git LFS before cloning:

  ```bash
  # macOS (Homebrew)
  brew install git-lfs

  # Ubuntu/Debian
  sudo apt-get install git-lfs

  # After installation, initialize Git LFS
  git lfs install
  ```

- **CMake**: Required to build kallisto (version 3.0 or higher)

  ```bash
  # macOS
  brew install cmake

  # Ubuntu/Debian
  sudo apt-get install cmake
  ```

- **C++ compiler**: A modern C++ compiler with C++11 support (gcc 4.8+, clang 3.3+, or equivalent)

### Cloning this Repository

```bash
# Clone with Git LFS support
git lfs clone https://github.com/jasondk/mdge610-kallisto.git

# Or if you already have git lfs installed:
git clone https://github.com/jasondk/mdge610-kallisto.git
```

If the kallisto index file (`gencode.v44.kidx`) appears as a small text file (~130 bytes), Git LFS didn't download it properly. Run:

```bash
git lfs pull
```

### Installing kallisto from Source

You will need to build kallisto from source to modify and test convergence parameters.

```bash
# Clone kallisto
git clone https://github.com/pachterlab/kallisto.git
cd kallisto

# Create build directory
mkdir build
cd build

# Configure and build
cmake ..
make

# The kallisto binary will be at: build/src/kallisto
# Test it:
./src/kallisto version
```

For detailed instructions, see the [kallisto GitHub repository](https://github.com/pachterlab/kallisto).

## Contents

| File | Description |
|------|-------------|
| `assignment_handout.pdf` | Assignment instructions |
| `assignment_handout.tex` | LaTeX source for the handout |
| `1977 DLR EM paper.pdf` | Required reading: Dempster, Laird & Rubin (1977) |
| `gencode.v44.kidx` | Pre-built kallisto index (GENCODE v44 protein-coding transcripts) |
| `sim_reads_1.fastq.gz` | Simulated paired-end reads (read 1) |
| `sim_reads_2.fastq.gz` | Simulated paired-end reads (read 2) |
| `sim_true_counts.txt` | Ground truth transcript counts |

## Simulated Data Details

- **Reference**: GENCODE v44 human protein-coding transcriptome (110,962 transcripts)
- **Read pairs**: 1,000,000
- **Read length**: 75 bp paired-end
- **Fragment length**: Mean 250 bp, SD 50 bp
- **Sequencing error**: 1% per-base

## Running kallisto on the Provided Data

Once you have built kallisto, you can run it on the simulated data:

```bash
./kallisto quant -i gencode.v44.kidx -o output_dir sim_reads_1.fastq.gz sim_reads_2.fastq.gz
```

Results will be written to `output_dir/abundance.tsv`.

## Troubleshooting

**"kallisto: command not found"**: Make sure you're running kallisto from its build directory (`./src/kallisto`) or add it to your PATH.

**Build errors on macOS**: You may need to install Xcode command line tools: `xcode-select --install`

**Git LFS issues**: If files aren't downloading properly, ensure Git LFS is installed and run `git lfs pull`.

## Questions?

Bring questions to office hours or the designated Q&A class sessions.
