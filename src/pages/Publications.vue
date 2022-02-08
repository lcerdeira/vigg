<template>
  <q-page class="row justify-center">
    <div class="col-10 row justify-between q-my-md" style="max-width: 1000px">
      <div v-for="(pub, index) in publications" :key="index+'pub'" class="column">
        <q-card
          class="my-card col-grow column justify-between"
          :class="$q.platform.is.mobile ? 'q-my-md' : 'q-ma-md'"
          :style="{ width: $q.platform.is.mobile ? '100%' : '300px'}"
        >
          <!-- <q-btn
            flat
            dense
            style="text-transform: none"
            class="q-pa-none q-pa-sm column col-grow"
          >
          </q-btn> -->
          <q-card-section class="column">
              <div class="text-h6 q-pb-sm text-justify">{{pub.title}}</div>
              <div class="text-subtitle2 text-left" style="fontWeight: bold">{{pub.authors}}</div>
          </q-card-section>

          <q-card-actions vertical>
            <q-separator />
            <q-btn @click="openURL(pub.doi)" flat class="text-weight-bold" color="cyan">See publication</q-btn>
          </q-card-actions>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script>

const publications = [
  {
    title: 'Impact of seasonality and malaria control interventions on Anopheles density and species composition from three areas of Uganda with differing malaria endemicity',
    authors: 'Mawejje, Henry Ddumba, et al. (2021)',
    doi: 'https://doi.org/10.1186/s12936-021-03675-5'
  },
  {
    title: 'The genetic architecture of target‐site resistance to pyrethroid insecticides in the African malaria vectors Anopheles gambiae and Anopheles coluzzii',
    authors: 'Clarkson, Chris S., et al. (2021)',
    doi: 'https://doi.org/10.1111/mec.15845'
  },
  {
    title: 'Identification of a rapidly-spreading triple mutant for high-level metabolic insecticide resistance in Anopheles gambiae provides a real-time molecular diagnostic for anti-malarial intervention deployment',
    authors: 'Njoroge, H., et al. (2021)',
    doi: 'https://doi.org/10.1101/2021.02.11.429702'
  },
  {
    title: 'Resistance to pirimiphos-methyl in West African Anopheles is spreading via duplication and introgression of the Ace1 locus',
    authors: 'Grau-Bové, X., et al. (2021)',
    doi: 'https://doi.org/10.1371/journal.pgen.1009253'
  },
  {
    title: 'Cost-effectiveness analysis of PBO-LLINs compared to Non PBO LLINs in the reduction of malaria among children in Jinja district',
    authors: 'Kaakyo, M., et al. (2020)',
    doi: 'https://doi.org/10.1016/j.ijid.2020.09.799'
  },
  {
    title: 'Effect of long-lasting insecticidal nets with and without piperonyl butoxide on malaria indicators in Uganda (LLINEUP): a pragmatic, cluster-randomised trial embedded in a national LLIN distribution campaign',
    authors: 'Staedke, S. G., et al. (2020)',
    doi: 'https://doi.org/10.1016/S0140-6736(20)30214-2'
  },
  {
    title: 'Evolution of the insecticide target Rdl in African Anopheles is driven by interspecific and interkaryotypic introgression',
    authors: 'Grau-Bové, X.,et al. (2020)',
    doi: 'https://doi.org/10.1093/molbev/msaa128'
  },
  {
    title: 'Genome variation and population structure among 1,142 mosquitoes of the African malaria vector species Anopheles gambiae and Anopheles coluzzii',
    authors: 'The Anopheles gambiae 1000 Genomes Consortium (2020)',
    doi: 'https://doi.org/10.1101/gr.262790.120'
  },
  {
    title: 'Whole genome sequencing reveals high complexity of copy number variation at insecticide resistance loci in malaria mosquitoes',
    authors: 'Lucas, E. R., et al. (2019)',
    doi: 'https://doi.org/10.1101/gr.245795.118'
  },
  {
    title: 'A high throughput multi-locus insecticide resistance marker panel for tracking resistance emergence and spread in Anopheles gambiae',
    authors: 'Lucas, E. R., et al. (2019)',
    doi: 'https://doi.org/10.1038/s41598-019-49892-6'
  },
  {
    title: 'Candidate-gene based GWAS identifies reproducible DNA markers for metabolic pyrethroid resistance from standing genetic variation in East African Anopheles gambiae (in press)',
    authors: 'Weetman, D., et al. (2018)',
    doi: 'https://doi.org/10.1038/s41598-018-21265-5'
  },
  {
    title: 'Genetic diversity of the African malaria vector Anopheles gambiae',
    authors: 'The Anopheles gambiae 1000 Genomes Consortium (2017)',
    doi: 'https://doi.org/10.1038/nature24995'
  },
  {
    title: 'Insecticide-Treated Nets and Protection against Insecticide-Resistant Malaria Vectors in Western Kenya',
    authors: 'Ochomo, E., et al. (2017)',
    doi: 'https://doi.org/10.3201/eid2305.161315'
  },
  {
    title: 'A significant association between deltamethrin resistance, Plasmodium falciparum infection and the Vgsc-1014S resistance mutation in Anopheles gambiae highlights the epidemiological importance of resistance markers',
    authors: 'Kabula, B., et al. (2016)',
    doi: 'https://doi.org/10.1186/s12936-016-1331-5'
  },
  {
    title: 'Identification, validation, and application of molecular diagnostics for insecticide resistance in malaria vectors',
    authors: 'Donnelly, M.J., Isaacs, A.T., Weetman, D. (2016) ',
    doi: 'https://doi.org/10.1016/j.pt.2015.12.001'
  },
  {
    title: 'Presence of the knockdown resistance mutation, Vgsc-1014F in Anopheles gambiae and An. arabiensis in western Kenya',
    authors: 'Ochomo, E., et al. (2015)',
    doi: 'https://doi.org/10.1186/s13071-015-1223-5'
  },
  {
    title: 'Estimation of allele-specific Ace-1 duplication in insecticide-resistant Anopheles mosquitoes from West Africa',
    authors: 'Djogbénou, L.S., et al. (2015)',
    doi: 'https://doi.org/10.1186/s12936-015-1026-3'
  },
  {
    title: 'Contemporary evolution of resistance at the major insecticide target site gene Ace-1 by mutation and copy number variation in the malaria mosquito Anopheles gambiae',
    authors: 'Weetman, D., et al. (2015)',
    content: 'Functionally constrained genes are ideal insecticide targets because disruption is often fatal, and resistance mutations are typically costly. Synaptic acetylcholinesterase (AChE) is an essential neurotransmission enzyme targeted by insecticides used increasingly in malaria control. In Anopheles and Culex mosquitoes, a glycine-serine substitution at codon 119 of the Ace-1 gene confers both resistance and fitness costs, especially for 119S/S homozygotes. G119S in Anopheles gambiae from Accra (Ghana) is strongly associated with resistance, and, despite expectations of cost, resistant 119S alleles are increasing significantly in frequency. Sequencing of Accra females detected only a single Ace-1 119S haplotype, whereas 119G diversity was high overall but very low at non-synonymous sites, evidence of strong purifying selection driven by functional constraint. Flanking microsatellites showed reduced diversity, elevated linkage disequilibrium and high differentiation of 119S, relative to 119G homozygotes across up to two megabases of the genome. Yet these signals of selection were inconsistent and sometimes weak tens of kilobases from Ace-1. This unexpected finding is attributable to apparently ubiquitous amplification of 119S alleles as part of a large copy number variant (CNV) far exceeding the size of the Ace-1 gene, whereas 119G alleles were unduplicated. Ace-1 CNV was detectable in archived samples collected when the 119S allele was rare in Ghana. Multicopy amplification of resistant alleles has not been observed previously and is likely to underpin the recent increase in 119S frequency. The large CNV compromised localization of the strong selective sweep around Ace-1, emphasizing the need to integrate CNV analysis into genome scans for selection.',
    doi: 'https://doi.org/10.1111/mec.13197'
  },
  {
    title: 'Evolution of insecticide resistance diagnostics in malaria vectors',
    authors: 'Weetman, D., Donnelly, M.J. (2015)',
    doi: 'https://doi.org/10.1093/trstmh/trv017'
  },
  {
    title: 'Parallel evolution or purifying selection, not introgression, explain similarity in the pyrethroid detoxification linked GSTE4 of Anopheles gambiae and An. arabiensis',
    authors: 'Wilding, C.S., et al. (2015)',
    doi: 'https://doi.org/10.1007/s00438-014-0910-9'
  },
  {
    title: 'Pyrethroid susceptibility of malaria vectors in four districts of western Kenya',
    authors: 'Ochomo, E., et al. (2014)',
    doi: 'https://doi.org/10.1186/1756-3305-7-310'
  },
  {
    title: 'Adaptive introgression between Anopheles sibling species eliminates a major genomic island but not reproductive isolation',
    authors: 'Clarkson, C.S., et al. (2014)',
    doi: 'https://doi.org/10.1038/ncomms5248'
  },
  {
    title: 'Metabolic and Target-Site Mechanisms Combine to Confer Strong DDT Resistance in Anopheles gambiae',
    authors: 'Mitchell, S.N, et al. (2014)',
    doi: 'https://doi.org/10.1371/journal.pone.0092662'
  },
  {
    title: 'CYP6 P450 Enzymes and ACE-1 Duplication Produce Extreme and Multiple Insecticide Resistance in the Malaria Mosquito Anopheles gambiae',
    authors: 'Edi, C.V., et al. (2014)',
    doi: 'https://doi.org/10.1371/journal.pgen.1004236'
  },
  {
    title: 'A cis-regulatory sequence driving metabolic insecticide resistance in mosquitoes: functional characterisation and signatures of selection',
    authors: 'Wilding, C.S., et al. (2012)',
    doi: 'https://doi.org/10.1016/j.ibmb.2012.06.003'
  },
  {
    title: 'Footprints of positive selection associated with a mutation (N1575Y) in the voltage-gated sodium channel of Anopheles gambiae',
    authors: 'Jones, C.M., et al. (2012)',
    doi: 'https://doi.org/10.1073/pnas.1201475109'
  },
  {
    title: 'Identification and validation of a gene causing cross-resistance between insecticide classes in Anopheles gambiae from Ghana',
    authors: 'Mitchell, S.N, et al. (2012)',
    doi: 'https://doi.org/10.1073/pnas.1203452109'
  },
  {
    title: 'Association Mapping of Insecticide Resistance in Wild Anopheles gambiae Populations: Major Variants Identified in a Low-Linkage Disequilbrium Genome',
    authors: 'Weetman, D., et al. (2010)',
    doi: 'https://doi.org/10.1371/journal.pone.0013140'
  }
]

import { openURL } from 'quasar'

export default {
  name: 'Publications',
  data () {
    return {
      publications
    }
  },
  methods: {
    openURL
  }
}
</script>

<style lang="scss" scoped>

</style>
