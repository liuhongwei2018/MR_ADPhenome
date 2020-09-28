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

### Outcome: HDL cholesterol
`#r outcome.blurb`
<br>

**Table 2:** SNPs associated with Cortical Surface Area avaliable in HDL cholesterol
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["SNP"],"name":[1],"type":["chr"],"align":["left"]},{"label":["CHROM"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["POS"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["REF"],"name":[4],"type":["chr"],"align":["left"]},{"label":["ALT"],"name":[5],"type":["chr"],"align":["left"]},{"label":["AF"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["BETA"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["SE"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["Z"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["P"],"name":[10],"type":["dbl"],"align":["right"]},{"label":["N"],"name":[11],"type":["dbl"],"align":["right"]},{"label":["TRAIT"],"name":[12],"type":["chr"],"align":["left"]}],"data":[{"1":"rs12630663","2":"3","3":"28007315","4":"T","5":"C","6":"0.374819","7":"0.0022","8":"0.0049","9":"0.4489796","10":"0.8980","11":"94311","12":"HDL_Cholesterol"},{"1":"rs2301718","2":"4","3":"106009763","4":"G","5":"A","6":"0.281329","7":"-0.0062","8":"0.0056","9":"-1.1071400","10":"0.7018","11":"94232","12":"HDL_Cholesterol"},{"1":"rs386424","2":"5","3":"81092787","4":"T","5":"G","6":"0.354704","7":"0.0057","8":"0.0052","9":"1.0961538","10":"0.1587","11":"94311","12":"HDL_Cholesterol"},{"1":"rs7715167","2":"5","3":"170778824","4":"T","5":"C","6":"0.649726","7":"0.0045","8":"0.0053","9":"0.8490566","10":"0.2775","11":"94311","12":"HDL_Cholesterol"},{"1":"rs12357321","2":"10","3":"21790476","4":"G","5":"A","6":"0.305707","7":"-0.0069","8":"0.0053","9":"-1.3018900","10":"0.1700","11":"94311","12":"HDL_Cholesterol"},{"1":"rs10876864","2":"12","3":"56401085","4":"G","5":"A","6":"0.610867","7":"-0.0050","8":"0.0048","9":"-1.0416700","10":"0.1267","11":"94311","12":"HDL_Cholesterol"},{"1":"rs34464850","2":"NA","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA"},{"1":"rs2802295","2":"NA","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA"},{"1":"rs11759026","2":"NA","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA"},{"1":"rs1628768","2":"NA","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA"},{"1":"rs10878349","2":"NA","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA"},{"1":"rs79600142","2":"NA","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

**Table 3:** Proxy SNPs for HDL cholesterol
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["target_snp"],"name":[1],"type":["chr"],"align":["left"]},{"label":["proxy_snp"],"name":[2],"type":["chr"],"align":["left"]},{"label":["ld.r2"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["Dprime"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["PHASE"],"name":[5],"type":["chr"],"align":["left"]},{"label":["X12"],"name":[6],"type":["lgl"],"align":["right"]},{"label":["CHROM"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["POS"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["REF.proxy"],"name":[9],"type":["chr"],"align":["left"]},{"label":["ALT.proxy"],"name":[10],"type":["chr"],"align":["left"]},{"label":["AF"],"name":[11],"type":["dbl"],"align":["right"]},{"label":["BETA"],"name":[12],"type":["dbl"],"align":["right"]},{"label":["SE"],"name":[13],"type":["dbl"],"align":["right"]},{"label":["Z"],"name":[14],"type":["dbl"],"align":["right"]},{"label":["P"],"name":[15],"type":["dbl"],"align":["right"]},{"label":["N"],"name":[16],"type":["dbl"],"align":["right"]},{"label":["TRAIT"],"name":[17],"type":["chr"],"align":["left"]},{"label":["ref"],"name":[18],"type":["chr"],"align":["left"]},{"label":["ref.proxy"],"name":[19],"type":["chr"],"align":["left"]},{"label":["alt"],"name":[20],"type":["chr"],"align":["left"]},{"label":["alt.proxy"],"name":[21],"type":["chr"],"align":["left"]},{"label":["ALT"],"name":[22],"type":["chr"],"align":["left"]},{"label":["REF"],"name":[23],"type":["chr"],"align":["left"]},{"label":["proxy.outcome"],"name":[24],"type":["lgl"],"align":["right"]}],"data":[{"1":"rs34464850","2":"rs2271386","3":"1.000000","4":"1.000000","5":"CA/GG","6":"NA","7":"3","8":"141712708","9":"G","10":"A","11":"0.151945","12":"0.0072","13":"0.0065","14":"1.10769231","15":"0.2140","16":"94309.00","17":"HDL_Cholesterol","18":"C","19":"A","20":"G","21":"G","22":"C","23":"G","24":"TRUE"},{"1":"rs2802295","2":"rs2253310","3":"1.000000","4":"1.000000","5":"AC/GG","6":"NA","7":"6","8":"108888593","9":"C","10":"G","11":"0.561499","12":"-0.0134","13":"0.0049","14":"-2.73469000","15":"0.0119","16":"91278.00","17":"HDL_Cholesterol","18":"A","19":"C","20":"G","21":"G","22":"G","23":"A","24":"TRUE"},{"1":"rs1628768","2":"rs6584545","3":"0.973962","4":"0.994692","5":"CA/TT","6":"NA","7":"10","8":"104999266","9":"A","10":"T","11":"0.790532","12":"0.0022","13":"0.0055","14":"0.40000000","15":"0.7550","16":"92718.94","17":"HDL_Cholesterol","18":"C","19":"A","20":"T","21":"T","22":"T","23":"C","24":"TRUE"},{"1":"rs10878349","2":"rs1038196","3":"0.996002","4":"1.000000","5":"AG/GC","6":"NA","7":"12","8":"66343400","9":"G","10":"C","11":"0.467912","12":"0.0000","13":"0.0048","14":"0.00000000","15":"0.9341","16":"94311.00","17":"HDL_Cholesterol","18":"A","19":"G","20":"G","21":"C","22":"G","23":"A","24":"TRUE"},{"1":"rs79600142","2":"rs436667","3":"1.000000","4":"1.000000","5":"CT/TC","6":"NA","7":"17","8":"43709415","9":"C","10":"T","11":"0.146757","12":"0.0005","13":"0.0060","14":"0.08333333","15":"0.5358","16":"91319.00","17":"HDL_Cholesterol","18":"C","19":"T","20":"T","21":"C","22":"C","23":"T","24":"TRUE"},{"1":"rs11759026","2":"NA","3":"NA","4":"NA","5":"NA","6":"NA","7":"NA","8":"NA","9":"NA","10":"NA","11":"NA","12":"NA","13":"NA","14":"NA","15":"NA","16":"NA","17":"NA","18":"NA","19":"NA","20":"NA","21":"NA","22":"NA","23":"NA","24":"NA"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

## Data harmonization
Harmonize the exposure and outcome datasets so that the effect of a SNP on the exposure and the effect of that SNP on the outcome correspond to the same allele. The harmonise_data function from the TwoSampleMR package can be used to perform the harmonization step, by default it try's to infer the forward strand alleles using allele frequency information.
<br>

**Table 4:** Harmonized Cortical Surface Area and HDL cholesterol datasets
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["SNP"],"name":[1],"type":["chr"],"align":["left"]},{"label":["effect_allele.exposure"],"name":[2],"type":["chr"],"align":["left"]},{"label":["other_allele.exposure"],"name":[3],"type":["chr"],"align":["left"]},{"label":["effect_allele.outcome"],"name":[4],"type":["chr"],"align":["left"]},{"label":["other_allele.outcome"],"name":[5],"type":["chr"],"align":["left"]},{"label":["beta.exposure"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["beta.outcome"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["eaf.exposure"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["eaf.outcome"],"name":[9],"type":["dbl"],"align":["right"]},{"label":["remove"],"name":[10],"type":["lgl"],"align":["right"]},{"label":["palindromic"],"name":[11],"type":["lgl"],"align":["right"]},{"label":["ambiguous"],"name":[12],"type":["lgl"],"align":["right"]},{"label":["id.outcome"],"name":[13],"type":["chr"],"align":["left"]},{"label":["chr.outcome"],"name":[14],"type":["dbl"],"align":["right"]},{"label":["pos.outcome"],"name":[15],"type":["dbl"],"align":["right"]},{"label":["se.outcome"],"name":[16],"type":["dbl"],"align":["right"]},{"label":["z.outcome"],"name":[17],"type":["dbl"],"align":["right"]},{"label":["pval.outcome"],"name":[18],"type":["dbl"],"align":["right"]},{"label":["samplesize.outcome"],"name":[19],"type":["dbl"],"align":["right"]},{"label":["outcome"],"name":[20],"type":["chr"],"align":["left"]},{"label":["mr_keep.outcome"],"name":[21],"type":["lgl"],"align":["right"]},{"label":["pval_origin.outcome"],"name":[22],"type":["chr"],"align":["left"]},{"label":["chr.exposure"],"name":[23],"type":["dbl"],"align":["right"]},{"label":["pos.exposure"],"name":[24],"type":["dbl"],"align":["right"]},{"label":["se.exposure"],"name":[25],"type":["dbl"],"align":["right"]},{"label":["z.exposure"],"name":[26],"type":["dbl"],"align":["right"]},{"label":["pval.exposure"],"name":[27],"type":["dbl"],"align":["right"]},{"label":["samplesize.exposure"],"name":[28],"type":["dbl"],"align":["right"]},{"label":["exposure"],"name":[29],"type":["chr"],"align":["left"]},{"label":["mr_keep.exposure"],"name":[30],"type":["lgl"],"align":["right"]},{"label":["pval_origin.exposure"],"name":[31],"type":["chr"],"align":["left"]},{"label":["id.exposure"],"name":[32],"type":["chr"],"align":["left"]},{"label":["action"],"name":[33],"type":["dbl"],"align":["right"]},{"label":["mr_keep"],"name":[34],"type":["lgl"],"align":["right"]},{"label":["pt"],"name":[35],"type":["dbl"],"align":["right"]},{"label":["pleitropy_keep"],"name":[36],"type":["lgl"],"align":["right"]},{"label":["mrpresso_RSSobs"],"name":[37],"type":["lgl"],"align":["right"]},{"label":["mrpresso_pval"],"name":[38],"type":["lgl"],"align":["right"]},{"label":["mrpresso_keep"],"name":[39],"type":["lgl"],"align":["right"]}],"data":[{"1":"rs10876864","2":"A","3":"G","4":"A","5":"G","6":"-628.5901","7":"-0.0050","8":"0.5774","9":"0.610867","10":"FALSE","11":"FALSE","12":"FALSE","13":"cQj2lM","14":"12","15":"56401085","16":"0.0048","17":"-1.04167000","18":"0.1267","19":"94311.00","20":"Willer2013hdl","21":"TRUE","22":"reported","23":"12","24":"56401085","25":"112.6859","26":"-5.578250","27":"2.430e-08","28":"31319","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"ylco6u","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs10878349","2":"G","3":"A","4":"G","5":"A","6":"-1039.9900","7":"0.0000","8":"0.5100","9":"0.467912","10":"FALSE","11":"FALSE","12":"FALSE","13":"cQj2lM","14":"12","15":"66343400","16":"0.0048","17":"0.00000000","18":"0.9341","19":"94311.00","20":"Willer2013hdl","21":"TRUE","22":"reported","23":"12","24":"66327632","25":"110.4866","26":"-9.412850","27":"4.829e-21","28":"32176","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"ylco6u","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs12357321","2":"A","3":"G","4":"A","5":"G","6":"-698.7452","7":"-0.0069","8":"0.3206","9":"0.305707","10":"FALSE","11":"FALSE","12":"FALSE","13":"cQj2lM","14":"10","15":"21790476","16":"0.0053","17":"-1.30189000","18":"0.1700","19":"94311.00","20":"Willer2013hdl","21":"TRUE","22":"reported","23":"10","24":"21790476","25":"119.6461","26":"-5.840100","27":"5.217e-09","28":"32176","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"ylco6u","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs12630663","2":"C","3":"T","4":"C","5":"T","6":"632.8110","7":"0.0022","8":"0.4117","9":"0.374819","10":"FALSE","11":"FALSE","12":"FALSE","13":"cQj2lM","14":"3","15":"28007315","16":"0.0049","17":"0.44897959","18":"0.8980","19":"94311.00","20":"Willer2013hdl","21":"TRUE","22":"reported","23":"3","24":"28007315","25":"111.2125","26":"5.690110","27":"1.270e-08","28":"32176","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"ylco6u","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs1628768","2":"C","3":"T","4":"C","5":"T","6":"972.9780","7":"-0.0022","8":"0.2386","9":"0.209468","10":"FALSE","11":"FALSE","12":"FALSE","13":"cQj2lM","14":"10","15":"104999266","16":"0.0055","17":"0.40000000","18":"0.7550","19":"92718.94","20":"Willer2013hdl","21":"TRUE","22":"reported","23":"10","24":"105012994","25":"132.0048","26":"7.370780","27":"1.696e-13","28":"32176","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"ylco6u","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs2301718","2":"A","3":"G","4":"A","5":"G","6":"737.2212","7":"-0.0062","8":"0.2269","9":"0.281329","10":"FALSE","11":"FALSE","12":"FALSE","13":"cQj2lM","14":"4","15":"106009763","16":"0.0056","17":"-1.10714000","18":"0.7018","19":"94232.00","20":"Willer2013hdl","21":"TRUE","22":"reported","23":"4","24":"106009763","25":"132.3556","26":"5.570004","27":"2.547e-08","28":"32176","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"ylco6u","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs2802295","2":"G","3":"A","4":"G","5":"A","6":"714.5850","7":"-0.0134","8":"0.6207","9":"0.561499","10":"FALSE","11":"FALSE","12":"FALSE","13":"cQj2lM","14":"6","15":"108888593","16":"0.0049","17":"-2.73469000","18":"0.0119","19":"91278.00","20":"Willer2013hdl","21":"TRUE","22":"reported","23":"6","24":"108926496","25":"112.9897","26":"6.324340","27":"2.543e-10","28":"32176","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"ylco6u","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs34464850","2":"C","3":"G","4":"C","5":"G","6":"1233.1854","7":"0.0072","8":"0.1534","9":"0.151945","10":"FALSE","11":"TRUE","12":"FALSE","13":"cQj2lM","14":"3","15":"141712708","16":"0.0065","17":"1.10769231","18":"0.2140","19":"94309.00","20":"Willer2013hdl","21":"TRUE","22":"reported","23":"3","24":"141721762","25":"152.7201","26":"8.074807","27":"6.758e-16","28":"31984","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"ylco6u","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs386424","2":"G","3":"T","4":"G","5":"T","6":"656.5430","7":"0.0057","8":"0.3008","9":"0.354704","10":"FALSE","11":"FALSE","12":"FALSE","13":"cQj2lM","14":"5","15":"81092787","16":"0.0052","17":"1.09615385","18":"0.1587","19":"94311.00","20":"Willer2013hdl","21":"TRUE","22":"reported","23":"5","24":"81092787","25":"120.0422","26":"5.469270","27":"4.519e-08","28":"32176","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"ylco6u","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs7715167","2":"C","3":"T","4":"C","5":"T","6":"662.7540","7":"0.0045","8":"0.6143","9":"0.649726","10":"FALSE","11":"FALSE","12":"FALSE","13":"cQj2lM","14":"5","15":"170778824","16":"0.0053","17":"0.84905660","18":"0.2775","19":"94311.00","20":"Willer2013hdl","21":"TRUE","22":"reported","23":"5","24":"170778824","25":"119.1375","26":"5.562930","27":"2.653e-08","28":"32068","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"ylco6u","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"},{"1":"rs79600142","2":"C","3":"T","4":"C","5":"T","6":"-1696.8300","7":"0.0005","8":"0.2198","9":"0.146757","10":"FALSE","11":"FALSE","12":"FALSE","13":"cQj2lM","14":"17","15":"43709415","16":"0.0060","17":"0.08333333","18":"0.5358","19":"91319.00","20":"Willer2013hdl","21":"TRUE","22":"reported","23":"17","24":"43897722","25":"143.2730","26":"-11.843300","27":"2.331e-32","28":"29435","29":"Grasby2020surfarea","30":"TRUE","31":"reported","32":"ylco6u","33":"2","34":"TRUE","35":"5e-08","36":"TRUE","37":"NA","38":"NA","39":"TRUE"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

SNPs that genome-wide significant in the outcome GWAS are likely pleitorpic and should be removed from analysis. Additionaly remove variants within the APOE locus by exclude variants 1MB either side of APOE e4 (rs429358 = 19:45411941, GRCh37.p13)
<br>


**Table 5:** SNPs that were genome-wide significant in the HDL cholesterol GWAS
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["SNP"],"name":[1],"type":["chr"],"align":["left"]},{"label":["chr.outcome"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["pos.outcome"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["pval.exposure"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["pval.outcome"],"name":[5],"type":["dbl"],"align":["right"]}],"data":[],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
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
##   k.outcome = col_logical(),
##   method = col_character(),
##   outliers_removed = col_logical(),
##   logistic = col_logical(),
##   or = col_logical()
## )
```

```
## See spec(...) for full column specifications.
```

<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["outliers_removed"],"name":[1],"type":["lgl"],"align":["right"]},{"label":["pve.exposure"],"name":[2],"type":["dbl"],"align":["right"]},{"label":["F"],"name":[3],"type":["dbl"],"align":["right"]},{"label":["Alpha"],"name":[4],"type":["dbl"],"align":["right"]},{"label":["NCP"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["Power"],"name":[6],"type":["dbl"],"align":["right"]}],"data":[{"1":"FALSE","2":"0.01726749","3":"53.82604","4":"0.05","5":"0.3497698","6":"0.0909348"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>

##  MR Results
To obtain an overall estimate of causal effect, the SNP-exposure and SNP-outcome coefficients were combined in 1) a fixed-effects meta-analysis using an inverse-variance weighted approach (IVW); 2) a Weighted Median approach; 3) Weighted Mode approach and 4) Egger Regression.


[**IVW**](https://doi.org/10.1002/gepi.21758) is equivalent to a weighted regression of the SNP-outcome coefficients on the SNP-exposure coefficients with the intercept constrained to zero. This method assumes that all variants are valid instrumental variables based on the Mendelian randomization assumptions. The causal estimate of the IVW analysis expresses the causal increase in the outcome (or log odds of the outcome for a binary outcome) per unit change in the exposure. [**Weighted median MR**](https://doi.org/10.1002/gepi.21965) allows for 50% of the instrumental variables to be invalid. [**MR-Egger regression**](https://doi.org/10.1093/ije/dyw220) allows all the instrumental variables to be subject to direct effects (i.e. horizontal pleiotropy), with the intercept representing bias in the causal estimate due to pleiotropy and the slope representing the causal estimate. [**Weighted Mode**](https://doi.org/10.1093/ije/dyx102) gives consistent estimates as the sample size increases if a plurality (or weighted plurality) of the genetic variants are valid instruments.
<br>



Table 6 presents the MR causal estimates of genetically predicted Cortical Surface Area on HDL cholesterol.
<br>

**Table 6** MR causaul estimates for Cortical Surface Area on HDL cholesterol
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["method"],"name":[5],"type":["fctr"],"align":["left"]},{"label":["nsnp"],"name":[6],"type":["int"],"align":["right"]},{"label":["b"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["se"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[9],"type":["dbl"],"align":["right"]}],"data":[{"1":"ylco6u","2":"cQj2lM","3":"Willer2013hdl","4":"Grasby2020surfarea","5":"Inverse variance weighted (fixed effects)","6":"11","7":"5.762648e-07","8":"1.780054e-06","9":"0.7461391"},{"1":"ylco6u","2":"cQj2lM","3":"Willer2013hdl","4":"Grasby2020surfarea","5":"Weighted median","6":"11","7":"-6.994483e-08","8":"2.483068e-06","9":"0.9775276"},{"1":"ylco6u","2":"cQj2lM","3":"Willer2013hdl","4":"Grasby2020surfarea","5":"Weighted mode","6":"11","7":"4.841459e-07","8":"2.925844e-06","9":"0.8718697"},{"1":"ylco6u","2":"cQj2lM","3":"Willer2013hdl","4":"Grasby2020surfarea","5":"MR Egger","6":"11","7":"-9.370220e-07","8":"6.940732e-06","9":"0.8955803"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

Figure 1 illustrates the SNP-specific associations with Cortical Surface Area versus the association in HDL cholesterol and the corresponding MR estimates.
<br>

<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MR_ADPhenome/results/MR_ADbidir/Grasby2020surfarea/Willer2013hdl/Grasby2020surfarea_5e-8_Willer2013hdl_MR_Analaysis_files/figure-html/scatter_plot-1.png" alt="Fig. 1: Scatterplot of SNP effects for the association of the Exposure on the Outcome"  />
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
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["method"],"name":[5],"type":["fctr"],"align":["left"]},{"label":["Q"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["Q_df"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["Q_pval"],"name":[8],"type":["dbl"],"align":["right"]}],"data":[{"1":"ylco6u","2":"cQj2lM","3":"Willer2013hdl","4":"Grasby2020surfarea","5":"MR Egger","6":"14.80973","7":"9","8":"0.09629663"},{"1":"ylco6u","2":"cQj2lM","3":"Willer2013hdl","4":"Grasby2020surfarea","5":"Inverse variance weighted","6":"14.89745","7":"10","8":"0.13584560"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

Figure 2 shows a funnel plot displaying the MR estimates of individual genetic variants against their precession. Aysmmetry in the funnel plot may arrise due to some genetic variants having unusally strong effects on the outcome, which is indicative of directional pleiotropy.
<br>

<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MR_ADPhenome/results/MR_ADbidir/Grasby2020surfarea/Willer2013hdl/Grasby2020surfarea_5e-8_Willer2013hdl_MR_Analaysis_files/figure-html/funnel_plot-1.png" alt="Fig. 2: Funnel plot of the MR causal estimates against their precession"  />
<p class="caption">Fig. 2: Funnel plot of the MR causal estimates against their precession</p>
</div>
<br>

Figure 3 shows a [Radial Plots](https://github.com/WSpiller/RadialMR) can be used to visualize influential data points with large contributions to Cochran's Q Statistic that may bias causal effect estimates.




```
## [1] "No significant Outliers"
```

<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MR_ADPhenome/results/MR_ADbidir/Grasby2020surfarea/Willer2013hdl/Grasby2020surfarea_5e-8_Willer2013hdl_MR_Analaysis_files/figure-html/Radial_Plot-1.png" alt="Fig. 4: Radial Plot showing influential data points using Radial IVW"  />
<p class="caption">Fig. 4: Radial Plot showing influential data points using Radial IVW</p>
</div>
<br>

The intercept of the MR-Regression model captures the average pleitropic affect across all genetic variants (Table 8).
<br>

**Table 8:** MR Egger test for directional pleitropy
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["egger_intercept"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["se"],"name":[6],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[7],"type":["dbl"],"align":["right"]}],"data":[{"1":"ylco6u","2":"cQj2lM","3":"Willer2013hdl","4":"Grasby2020surfarea","5":"0.001432982","6":"0.006206554","7":"0.8225695"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

Pleiotropy was also assesed using Mendelian Randomization Pleiotropy RESidual Sum and Outlier [(MR-PRESSO)](https://doi.org/10.1038/s41588-018-0099-7), that allows for the evlation of evaluation of horizontal pleiotropy in a standared MR model (Table 9). MR-PRESSO performs a global test for detection of horizontal pleiotropy and correction of pleiotropy via outlier removal (Table 10).
<br>

**Table 9:** MR-PRESSO Global Test for pleitropy
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["chr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["chr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["chr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["chr"],"align":["left"]},{"label":["pt"],"name":[5],"type":["dbl"],"align":["right"]},{"label":["outliers_removed"],"name":[6],"type":["lgl"],"align":["right"]},{"label":["n_outliers"],"name":[7],"type":["dbl"],"align":["right"]},{"label":["RSSobs"],"name":[8],"type":["dbl"],"align":["right"]},{"label":["pval"],"name":[9],"type":["dbl"],"align":["right"]}],"data":[{"1":"ylco6u","2":"cQj2lM","3":"Willer2013hdl","4":"Grasby2020surfarea","5":"5e-08","6":"FALSE","7":"0","8":"17.126","9":"0.1714"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>


**Table 10:** MR Estimates after MR-PRESSO outlier removal
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["fctr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["method"],"name":[5],"type":["fctr"],"align":["left"]},{"label":["nsnp"],"name":[6],"type":["lgl"],"align":["right"]},{"label":["b"],"name":[7],"type":["lgl"],"align":["right"]},{"label":["se"],"name":[8],"type":["lgl"],"align":["right"]},{"label":["pval"],"name":[9],"type":["lgl"],"align":["right"]}],"data":[{"1":"ylco6u","2":"cQj2lM","3":"Willer2013hdl","4":"Grasby2020surfarea","5":"mrpresso","6":"NA","7":"NA","8":"NA","9":"NA"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

<div class="figure" style="text-align: center">
<img src="/sc/arion/projects/LOAD/shea/Projects/MR_ADPhenome/results/MR_ADbidir/Grasby2020surfarea/Willer2013hdl/Grasby2020surfarea_5e-8_Willer2013hdl_MR_Analaysis_files/figure-html/scatter_plot_outlier-1.png" alt="Fig. 5: Scatterplot of SNP effects for the association of the Exposure on the Outcome after outlier removal"  />
<p class="caption">Fig. 5: Scatterplot of SNP effects for the association of the Exposure on the Outcome after outlier removal</p>
</div>
<br>

**Table 11:** Heterogenity Tests after outlier removal
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["fctr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["method"],"name":[5],"type":["fctr"],"align":["left"]},{"label":["Q"],"name":[6],"type":["lgl"],"align":["right"]},{"label":["Q_df"],"name":[7],"type":["lgl"],"align":["right"]},{"label":["Q_pval"],"name":[8],"type":["lgl"],"align":["right"]}],"data":[{"1":"ylco6u","2":"cQj2lM","3":"Willer2013hdl","4":"Grasby2020surfarea","5":"mrpresso","6":"NA","7":"NA","8":"NA"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>

**Table 12:** MR Egger test for directional pleitropy after outlier removal
<div data-pagedtable="false">
  <script data-pagedtable-source type="application/json">
{"columns":[{"label":["id.exposure"],"name":[1],"type":["fctr"],"align":["left"]},{"label":["id.outcome"],"name":[2],"type":["fctr"],"align":["left"]},{"label":["outcome"],"name":[3],"type":["fctr"],"align":["left"]},{"label":["exposure"],"name":[4],"type":["fctr"],"align":["left"]},{"label":["method"],"name":[5],"type":["fctr"],"align":["left"]},{"label":["egger_intercept"],"name":[6],"type":["lgl"],"align":["right"]},{"label":["se"],"name":[7],"type":["lgl"],"align":["right"]},{"label":["pval"],"name":[8],"type":["lgl"],"align":["right"]}],"data":[{"1":"ylco6u","2":"cQj2lM","3":"Willer2013hdl","4":"Grasby2020surfarea","5":"mrpresso","6":"NA","7":"NA","8":"NA"}],"options":{"columns":{"min":{},"max":[10]},"rows":{"min":[10],"max":[10]},"pages":{}}}
  </script>
</div>
<br>
