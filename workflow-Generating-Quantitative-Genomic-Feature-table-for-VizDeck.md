This workflow how to take a table quantitative information on a genomic feature and bring into VizDeck. Specifically a gff format table with DNA methylation information will be joing with functional and gene characteristic information.

In this instance I will start with the query first:

    SELECT 
    seqname,
    start as CpG_pos,
    CAST(start AS FLOAT(1))/(mRNA.column5 - mRNA.column4)*100 as Rel_CpG_pos,
    score as methratio,
    term,
    GOSlim_bin,
    aspect,
    mRNA.column5 - mRNA.column4 as mRNA_length 
  
    FROM [sr320@washington.edu].[BiGill_methratio_Gene_Genomic_GFF] gff
    left join [sr320@washington.edu].[qDOD_Cgigas_GO_GOslim] des
    ​on gff.seqname = des.CGI_ID
    left join [sr320@washington.edu].[oyster_v9_mRNA GFF] mRNA
    on gff.seqname = mRNA.Column9
 
    Order by mRNA_length desc

Explanation: The _gff_ was joined with _des_ (to get gene function) and _mRNA_ to indirectly obtain gene length.

Below are snapshots and links to the tables.

<img src="https://www.evernote.com/shard/s10/sh/8dd06173-b203-4091-ab6b-1b1d77400303/d4d4f97d1b8b4c5ae6509ae13deb1c38/deep/0/Screenshot%205/25/13%209:09%20AM.jpg" alt="Screenshot%205/25/13%209:09%20AM" width = 50%/>
<hr>
<https://sqlshare.escience.washington.edu/sqlshare#s=query/sr320%40washington.edu/BiGill_methratio_Gene_Genomic_GFF>
<hr>
<img src="https://www.evernote.com/shard/s10/sh/8bfcd8f1-f4b5-4575-b273-3b008921ba47/333e762dcf5bad94532daea8bd10c10a/deep/0/Screenshot%205/25/13%209:10%20AM.jpg" alt="Screenshot%205/25/13%209:10%20AM" width = 80%/>
<hr>
<https://sqlshare.escience.washington.edu/sqlshare#s=query/sr320%40washington.edu/qDOD_Cgigas_GO_GOslim>
<hr>
<img src="https://www.evernote.com/shard/s10/sh/307d60f1-6fd4-4ff6-8a9e-06b61e9d9428/930ce97eba060efd0071af347ae2c382/deep/0/Screenshot%205/25/13%209:13%20AM.jpg" alt="Screenshot%205/25/13%209:13%20AM" width = 50%  />
<hr>
<https://sqlshare.escience.washington.edu/sqlshare#s=query/sr320%40washington.edu/oyster_v9_mRNA%20GFF>
<hr>

###Resulting table
<img src="https://www.evernote.com/shard/s10/sh/8c37fe5a-f214-484b-927c-12bfe0e71e05/23572312ac5d034f3c04307a10371035/deep/0/Screenshot%205/25/13%209:18%20AM.jpg" alt="Screenshot%205/25/13%209:18%20AM" width = 80% />
<hr>
<https://sqlshare.escience.washington.edu/sqlshare#s=query/sr320%40washington.edu/BiGill_Gene_Methratio_VD>
<hr>
