---
title: "Mendelian Randomization Analysis"
author: "Dr. Shea Andrews"
date: "2020-09-27"
output:
  html_document:
    df_print: paged
    keep_md: true
    toc: true
    number_sections: false
    toc_depth: 4
    toc_float:
      collapsed: false
      smooth_scroll: false
params:
  rwd: NA
  exposure.code: NA
  Exposure: NA
  exposure.snps: NA
  outcome.code: NA
  Outcome: NA
  outcome.snps: NA
  proxy.snps: NA
  harmonized.dat: NA
  p.threshold: NA
  r2.threshold: NA
  kb.threshold: NA
  mrpresso_global: NA
  mrpresso_global_wo_outliers: NA
  power: NA
  out: NA
editor_options:
  chunk_output_type: console
---






## Instrumental Variables
**SNP Inclusion:** SNPS associated with at a p-value threshold of p < 5e-8 were included in this analysis.
<br>

**LD Clumping:** For standard two sample MR it is important to ensure that the instruments for the exposure are independent. LD clumping was performed in PLINK using the EUR samples from the 1000 Genomes Project to estimate LD between SNPs, and, amongst SNPs that have an LD above a given threshold, retain only the SNP with the lowest p-value. A clumping window of 10^{4}, r2 of 0.001 and significance level of 1 was used for the index and secondary SNPs.
<br>

**Proxy SNPs:** Where SNPs were not available in the outcome GWAS, the EUR thousand genomes was queried to identify potential proxy SNPs that are in linkage disequilibrium (r2 > 0.8) of the missing SNP.
<br>

### Exposure: Cortical Surface Area
`#r exposure.blurb`
<br>

