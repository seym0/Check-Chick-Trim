# About
This is a repository for storing the Check-Chick-Trim study project of the Introduction to Bioinformatics course from the Hyperskill platform.
# Article
### Methods
The present study aims to improve the quality of sequencing data for the bacterium  Herbaspirillum seropedicae isolated from aldur root nodules (SRR15712950), the data was taken from SRA database [1]. SRA Toolkit 3.0.1 [2] was used to unpack the SRR15712950 archive, FastQC 0.11.9 [3] was used to quality control checks, Trimmomatic 0.39 [4] was used to to improve the FastQC metrics by ILLUMINACLIP:~/project/Trimmomatic-0.39/adapters/TruSeq3-PE.fa:2:30:10 and CROP:220 options for paired-end reads. 
### Results
Comparing the quality of the original data with the data obtained after trimming, two quality parameters have improved: Per base sequence content and Adapter Content from “red” to “green”. Module Per sequence GC content deteriorated from “orange” to “red” and parameter Overrepresented sequences remained bad without change. 
### Discussion
Dataset requires more analysis, thus it cannot be used. I suppose that the data still contains contamination from the need to trim adaptors because two peaks on the parameter Per sequence GC content are present.
### References
1. SRA [Internet]. Bethesda (MD): National Library of Medicine (US), National Center for Biotechnology Information; 2004 – [cited 2023 Jan 12]. Available from: https://www.ncbi.nlm.nih.gov/sra
2. SRA Toolkit Development Team. The NCBI SRA Toolkit [Online]. Available online at: https://github.com/ncbi/sra-tools.git
3. Andrews, S. (2010). FastQC: A Quality Control Tool for High Throughput Sequence Data [Online]. Available online at: http://www.bioinformatics.babraham.ac.uk/projects/fastqc/
4. Bolger, A. M., Lohse, M., & Usadel, B. (2014). Trimmomatic: A flexible trimmer for Illumina Sequence Data. Bioinformatics, btu170

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

6. When I later added ```CROP:220```, quality parameters Per base seqs content and Adapter content improved, whereas %GC-content degrades. Other parameters remained unchanged.
- second_trim/output_forward_paired1_fastqc.html

7. Finally, you can see the result in the file 
- second_trim/output_forward_paired1_fastqc.html
