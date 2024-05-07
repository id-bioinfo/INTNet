INTNet
=====
Multi-task multilabel deep neural networks for identification and classification of integrons.

INTNet is designed to identify and classify integron integrases, predict bacterial hosts, and associate ARGs (multi-label) with integrons. This versatile tool supports a range of input types including:
* Long Amino Acid Sequences (Full Length/Contigs)
* Long Nucleotide Sequences
* Short Amino Acid Reads (30-50 aa)
* Short Nucleotide Reads (100-150 nt)

All inputs should be in FASTA format.

**INTNet Components**\
INTNet comprises two specialized models to accommodate different read lengths:
* **INTNet-s**: Optimized for short reads, enhancing prediction accuracy for sequences ranging from 30 to 50 amino acids or 100 to 150 nucleotides.
* **INTNet-l**: Tailored for long sequences, ensuring robust predictions for full-length contigs or long nucleotide sequences.

![alt text](https://github.com/patience111/INTNet/blob/master/pics/INTNet_workflow.jpg)

Installation
------------
clone the program to your local machine\
git clone https://github.com/patience111/INTNet


**1. Setting up environment**


**1.1 Installation with conda**


1.1.1 For **CPU** inference, you could install the program with conda YAML file in the installation directory with the following commands:

```
cd ./installation 
conda env create -f INTNet-CPU.yml -n INTNet-cpu
conda activate INTNet-cpu
```

(This was tested on Ubuntu 16.04, 20.04; Windows 10, macOS(14.1.1))\
 ![alt text](https://github.com/patience111/INTNet/blob/master/pics/test_cpu.jpg)

 1.1.2 For **GPU** inference, you could install the program with conda YAML file in the installation directory with the following commands:</br>
```
cd ./installation
conda env create -f INTNet-GPU.yml -n INTNet-gpu
conda activate INTNet-gpu
```
(This was tested on Ubuntu 16.04, cuda 10.1, Driver Version: 430.64)\
    ![alt text](https://github.com/patience111/INTNet/blob/master/pics/test_gpu_1.jpg)
    ![alt text](https://github.com/patience111/INTNet/blob/master/pics/test_gpu_2.jpg)


**1.2 Or, if you prefer installing dependencies manually, you might find this information useful:**\
The program was tested with the following package version, you can install exactly the same version or other compatible versions.
```
Biopython:  1.79
tensorflow:  2.2.0 
cuda: 10.2 (for GPU using)
cudnn: 7.6.5.32 (for GPU using)
numpy: 1.18.5
scikit-learn: 0.24.1
tqdm: 4.56.0
```
**2. Getting trained models**

```   
cd ./models
bash get-models.sh
```
Quickstart Guide
----------------
***for long sequences***

```
python intnet.py --input input_path_data  --type aa/nt --model argnet-l  --outname output_file_name
```
***for short reads***

```
python intnet.py --input input_path_data --type aa/nt --model argnet-s --outname output_file_name
```

**general options:**</br>
     --input/-i&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;the test file as input </br>
     --type/-t &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;molecular type of your test data (aa for amino acid, nt for nucleotide)</br>
     --model/-m&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;the model you assign to make the prediction (argnet-l for long sequences, argnet-s for short reads) </br>
     --outname/-on&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;the output file name </br>


**optional arguments:**</br>
  -h, --help            show this help message and exit</br></br>
  ![alt text](https://github.com/patience111/INTNet/blob/master/pics/intnet_helpPage.png)</br>
  -i INPUT, --input INPUT </br>
                        the test data as input </br></br>
  -t {aa,nt}, --type {aa,nt} </br>
                        molecular type of your input file </br></br>
  -m {argnet-s,argnet-l}, --model {argnet-s,argnet-l} </br>
                        the model to make the prediction </br></br>
  -on OUTNAME, --outname OUTNAME </br>
                        the name of results output </br></br>


Example
----------
if we predict the long amino acid contigs by using ARGNet-L model, we could use command line (if you are in ARGNet dirctory):</br></br>
```
python3 ./scripts/argnet.py -i ./tests/aa/long/arg100p.fasta -t aa -m argnet-l -on argnet_lsaa_test.txt
```
**output** will be like and saved in the **results** folder: </br>
![alt text](https://github.com/patience111/ARGNet/blob/main/pics/lsaa_prediction.png)</br>
the first column **test_id** is the sequence label of the test sequnece.</br>
the second column **ARG_prediction** is the "ARG" or "non-ARG" prediction of the input sequence.</br>
the third column **resistance_category** is the classifition of the 36 antibiotics categories of the input sequence resisting to.</br>
the last column **probability** is the classifition probability of the antibiotic predition of the input sequence by the model.