**Table 1:** Independent SNPs associated with Cortical Surface Area
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["SNP"],"name":[1],"type":["chr"],"align":["left"]},{"label":["CHROM"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["POS"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["REF"],"name":[4],"type":["chr"],"align":["left"]},{"label":["ALT"],"name":[5],"type":["chr"],"align":["left"]},{"label":["AF"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["BETA"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["SE"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["Z"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["P"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["N"],"name":[11],"type":["dbl"],"align":["right"]},{"label":["TRAIT"],"name":[12],"type":["chr"],"align":["left"]}],"data":[{"1":"rs12630663","2":"3","3":"28007315","4":"T","5":"C","6":"0.4117","7":"632.8110","8":"111.2125","9":"5.690110","10":"1.270e-08","11":"32176","12":"Cortical_Surface_Area"},{"1":"rs34464850","2":"3","3":"141721762","4":"G","5":"C","6":"0.1534","7":"1233.1854","8":"152.7201","9":"8.074807","10":"6.758e-16","11":"31984","12":"Cortical_Surface_Area"},{"1":"rs2301718","2":"4","3":"106009763","4":"G","5":"A","6":"0.2269","7":"737.2212","8":"132.3556","9":"5.570004","10":"2.547e-08","11":"32176","12":"Cortical_Surface_Area"},{"1":"rs386424","2":"5","3":"81092787","4":"T","5":"G","6":"0.3008","7":"656.5430","8":"120.0422","9":"5.469270","10":"4.519e-08","11":"32176","12":"Cortical_Surface_Area"},{"1":"rs7715167","2":"5","3":"170778824","4":"T","5":"C","6":"0.6143","7":"662.7540","8":"119.1375","9":"5.562930","10":"2.653e-08","11":"32068","12":"Cortical_Surface_Area"},{"1":"rs2802295","2":"6","3":"108926496","4":"A","5":"G","6":"0.6207","7":"714.5850","8":"112.9897","9":"6.324340","10":"2.543e-10","11":"32176","12":"Cortical_Surface_Area"},{"1":"rs11759026","2":"6","3":"126792095","4":"A","5":"G","6":"0.2376","7":"1301.5200","8":"134.6156","9":"9.668420","10":"4.106e-22","11":"31907","12":"Cortical_Surface_Area"},{"1":"rs12357321","2":"10","3":"21790476","4":"G","5":"A","6":"0.3206","7":"-698.7452","8":"119.6461","9":"-5.840100","10":"5.217e-09","11":"32176","12":"Cortical_Surface_Area"},{"1":"rs1628768","2":"10","3":"105012994","4":"T","5":"C","6":"0.2386","7":"972.9780","8":"132.0048","9":"7.370780","10":"1.696e-13","11":"32176","12":"Cortical_Surface_Area"},{"1":"rs10876864","2":"12","3":"56401085","4":"G","5":"A","6":"0.5774","7":"-628.5901","8":"112.6859","9":"-5.578250","10":"2.430e-08","11":"31319","12":"Cortical_Surface_Area"},{"1":"rs10878349","2":"12","3":"66327632","4":"A","5":"G","6":"0.5100","7":"-1039.9900","8":"110.4866","9":"-9.412850","10":"4.829e-21","11":"32176","12":"Cortical_Surface_Area"},{"1":"rs79600142","2":"17","3":"43897722","4":"T","5":"C","6":"0.2198","7":"-1696.8300","8":"143.2730","9":"-11.843300","10":"2.331e-32","11":"29435","12":"Cortical_Surface_Area"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

### Outcome: Insomnia
`#r outcome.blurb`
<br>

**Table 2:** SNPs associated with Cortical Surface Area avaliable in Insomnia
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["SNP"],"name":[1],"type":["chr"],"align":["left"]},{"label":["CHROM"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["POS"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["REF"],"name":[4],"type":["chr"],"align":["left"]},{"label":["ALT"],"name":[5],"type":["chr"],"align":["left"]},{"label":["AF"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["BETA"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["SE"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["Z"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["P"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["N"],"name":[11],"type":["dbl"],"align":["right"]},{"label":["TRAIT"],"name":[12],"type":["chr"],"align":["left"]}],"data":[{"1":"rs12630663","2":"3","3":"28007315","4":"T","5":"C","6":"0.374819","7":"1.033510e-03","8":"0.0008677692","9":"1.191","10":"2.338e-01","11":"1326797","12":"Insomnia_Symptoms"},{"1":"rs34464850","2":"3","3":"141721762","4":"G","5":"C","6":"0.151809","7":"-7.291637e-05","8":"0.0008680520","9":"-0.084","10":"9.332e-01","11":"1329560","12":"Insomnia_Symptoms"},{"1":"rs2301718","2":"4","3":"106009763","4":"G","5":"A","6":"0.281329","7":"-6.838907e-04","8":"0.0008700899","9":"-0.786","10":"4.316e-01","11":"1320626","12":"Insomnia_Symptoms"},{"1":"rs386424","2":"5","3":"81092787","4":"T","5":"G","6":"0.354704","7":"3.544970e-03","8":"0.0008656815","9":"4.095","10":"4.219e-05","11":"1327976","12":"Insomnia_Symptoms"},{"1":"rs7715167","2":"5","3":"170778824","4":"T","5":"C","6":"0.649726","7":"-3.150380e-03","8":"0.0008650143","9":"-3.642","10":"2.701e-04","11":"1330800","12":"Insomnia_Symptoms"},{"1":"rs2802295","2":"6","3":"108926496","4":"A","5":"G","6":"0.561291","7":"-2.254610e-03","8":"0.0008664921","9":"-2.602","10":"9.256e-03","11":"1328056","12":"Insomnia_Symptoms"},{"1":"rs11759026","2":"6","3":"126792095","4":"A","5":"G","6":"0.226251","7":"-2.732530e-03","8":"0.0008663688","9":"-3.154","10":"1.609e-03","11":"1327471","12":"Insomnia_Symptoms"},{"1":"rs12357321","2":"10","3":"21790476","4":"G","5":"A","6":"0.305707","7":"4.680887e-03","8":"0.0008681170","9":"5.392","10":"6.985e-08","11":"1318348","12":"Insomnia_Symptoms"},{"1":"rs1628768","2":"10","3":"105012994","4":"T","5":"C","6":"0.216795","7":"-2.440750e-03","8":"0.0008664371","9":"-2.817","10":"4.849e-03","11":"1327848","12":"Insomnia_Symptoms"},{"1":"rs10876864","2":"12","3":"56401085","4":"G","5":"A","6":"0.610867","7":"1.843449e-03","8":"0.0008658757","9":"2.129","10":"3.329e-02","11":"1330800","12":"Insomnia_Symptoms"},{"1":"rs10878349","2":"12","3":"66327632","4":"A","5":"G","6":"0.467672","7":"5.167530e-03","8":"0.0008645697","9":"5.977","10":"2.267e-09","11":"1328248","12":"Insomnia_Symptoms"},{"1":"rs79600142","2":"17","3":"43897722","4":"T","5":"C","6":"0.148256","7":"2.844460e-04","8":"0.0008672140","9":"0.328","10":"7.432e-01","11":"1330747","12":"Insomnia_Symptoms"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

**Table 3:** Proxy SNPs for Insomnia
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["proxy.outcome"],"name":[1],"type":["lgl"],"align":["right"]},{"label":["target_snp"],"name":[2],"type":["lgl"],"align":["right"]},{"label":["proxy_snp"],"name":[3],"type":["lgl"],"align":["right"]},{"label":["ld.r2"],"name":[4],"type":["lgl"],"align":["right"]},{"label":["Dprime"],"name":[5],"type":["lgl"],"align":["right"]},{"label":["ref.proxy"],"name":[6],"type":["lgl"],"align":["right"]},{"label":["alt.proxy"],"name":[7],"type":["lgl"],"align":["right"]},{"label":["CHROM"],"name":[8],"type":["lgl"],"align":["right"]},{"label":["POS"],"name":[9],"type":["lgl"],"align":["right"]},{"label":["ALT.proxy"],"name":[10],"type":["lgl"],"align":["right"]},{"label":["REF.proxy"],"name":[11],"type":["lgl"],"align":["right"]},{"label":["AF"],"name":[12],"type":["lgl"],"align":["right"]},{"label":["BETA"],"name":[13],"type":["lgl"],"align":["right"]},{"label":["SE"],"name":[14],"type":["lgl"],"align":["right"]},{"label":["P"],"name":[15],"type":["lgl"],"align":["right"]},{"label":["N"],"name":[16],"type":["lgl"],"align":["right"]},{"label":["ref"],"name":[17],"type":["lgl"],"align":["right"]},{"label":["alt"],"name":[18],"type":["lgl"],"align":["right"]},{"label":["ALT"],"name":[19],"type":["lgl"],"align":["right"]},{"label":["REF"],"name":[20],"type":["lgl"],"align":["right"]},{"label":["PHASE"],"name":[21],"type":["lgl"],"align":["right"]}],"data":[{"1":"NA","2":"NA","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

## Data harmonization
Harmonize the exposure and outcome datasets so that the effect of a SNP on the exposure and the effect of that SNP on the outcome correspond to the same allele. The harmonise_data function from the TwoSampleMR package can be used to perform the harmonization step, by default it try's to infer the forward strand alleles using allele frequency information.
<br>

**Table 4:** Harmonized Cortical Surface Area and Insomnia datasets
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["SNP"],"name":[1],"type":["chr"],"align":["left"]},{"label":["effect_allele.exposure"],"name":[2],"type":["chr"],"align":["left"]},{"label":["other_allele.exposure"],"name":[3],"type":["chr"],"align":["left"]},{"label":["effect_allele.outcome"],"name":[4],"type":["chr"],"align":["left"]},{"label":["other_allele.outcome"],"name":[5],"type":["chr"],"align":["left"]},{"label":["beta.exposure"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["beta.outcome"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["eaf.exposure"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["eaf.outcome"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["remove"],"name":[10],"type":["lgl"],"align":["right"]},{"label":["palindromic"],"name":[11],"type":["lgl"],"align":["right"]},{"label":["ambiguous"],"name":[12],"type":["lgl"],"align":["right"]},{"label":["id.outcome"],"name":[13],"type":["chr"],"align":["left"]},{"label":["chr.outcome"],"name":[14],"type":["dbl"],"align":["right"]},{"label":["pos.outcome"],"name":[15],"type":["dbl"],"align":["right"]},{"label":["se.outcome"],"name":[16],"type":["dbl"],"align":["right"]},{"label":["z.outcome"],"name":[17],"type":["dbl"],"align":["right"]},{"label":["pval.outcome"],"name":[18],"type":["dbl"],"align":["right"]},{"label":["samplesize.outcome"],"name":[19],"type":["dbl"],"align":["right"]},{"label":["outcome"],"name":[20],"type":["chr"],"align":["left"]},{"label":["mr_keep.outcome"],"name":[21],"type":["lgl"],"align":["right"]},{"label":["pval_origin.outcome"],"name":[22],"type":["chr"],"align":["left"]},{"label":["chr.exposure"],"name":[23],"type":["dbl"],"align":["right"]},{"label":["pos.exposure"],"name":[24],"type":["dbl"],"align":["right"]},{"label":["se.exposure"],"name":[25],"type":["dbl"],"align":["right"]},{"label":["z.exposure"],"name":[26],"type":["dbl"],"align":["right"]},{"label":["pval.exposure"],"name":[27],"type":["dbl"],"align":["right"]},{"label":["samplesize.exposure"],"name":[28],"type":["dbl"],"align":["right"]},{"label":["exposure"],"name":[29],"type":["chr"],"align":["left"]},{"label":["mr_keep.exposure"],"name":[30],"type":["lgl"],"align":["right"]},{"label":["pval_origin.exposure"],"name":[31],"type":["chr"],"align":["left"]},{"label":["id.exposure"],"name":[32],"type":["chr"],"align":["left"]},{"label":["action"],"name":[33],"type":["dbl"],"align":["right"]},{"label":["mr_keep"],"name":[34],"type":["lgl"],"align":["right"]},{"label":["pt"],"name":[35],"type":["dbl"],"align":["right"]},{"label":["pleitropy_keep"],"name":[36],"type":["lgl"],"align":["right"]},{"label":["mrpresso_RSSobs"],"name":[37],"type":["dbl"],"align":["right"]},{"label":["mrpresso_pval"],"name":[38],"type":["chr"],"align":["left"]},{"label":["mrpresso_keep"],"name":[39],"type":["lgl"],"align":["right"]}],"data":[{"1":"rs10876864","2":"A","3":"G","4":"A","5":"G","6":"-628.5901","7":"1.843449e-03","8":"0.5774","9":"0.610867","10":"FALSE","11":"FALSE","12":"FALSE","13":"miz4HH","14":"12","15":"56401085","16":"0.0008658757","17":"2.129","18":"3.329e-02","19":"1330800","20":"Jansen2018insomnia23andMe","21":"TRUE","22":"reported","23":"12","24":"56401085","25":"112.6859","26":"-5.578250","27":"2.430e-08","28":"31319","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"2kWqiF","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"1.303360e-06","38":"1","39":"TRUE"},{"1":"rs10878349","2":"G","3":"A","4":"G","5":"A","6":"-1039.9900","7":"5.167530e-03","8":"0.5100","9":"0.467672","10":"FALSE","11":"FALSE","12":"FALSE","13":"miz4HH","14":"12","15":"66327632","16":"0.0008645697","17":"5.977","18":"2.267e-09","19":"1328248","20":"Jansen2018insomnia23andMe","21":"TRUE","22":"reported","23":"12","24":"66327632","25":"110.4866","26":"-9.412850","27":"4.829e-21","28":"32176","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"2kWqiF","33":"2","34":"TRUE","35":"5e-08","36":"FALSE","37":"NA","38":"NA","39":"NA"},{"1":"rs11759026","2":"G","3":"A","4":"G","5":"A","6":"1301.5200","7":"-2.732530e-03","8":"0.2376","9":"0.226251","10":"FALSE","11":"FALSE","12":"FALSE","13":"miz4HH","14":"6","15":"126792095","16":"0.0008663688","17":"-3.154","18":"1.609e-03","19":"1327471","20":"Jansen2018insomnia23andMe","21":"TRUE","22":"reported","23":"6","24":"126792095","25":"134.6156","26":"9.668420","27":"4.106e-22","28":"31907","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"2kWqiF","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"2.027059e-06","38":"1","39":"TRUE"},{"1":"rs12357321","2":"A","3":"G","4":"A","5":"G","6":"-698.7452","7":"4.680887e-03","8":"0.3206","9":"0.305707","10":"FALSE","11":"FALSE","12":"FALSE","13":"miz4HH","14":"10","15":"21790476","16":"0.0008681170","17":"5.392","18":"6.985e-08","19":"1318348","20":"Jansen2018insomnia23andMe","21":"TRUE","22":"reported","23":"10","24":"21790476","25":"119.6461","26":"-5.840100","27":"5.217e-09","28":"32176","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"2kWqiF","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"1.635303e-05","38":"<0.0011","39":"FALSE"},{"1":"rs12630663","2":"C","3":"T","4":"C","5":"T","6":"632.8110","7":"1.033510e-03","8":"0.4117","9":"0.374819","10":"FALSE","11":"FALSE","12":"FALSE","13":"miz4HH","14":"3","15":"28007315","16":"0.0008677692","17":"1.191","18":"2.338e-01","19":"1326797","20":"Jansen2018insomnia23andMe","21":"TRUE","22":"reported","23":"3","24":"28007315","25":"111.2125","26":"5.690110","27":"1.270e-08","28":"32176","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"2kWqiF","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"3.448078e-06","38":"0.4092","39":"TRUE"},{"1":"rs1628768","2":"C","3":"T","4":"C","5":"T","6":"972.9780","7":"-2.440750e-03","8":"0.2386","9":"0.216795","10":"FALSE","11":"FALSE","12":"FALSE","13":"miz4HH","14":"10","15":"105012994","16":"0.0008664371","17":"-2.817","18":"4.849e-03","19":"1327848","20":"Jansen2018insomnia23andMe","21":"TRUE","22":"reported","23":"10","24":"105012994","25":"132.0048","26":"7.370780","27":"1.696e-13","28":"32176","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"2kWqiF","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"2.008566e-06","38":"1","39":"TRUE"},{"1":"rs2301718","2":"A","3":"G","4":"A","5":"G","6":"737.2212","7":"-6.838907e-04","8":"0.2269","9":"0.281329","10":"FALSE","11":"FALSE","12":"FALSE","13":"miz4HH","14":"4","15":"106009763","16":"0.0008700899","17":"-0.786","18":"4.316e-01","19":"1320626","20":"Jansen2018insomnia23andMe","21":"TRUE","22":"reported","23":"4","24":"106009763","25":"132.3556","26":"5.570004","27":"2.547e-08","28":"32176","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"2kWqiF","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"4.063304e-08","38":"1","39":"TRUE"},{"1":"rs2802295","2":"G","3":"A","4":"G","5":"A","6":"714.5850","7":"-2.254610e-03","8":"0.6207","9":"0.561291","10":"FALSE","11":"FALSE","12":"FALSE","13":"miz4HH","14":"6","15":"108926496","16":"0.0008664921","17":"-2.602","18":"9.256e-03","19":"1328056","20":"Jansen2018insomnia23andMe","21":"TRUE","22":"reported","23":"6","24":"108926496","25":"112.9897","26":"6.324340","27":"2.543e-10","28":"32176","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"2kWqiF","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"2.191841e-06","38":"0.9647","39":"TRUE"},{"1":"rs34464850","2":"C","3":"G","4":"C","5":"G","6":"1233.1854","7":"-7.291637e-05","8":"0.1534","9":"0.151809","10":"FALSE","11":"TRUE","12":"FALSE","13":"miz4HH","14":"3","15":"141721762","16":"0.0008680520","17":"-0.084","18":"9.332e-01","19":"1329560","20":"Jansen2018insomnia23andMe","21":"TRUE","22":"reported","23":"3","24":"141721762","25":"152.7201","26":"8.074807","27":"6.758e-16","28":"31984","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"2kWqiF","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"2.663865e-06","38":"0.8789","39":"TRUE"},{"1":"rs386424","2":"G","3":"T","4":"G","5":"T","6":"656.5430","7":"3.544970e-03","8":"0.3008","9":"0.354704","10":"FALSE","11":"FALSE","12":"FALSE","13":"miz4HH","14":"5","15":"81092787","16":"0.0008656815","17":"4.095","18":"4.219e-05","19":"1327976","20":"Jansen2018insomnia23andMe","21":"TRUE","22":"reported","23":"5","24":"81092787","25":"120.0422","26":"5.469270","27":"4.519e-08","28":"32176","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"2kWqiF","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"2.038141e-05","38":"<0.0011","39":"FALSE"},{"1":"rs7715167","2":"C","3":"T","4":"C","5":"T","6":"662.7540","7":"-3.150380e-03","8":"0.6143","9":"0.649726","10":"FALSE","11":"FALSE","12":"FALSE","13":"miz4HH","14":"5","15":"170778824","16":"0.0008650143","17":"-3.642","18":"2.701e-04","19":"1330800","20":"Jansen2018insomnia23andMe","21":"TRUE","22":"reported","23":"5","24":"170778824","25":"119.1375","26":"5.562930","27":"2.653e-08","28":"32068","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"2kWqiF","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"6.102278e-06","38":"0.0539","39":"TRUE"},{"1":"rs79600142","2":"C","3":"T","4":"C","5":"T","6":"-1696.8300","7":"2.844460e-04","8":"0.2198","9":"0.148256","10":"FALSE","11":"FALSE","12":"FALSE","13":"miz4HH","14":"17","15":"43897722","16":"0.0008672140","17":"0.328","18":"7.432e-01","19":"1330747","20":"Jansen2018insomnia23andMe","21":"TRUE","22":"reported","23":"17","24":"43897722","25":"143.2730","26":"-11.843300","27":"2.331e-32","28":"29435","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"2kWqiF","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"5.781469e-06","38":"0.3135","39":"TRUE"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

SNPs that genome-wide significant in the outcome GWAS are likely pleitorpic and should be removed from analysis. Additionaly remove variants within the APOE locus by exclude variants 1MB either side of APOE e4 (rs429358 = 19:45411941, GRCh37.p13)
<br>


**Table 5:** SNPs that were genome-wide significant in the Insomnia GWAS
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["SNP"],"name":[1],"type":["chr"],"align":["left"]},{"label":["chr.outcome"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["pos.outcome"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["pval.exposure"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["pval.outcome"],"name":[5],"type":["dbl"],"align":["right"]}],"data":[{"1":"rs10878349","2":"12","3":"66327632","4":"4.829e-21","5":"2.267e-09"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>


## Instrument Strength
To ensure that the first assumption of MR is not violated (Non-zero effect assumption), the genetic variants selected should be robustly associated with the exposure. Weak instruments, where the variance in the exposure explained by the the instruments is a small portion of the total variance, may result in poor precission and accuracy of the causal effect estiamte. The strength of an instrument can be evaluated using the F statistic, if F is less than 10, this is an indication of weak instrument.


```
## Parsed with column specification:
## cols(
##   .default = col_double(),
##   exposure = col_character(),
##   outcome = col_character(),
##   method = col_character(),
##   outliers_removed = col_logical(),
##   logistic = col_logical(),
##   beta = col_logical()
## )
```

```
## See spec(...) for full column specifications.
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["outliers_removed"],"name":[1],"type":["lgl"],"align":["right"]},{"label":["pve.exposure"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["F"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["Alpha"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["NCP"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["Power"],"name":[6],"type":["dbl"],"align":["right"]}],"data":[{"1":"FALSE","2":"0.01722786","3":"53.70035","4":"0.05","5":"1.465789","6":"0.2276089"},{"1":"TRUE","2":"0.01532379","3":"58.27031","4":"0.05","5":"1.360051","6":"0.2145555"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

##  MR Results
To obtain an overall estimate of causal effect, the SNP-exposure and SNP-outcome coefficients were combined in 1) a fixed-effects meta-analysis using an inverse-variance weighted approach (IVW); 2) a Weighted Median approach; 3) Weighted Mode approach and 4) Egger Regression.


[**IVW**](https://doi.org/10.1002/gepi.21758) is equivalent to a weighted regression of the SNP-outcome coefficients on the SNP-exposure coefficients with the intercept constrained to zero. This method assumes that all variants are valid instrumental variables based on the Mendelian randomization assumptions. The causal estimate of the IVW analysis expresses the causal increase in the outcome (or log odds of the outcome for a binary outcome) per unit change in the exposure. [**Weighted median MR**](https://doi.org/10.1002/gepi.21965) allows for 50% of the instrumental variables to be invalid. [**MR-Egger regression**](https://doi.org/10.1093/ije/dyw220) allows all the instrumental variables to be subject to direct effects (i.e. horizontal pleiotropy), with the intercept representing bias in the causal estimate due to pleiotropy and the slope representing the causal estimate. [**Weighted Mode**](https://doi.org/10.1093/ije/dyx102) gives consistent estimates as the sample size increases if a plurality (or weighted plurality) of the genetic variants are valid instruments.
<br>



Table 6 presents the MR causal estimates of genetically predicted Cortical Surface Area on Insomnia.
<br>

**Table 6** MR causaul estimates for Cortical Surface Area on Insomnia
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["method"],"name":[5],"type":["fctr"],"align":["left"]},{"label":["nsnp"],"name":[6],"type":["int"],"align":["right"]},{"label":["b"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["se"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[9],"type":["dbl"],"align":["right"]}],"data":[{"1":"2kWqiF","2":"miz4HH","3":"Jansen2018insomnia23andMe","4":"Grasby2020surfarea","5":"Inverse variance weighted (fixed effects)","6":"11","7":"-1.186687e-06","8":"2.708503e-07","9":"0.0000117952"},{"1":"2kWqiF","2":"miz4HH","3":"Jansen2018insomnia23andMe","4":"Grasby2020surfarea","5":"Weighted median","6":"11","7":"-6.291192e-07","8":"4.389836e-07","9":"0.1518215720"},{"1":"2kWqiF","2":"miz4HH","3":"Jansen2018insomnia23andMe","4":"Grasby2020surfarea","5":"Weighted mode","6":"11","7":"-7.982152e-07","8":"4.095644e-07","9":"0.0798890023"},{"1":"2kWqiF","2":"miz4HH","3":"Jansen2018insomnia23andMe","4":"Grasby2020surfarea","5":"MR Egger","6":"11","7":"7.428652e-08","8":"2.113778e-06","9":"0.9727320719"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

Figure 1 illustrates the SNP-specific associations with Cortical Surface Area versus the association in Insomnia and the corresponding MR estimates.
<br>

<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MR_ADPhenome/results/MR_ADbidir/Grasby2020surfarea/Jansen2018insomnia23andMe/Grasby2020surfarea_5e-8_Jansen2018insomnia23andMe_MR_Analaysis_files/figure-html/scatter_plot-1.png" alt="Fig. 1: Scatterplot of SNP effects for the association of the Exposure on the Outcome"  />
<p class="caption">Fig. 1: Scatterplot of SNP effects for the association of the Exposure on the Outcome</p>
</div>
<br>


## Pleiotropy
A Cochrans Q heterogeneity test can be used to formaly assesse for the presence of heterogenity (Table 7), with excessive heterogeneity indicating that there is a meaningful violation of at least one of the MR assumptions.
these assumptions..
<br>

**Table 7:** Heterogenity Tests
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["method"],"name":[5],"type":["fctr"],"align":["left"]},{"label":["Q"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["Q_df"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["Q_pval"],"name":[8],"type":["dbl"],"align":["right"]}],"data":[{"1":"2kWqiF","2":"miz4HH","3":"Jansen2018insomnia23andMe","4":"Grasby2020surfarea","5":"MR Egger","6":"68.16954","7":"9","8":"3.475585e-11"},{"1":"2kWqiF","2":"miz4HH","3":"Jansen2018insomnia23andMe","4":"Grasby2020surfarea","5":"Inverse variance weighted","6":"71.24788","7":"10","8":"2.544359e-11"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

Figure 2 shows a funnel plot displaying the MR estimates of individual genetic variants against their precession. Aysmmetry in the funnel plot may arrise due to some genetic variants having unusally strong effects on the outcome, which is indicative of directional pleiotropy.
<br>

<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MR_ADPhenome/results/MR_ADbidir/Grasby2020surfarea/Jansen2018insomnia23andMe/Grasby2020surfarea_5e-8_Jansen2018insomnia23andMe_MR_Analaysis_files/figure-html/funnel_plot-1.png" alt="Fig. 2: Funnel plot of the MR causal estimates against their precession"  />
<p class="caption">Fig. 2: Funnel plot of the MR causal estimates against their precession</p>
</div>
<br>

Figure 3 shows a [Radial Plots](https://github.com/WSpiller/RadialMR) can be used to visualize influential data points with large contributions to Cochran's Q Statistic that may bias causal effect estimates.



<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MR_ADPhenome/results/MR_ADbidir/Grasby2020surfarea/Jansen2018insomnia23andMe/Grasby2020surfarea_5e-8_Jansen2018insomnia23andMe_MR_Analaysis_files/figure-html/Radial_Plot-1.png" alt="Fig. 4: Radial Plot showing influential data points using Radial IVW"  />
<p class="caption">Fig. 4: Radial Plot showing influential data points using Radial IVW</p>
</div>
<br>

The intercept of the MR-Regression model captures the average pleitropic affect across all genetic variants (Table 8).
<br>

**Table 8:** MR Egger test for directional pleitropy
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["egger_intercept"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["se"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[7],"type":["dbl"],"align":["right"]}],"data":[{"1":"2kWqiF","2":"miz4HH","3":"Jansen2018insomnia23andMe","4":"Grasby2020surfarea","5":"-0.001300591","6":"0.002040122","7":"0.5396726"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

Pleiotropy was also assesed using Mendelian Randomization Pleiotropy RESidual Sum and Outlier [(MR-PRESSO)](https://doi.org/10.1038/s41588-018-0099-7), that allows for the evlation of evaluation of horizontal pleiotropy in a standared MR model (Table 9). MR-PRESSO performs a global test for detection of horizontal pleiotropy and correction of pleiotropy via outlier removal (Table 10).
<br>

**Table 9:** MR-PRESSO Global Test for pleitropy
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["chr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["chr"],"align":["left"]},{"label":["pt"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["outliers_removed"],"name":[6],"type":["lgl"],"align":["right"]},{"label":["n_outliers"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["RSSobs"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[9],"type":["chr"],"align":["left"]}],"data":[{"1":"2kWqiF","2":"miz4HH","3":"Jansen2018insomnia23andMe","4":"Grasby2020surfarea","5":"5e-08","6":"FALSE","7":"2","8":"82.9406","9":"<1e-04"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>


**Table 10:** MR Estimates after MR-PRESSO outlier removal
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["method"],"name":[5],"type":["fctr"],"align":["left"]},{"label":["nsnp"],"name":[6],"type":["int"],"align":["right"]},{"label":["b"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["se"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[9],"type":["dbl"],"align":["right"]}],"data":[{"1":"2kWqiF","2":"miz4HH","3":"Jansen2018insomnia23andMe","4":"Grasby2020surfarea","5":"Inverse variance weighted (fixed effects)","6":"9","7":"-1.204181e-06","8":"2.838850e-07","9":"2.217436e-05"},{"1":"2kWqiF","2":"miz4HH","3":"Jansen2018insomnia23andMe","4":"Grasby2020surfarea","5":"Weighted median","6":"9","7":"-6.322796e-07","8":"4.392420e-07","9":"1.500149e-01"},{"1":"2kWqiF","2":"miz4HH","3":"Jansen2018insomnia23andMe","4":"Grasby2020surfarea","5":"Weighted mode","6":"9","7":"-3.801672e-07","8":"4.711484e-07","9":"4.430526e-01"},{"1":"2kWqiF","2":"miz4HH","3":"Jansen2018insomnia23andMe","4":"Grasby2020surfarea","5":"MR Egger","6":"9","7":"5.585106e-07","8":"1.407335e-06","9":"7.032942e-01"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MR_ADPhenome/results/MR_ADbidir/Grasby2020surfarea/Jansen2018insomnia23andMe/Grasby2020surfarea_5e-8_Jansen2018insomnia23andMe_MR_Analaysis_files/figure-html/scatter_plot_outlier-1.png" alt="Fig. 5: Scatterplot of SNP effects for the association of the Exposure on the Outcome after outlier removal"  />
<p class="caption">Fig. 5: Scatterplot of SNP effects for the association of the Exposure on the Outcome after outlier removal</p>
</div>
<br>

**Table 11:** Heterogenity Tests after outlier removal
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["method"],"name":[5],"type":["fctr"],"align":["left"]},{"label":["Q"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["Q_df"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["Q_pval"],"name":[8],"type":["dbl"],"align":["right"]}],"data":[{"1":"2kWqiF","2":"miz4HH","3":"Jansen2018insomnia23andMe","4":"Grasby2020surfarea","5":"MR Egger","6":"21.19195","7":"7","8":"0.0034962066"},{"1":"2kWqiF","2":"miz4HH","3":"Jansen2018insomnia23andMe","4":"Grasby2020surfarea","5":"Inverse variance weighted","6":"26.60850","7":"8","8":"0.0008258386"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

**Table 12:** MR Egger test for directional pleitropy after outlier removal
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["egger_intercept"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["se"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[7],"type":["dbl"],"align":["right"]}],"data":[{"1":"2kWqiF","2":"miz4HH","3":"Jansen2018insomnia23andMe","4":"Grasby2020surfarea","5":"-0.001916433","6":"0.001432744","7":"0.2228513"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>
