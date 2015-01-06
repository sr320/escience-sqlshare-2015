This workflow outlines how to transfer coordinates of CDS (ie exons) from genome scaffolds to genes. A GFF file with mRNA and CDS regions was published and with the oyster genome -Zhang, G; Fang, X; Guo, X; Li, L; Luo, R; Xu, F; Yang, P; Zhang, L; Wang, X; Qi, H; Zhu, Y; Yang, L; Huang, Z (2012) Genomic data from the Pacific oyster (Crassostrea gigas). GigaScience. http://dx.doi.org/10.5524/100030

<hr>
<img src="https://www.evernote.com/shard/s10/sh/9eb7c221-8d27-476f-b009-6e0d815b228e/62be962180ae36159e30683aec067ab7/deep/0/Screenshot%205/24/13%201:47%20PM.png" alt="Screenshot%205/24/13%201:47%20PM" width = 60%/>
<hr>

Files were separated based on Column3 (in TextWrangler) uploaded to SQLShare.
In SQLShare they were _Edited_ to have only Gene IDs in Column9 (for joining purposes).

<img src="https://www.evernote.com/shard/s10/sh/473da017-8dcb-4923-aec5-d6e1e4708559/461b3c1ad4ee355a73e8c2fe8bee0516/deep/0/Screenshot%205/24/13%201:49%20PM.png" alt="Screenshot%205/24/13%201:49%20PM" width = 60% />
<hr>
<https://sqlshare.escience.washington.edu/sqlshare#s=query/sr320%40washington.edu/oyster_v9_mRNA%20GFF>
<hr>
<img src="https://www.evernote.com/shard/s10/sh/44246e68-def8-413c-a360-77303bc3922b/32f4c61c7c83bcba0b2e2e7703ed7f2d/deep/0/Screenshot%205/24/13%201:54%20PM.png" alt="Screenshot%205/24/13%201:54%20PM" width = 60% />
<hr>
<img src="https://www.evernote.com/shard/s10/sh/70fdac3f-eb29-4580-ad5c-4df3af8cd1e7/391d14510152050d860e73eceaacfd5e/deep/0/Screenshot%205/24/13%201:56%20PM.png" alt="Screenshot%205/24/13%201:56%20PM" width = 60% />
<hr>
<https://sqlshare.escience.washington.edu/sqlshare#s=query/sr320%40washington.edu/Snapshot%20of%20CDS%20GFF>
<hr>

Next step is to join the two files on Column9 (GeneID) and then change Start and Stop (C4 and C5) numbers so are able to map CDS (in the correct orientation - 5' 3') to the genes. Eventually hope to develop gene specific "genome browser".

**Left Join**

<img src="https://www.evernote.com/shard/s10/sh/8d833949-a09b-45be-b142-ffecaf902dc6/b9985e140715f5da74bdefd95e30bca9/deep/0/Screenshot%205/24/13%202:01%20PM.png" alt="Screenshot%205/24/13%202:01%20PM" width = 70%/>
<hr>


**Creating new GFF**

    SELECT
    cd.Column9 as seqname,  
    cd.Column2 as source,  
    cd.Column3 as feature, 
    
    Case when Column7 = '+'
    then Column4 - mRNA_start + 1
    Else mRNA_end - Column5 + 1
    END as start,
  
    Case when Column7 = '+'
    then Column5 - mRNA_start + 1
    Else mRNA_end - Column4 + 1
    END as [end],
  
    cd.Column6 as score,  
    cd.Column7 as strand,  
    cd.Column6 as frame,  
    cd.Column6 as attribute  
  
    FROM 
    [sr320@washington.edu].[CDS GFF with Gene start and stop] cd
   
    Order by Column1 Desc, Column9 --makes it easy to see big genes​​​
        
<hr>
<img src="https://www.evernote.com/shard/s10/sh/0bc75d35-ffc7-4293-89d6-723e74b60337/8c728ccaadf11a6c48034a215102ecd7/deep/0/Screenshot%205/26/13%202:41%20PM.jpg" alt="Screenshot%205/26/13%202:41%20PM" width = 60%/>
<hr>
<https://sqlshare.escience.washington.edu/sqlshare#s=query/sr320%40washington.edu/TJGR_GeneBased_CDS_GFF>
<hr>
Downloading file (CSV format)

<img src="https://www.evernote.com/shard/s10/sh/8a2740b3-9e17-47d5-925f-99dc586e3e0d/ea2aebf8dc0887184282f6f1e4d87c5d/deep/0/Screenshot%205/26/13%202:46%20PM.jpg" alt="Screenshot%205/26/13%202:46%20PM" width = 60% />
<hr>
Converting CSV to Tab-delimited

<img src="https://www.evernote.com/shard/s10/sh/fbda61f1-15de-4d91-ae26-4138cb040fce/796c298aa248ad59af99cef61eaadc24/deep/0/Screenshot%205/26/13%203:08%20PM.jpg" alt="Screenshot%205/26/13%203:08%20PM" width =70%/>
<hr>
In TextWrangler

<img src="https://www.evernote.com/shard/s10/sh/432e7a78-33b4-4195-b097-b2841a5d720e/bbc953dc5c16261cd6f995f361b9e4a4/deep/0/Screenshot%205/26/13%203:10%20PM.jpg" alt="Screenshot%205/26/13%203:10%20PM" width = 60%/>
<hr>
Visualize file in IGV

<img src="https://www.evernote.com/shard/s10/sh/f9519bf3-9eff-4ea2-88a7-52dfbed49c3b/df1c66c027d017f91d3e2cfe211ad1bc/deep/0/Screenshot%205/26/13%203:17%20PM.jpg" alt="Screenshot%205/26/13%203:17%20PM" width = 60% />
    
    
​