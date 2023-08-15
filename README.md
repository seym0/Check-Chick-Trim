# About
This is a repository for storing the Check-Chick-Trim study project of the Introduction to Bioinformatics course from the Hyperskill platform.

# Steps
1. To obtain the sequencing data from the SRA NCBI, I navigated to the database and searched for the desired run-file, which in this case was SRR15712950 ([SRX12008558](https://www.ncbi.nlm.nih.gov/sra/SRX12008558[accn]): WGS sequencing of Herbaspirillum seropedicae I88 isolated from aldur root nodules). Once I located the data, I downloaded it using wget in Ubuntu and created a project folder to store it.

2. Next, I downloaded and installed sratoolkit.3.0.1-ubuntu64, a tool used to extract data from SRA run-files. I also appended the path to the binaries to the PATH environment variable using the export command.

3. To unpack the SRR*** run-file, I used the ```fastq-dump --split-3``` to obtain forward and reverse Illumina reads. This resulted in three files: 
- SRR15712950.fastq (both reads), 
- SRR15712950_1.fastq (forward reads), 
- SRR15712950_2.fastq (reverse reads). 

4. To see the quality of the data, I ran FastQC on each of the three files using the ```./fastqc``` command. This resulted in three files:
- before_trim/SRR15712950.fastq.html
- before_trim/SRR15712950_1_fastqc.html
- before_trim/SRR15712950_2_fastqc.html

5. Then I trimmed the forward and reverse reads using Trimmomatic, a command line tool that can be used to trim and crop Illumina (FASTQ) data as well as to remove adapters. Firstly, I used only ILLUMINACLIP to cut adapters ```ILLUMINACLIP:./Trimmomatic-0.39/adapters/TruSeq3-PE.fa:2:30:10) ```
This resuted in file:
- first_trim/output_forward_paired_fastqc.html

6. When I later added ```CROP:220```, quality parameters per base seqs content and adapter content improved, whereas %GC-content degrades. Other parameters remained unchanged.
- second_trim/output_forward_paired1_fastqc.html

7. Finally, you can see the result in the file 
- output_forward_paired1_fastqc.html.
