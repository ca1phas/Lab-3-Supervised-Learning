Source: https://github.com/MoH-Malaysia/covid19-public/tree/main/epidemic

# Open data on COVID-19 in Malaysia

**The scope and granularity of data in this repo will evolve over time.**

- Documentation and data descriptions contained within subfolders.
- Submit pull requests to [share your work for the community](/CONTRIB.md#share-your-work) or [request more data](/CONTRIB.md#data-requests).

**All data is correct as of 2359 of date, unless stated otherwise.**

---

### Cases and Testing

1. [`cases_malaysia.csv`](/epidemic/cases_malaysia.csv): Daily recorded COVID-19 cases at country level.
2. [`cases_state.csv`](/epidemic/cases_state.csv): Daily recorded COVID-19 cases at state level.
3. [`clusters.csv`](/epidemic/clusters.csv): Exhaustive list of announced clusters with relevant epidemiological datapoints.
4. [`tests_malaysia.csv`](/epidemic/tests_malaysia.csv): Daily tests (note: not necessarily unique individuals) by type at country level.
5. [`tests_state.csv`](/epidemic/tests_malaysia.csv): Daily tests (note: not necessarily unique individuals) by type at state level.

### Healthcare

1. [`pkrc.csv`](/epidemic/pkrc.csv): Flow of patients to/out of Covid-19 Quarantine and Treatment Centres (PKRC), with capacity and utilisation.
2. [`hospital.csv`](/epidemic/hospital.csv): Flow of patients to/out of hospitals, with capacity and utilisation.
3. [`icu.csv`](/epidemic/icu.csv): Capacity and utilisation of intensive care unit (ICU) beds.

### Deaths

1. [`deaths_malaysia.csv`](/epidemic/deaths_malaysia.csv): Daily deaths due to COVID-19 at country level.
2. [`deaths_state.csv`](/epidemic/deaths_state.csv): Daily deaths due to COVID-19 at state level.

### Vaccinations

1. [`vax_malaysia.csv`](/vaccination/vax_malaysia.csv): Vaccinations (daily and cumulative, by dose type and brand) at country level.
2. [`vax_state.csv`](/vaccination/vax_state.csv): Vaccinations (daily and cumulative, by dose type and brand) at state level.
3. [`vax_district.csv`](/vaccination/vax_district.csv): Vaccinations (daily and cumulative, by dose type and brand) at district level.
4. [`vax_school.csv`](/vaccination/vax_school.csv): Vaccination coverage for public schools.
5. [`vax_demog_age.csv`'](/vaccination/vax_demog_age.csv): Vaccinations by age group, at district level.
6. [`vax_demog_age_children.csv`'](/vaccination/vax_demog_age_children.csv): Vaccinations by age group with single-year granularity for individuals < 18yo, at district level.
7. [`vax_demog_sex.csv`'](/vaccination/vax_demog_sex.csv): Vaccinations by sex, at district level.
8. [`vax_demog_ethnicity.csv`'](/vaccination/vax_demog_ethnicity.csv): Vaccinations by ethnicity, at district level.
9. [`vax_demog_nationality.csv`'](/vaccination/vax_demog_nationality.csv): Vaccinations by nationality, at district level.
10. [`vax_demog_highrisk.csv`'](/vaccination/vax_demog_highrisk.csv): Vaccinations for special categories (healthcare workers, OKU, individuals with comorbidities) at district level.

### Mobility and Contact Tracing

1. [`checkin_malaysia.csv`](/mysejahtera/checkin_malaysia.csv): Daily checkins on MySejahtera at country level.
2. [`checkin_state.csv`](/mysejahtera/checkin_state.csv): Daily checkins on MySejahtera at state level.
3. [`checkin_malaysia_time.csv`](/mysejahtera/checkin_malaysia_time.csv): Time distribution of daily checkins on MySejahtera at country level.
4. [`trace_malaysia.csv`](/mysejahtera/trace_malaysia.csv): Daily casual contacts traced and hotspots identified by HIDE, at country level.

### Static data

1. [`population.csv`](/static/population.csv) (last updated from DOSM 2020 census, as published in 2022):

- `idxs`: integer coding for states (employed in cases linelist, cluster file, and school vax file)
- `pop`: total population (all other columns are subset of `pop`)
- `pop_18`: population aged 18+
- `pop_60`: population aged 60+, also a subset of `pop_18`
- `pop_12`: population aged 12-17
- `pop_5`: population aged 5-11

_Static data will remain unchanged unless there is an update from the source, e.g. if DOSM makes an update to population estimates. We provide this data here not to supersede the source, but rather to be transparent about the data we use to compute key statistics e.g. the % of the population that is vaccinated. We also hope this ensures synchronisation (across various independent analysts) of key statistics._

# Documentation for epidemic datasets

## File naming convention

| Filename            | Naming convention |    Update frequency     |
| :------------------ | :---------------: | :---------------------: |
| cases_malaysia.csv  |    Static name    | Daily by 2359 (for T-0) |
| cases_state.csv     |    Static name    | Daily by 2359 (for T-0) |
| deaths_malaysia.csv |    Static name    | Daily by 2359 (for T-0) |
| deaths_state.csv    |    Static name    | Daily by 2359 (for T-0) |
| clusters.csv        |    Static name    | Daily by 2359 (for T-1) |
| pkrc.csv            |    Static name    | Daily by 2359 (for T-0) |
| hospital.csv        |    Static name    | Daily by 2359 (for T-0) |
| icu.csv             |    Static name    | Daily by 2359 (for T-0) |
| tests_malaysia.csv  |    Static name    |  At least twice weekly  |
| tests_state.csv     |    Static name    |  At least twice weekly  |

## Metadata (Variables & Methodology)

### Cases and Testing

1. `date`: yyyy-mm-dd format; data correct as of 1200hrs on that date
2. `state`: name of state (present in state file, but not country file)
3. `cases_new`: cases reported in the 24h since the last report
4. `cases_import`: imported cases reported in the 24h since the last report
5. `cases_active`: Covid+ individuals who have not recovered or died
6. `cases_recovered` recovered cases reported in the 24h since the last report
7. `cases_cluster`: number of cases attributable to clusters; the difference between `cases_new` and the sum of cases attributable to clusters is the number of sporadic cases
8. `cluster_x`: cases attributable to clusters under category `x`; possible values for `x` are import, religious, community, highRisk, education, detentionCentre, and workplace
9. `cases_agecat`: cases falling into one of 4 age categories, i.e. child (0-11), adolescent (12-17), adult (18-59), elderly (60+); note that the sum of cases by age may not equal the total cases for that day, as some cases are registered without ages or with unverifiable age data
10. `cases_pvax`: number of partially-vaccinated individuals who tested positive for Covid (perfect subset of `cases_new`), where "partially vaccinated" is defined as receiving at least 1 dose of a 2-dose vaccine at least 1 day prior to testing positive, or receiving the Cansino vaccine between 1-27 days before testing positive
11. `cases_fvax`: number of fully-vaccinated who tested positive for Covid (perfect subset of `cases_new`), where "fully vaccinated" is defined as receiving the 2nd dose of a 2-dose vaccine at least 14 days prior to testing positive, or receiving the Cansino vaccine at least 28 days before testing positive
12. `rtk-ag`: number of tests done using Antigen Rapid Test Kits (RTK-Ag)
13. `pcr`: number of tests done using Real-time Reverse Transcription Polymerase Chain Reaction (RT-PCR) technology

### Deaths

1. `date`: yyyy-mm-dd format; data correct as of 1200hrs on that date
2. `state`: name of state (present in state file, but not country file)
3. `deaths_new`: deaths due to COVID-19 based on **date reported to public**
4. `deaths_bid`: deaths due to COVID-19 which were brought-in dead based on **date reported to public** (perfect subset of `deaths_new`)
5. `deaths_new_dod`: deaths due to COVID-19 based on **date of death**
6. `deaths_bid_dod`: deaths due to COVID-19 which were brought-in dead based on **date of death** (perfect subset of `deaths_new_dod`)
7. `deaths_pvax`: number of partially-vaccinated individuals who died due to COVID-19 based on **date of death** (perfect subset of `deaths_new_dod`), where "partially vaccinated" is defined as receiving at least 1 dose of a 2-dose vaccine at least 1 day prior to testing positive, or receiving the Cansino vaccine between 1-27 days before testing positive.
8. `deaths_fvax`: number of fully-vaccinated who died due to COVID-19 based on **date of death** (perfect subset of `deaths_new_dod`), where "fully vaccinated" is defined as receiving the 2nd dose of a 2-dose vaccine at least 14 days prior to testing positive, or receiving the Cansino vaccine at least 28 days before testing positive.
9. `deaths_tat`: median days between date of death and date of report for all deaths reported on the day

### Cluster analysis

1. `cluster`: unique textual identifier of cluster; nomenclature does not necessarily signify address
2. `state` and `district`: geographical epicentre of cluster, if localised; inter-district and inter-state clusters are possible and present in the dataset
3. `date_announced`: date of declaration as cluster
4. `date_last_onset`: most recent date of onset of symptoms for individuals within the cluster. note that this is distinct from the date on which said individual was tested, and the date on which their test result was received; consequently, today's date may not necessarily be present in this column.
5. `category`: classification as per variable `cluster_x` above
6. `status`: active or ended
7. `cases_new`: number of new cases detected within cluster in the 24h since the last report
8. `cases_total`: total number of cases traced to cluster
9. `cases_active`: active cases within cluster
10. `tests`: number of tests carried out on individuals within the cluster; denominator for computing a cluster's current positivity rate
11. `icu`: number of individuals within the cluster currently under intensive care
12. `deaths`: number of individuals within the cluster who passed away due to COVID-19
13. `recovered`: number of individuals within the cluster who tested positive for and subsequently recovered from COVID-19

### Healthcare

_The datasets below have been constructed to provide 3 kinds of insight. First, the inflow and outflow of patients from quarantine centres, hospitals, and intensive care is, without any further scaling or context, critical to monitor - especially when clear divergences between infections and healthcare outcomes start to be observed (e.g. due to vaccination). Second, comparing against available capacity (number of beds, intensive care units, ventilators) allows for understanding of the strain exerted by the epidemic on the healthcare system. Third, the inclusion of datapoints on non-Covid patients demonstrates the interactions between the epidemic and broader health outcomes._

### PKRC (COVID-19 Quarantine and Treatment Centre)

1. `date`: yyyy-mm-dd format; data correct as of 2359hrs on that date
2. `state`: name of state; note that (unlike with other datasets), it is not necessary that there be an observation for every state on every date. for instance, there are no PKRCs in W.P. Kuala Lumpur and W.P Putrajaya.
3. `beds`: total PKRC beds (with related medical infrastructure)
4. `admitted_x`: number of individuals in category `x` admitted to PKRCs, where `x` can be suspected/probable, COVID-19 positive, or non-COVID
5. `discharged_x`: number of individuals in category `x` discharged from PKRCs
6. `pkrc_x`: total number of individuals in category `x` in PKRCs; this is a stock variable altered by flows from admissions and discharges

### Hospital

1. `date`: yyyy-mm-dd format; data correct as of 2359hrs on that date
2. `state`: name of state, with similar qualification on exhaustiveness of date-state combos as PKRC data
3. `beds`: total hospital beds (with related medical infrastructure)
4. `beds_covid`: total beds dedicated for COVID-19
5. `beds_noncrit`: total hospital beds for non-critical care
6. `admitted_x`: number of individuals in category `x` admitted to hospitals, where `x` can be suspected/probable, COVID-19 positive, or non-COVID
7. `discharged_x`: number of individuals in category `x` discharged from hospitals
8. `hosp_x`: total number of individuals in category `x` in hospitals; this is a stock variable altered by flows from admissions and discharges

### ICU

1. `date`: yyyy-mm-dd format; data correct as of 2359hrs on that date
2. `state`: name of state, with similar qualification on exhaustiveness of date-state combos as PKRC data
3. `beds_icu`: total gazetted ICU beds
4. `beds_icu_rep`: total beds aside from (3) which are temporarily or permanently designated to be under the care of Anaesthesiology & Critical Care departments
5. `beds_icu_total`: total critical care beds available (with related medical infrastructure)
6. `beds_icu_covid`: total critical care beds dedicated for COVID-19
7. `vent`: total available ventilators
8. `vent_port`: total available portable ventilators
9. `icu_x`: total number of individuals in category `x` under intensive care, where `x` can be suspected/probable, COVID-19 positive, or non-COVID; this is a stock variable
10. `vent_x`: total number of individuals in category `x` on mechanical ventilation, where `x` can be suspected/probable, COVID-19 positive, or non-COVID; this is a stock variable

# Documentation for MySejahtera datasets

_Note: As per the MySejahtera privacy policy, individual-level check-in data is purged after 90 days. These summary statistics are stored only as aggregated totals; MySejahtera does not store the underlying data. Consequently, data revisions are not possible for dates more than 90 days ago, even if an inconsistency is spotted._

## File naming convention

1. `checkin_malaysia.csv`: Static name; file is updated by 1500hrs daily
2. `checkin_malaysia_time.csv`: Static name; file is updated by 1500hrs daily
3. `trace_malaysia.csv`: Static name; file is updated by 1500hrs daily

## Variables and Methodology

1. `date`: yyyy-mm-dd format; data correct as of 2359hrs on that date
2. `checkins`: number of checkins at all locations registered on MySejahtera
3. `unique_ind`: number of unique accounts which checked in
4. `unique_loc`: number of unique premises checked into
5. `i`: in the time density file, checkins are aggregated by half-hour buckets, giving 48 in total; bucket `i` corresponds to the ith half-hour slot of the day. for instance, `i = 0` corresponds to 0000 - 0029; `i = 31` corresponds to 1500 - 1529.
6. `casual_contacts`: number of casual contacts identified and notified by CPRC's automated contact tracing system
7. `hide_large`: number of large hotspots identified by CPRC's hotspot identification system
8. `hide_small`: number of small hotspots identified by CPRC's hotspot identification system

# Documentation for Vaccination datasets

At the time of this repo's creation, vaccination datasets were handled by the COVID-19 Immunisation Task Force (CITF), and made available via the [CITF GitHub](https://github.com/CITF-Malaysia/citf-public), which was already in existence. These datasets were ported to the MoH GiHhub from 1st November 2021 onwards, but continually maintained on the CITF GitHub for completeness. Supplementary datasets (published in September or later) were originally published on the MoH GitHub, and are documented below.

## Variables and Methodology

### Vaccination

1. `date`: yyyy-mm-dd format; data correct as of 2359hrs on that date
2. `daily_partial`: number of individuals who received the first dose of a two-dose protocol
3. `daily_partial_adol`: subset (already included) of `daily_partial`, but for individuals aged 12-17 only
4. `daily_partial_child`: subset (already included) of `daily_partial`, but for individuals aged 5-11 only
5. `daily_full`: number of individuals who completed their original protocol (whether the 2nd dose of a two-dose protocol, or a single-dose protocol)
6. `daily_full_adol`: subset (already included) of `daily_full`, but for individuals aged 12-17 only
7. `daily_full_child`: subset (already included) of `daily_full`, but for individuals aged 5-11 only
8. `daily_booster`: number of individuals who received one dose beyond the original protocol
9. `daily`: total doses administered
10. `cumul_x`: cumulative doses falling into category `x`, where `x` is one of the daily categories
11. `brandX`: denotes the number of 1st, 2nd, or 3rd doses administered for that brand; note that `cansino2` is omitted as it is a single-dose protocol
12. `pendingX`: number of records with an indeterminate brand, usually due to errors synchronising with the Vaccine Management System (VMS) blockchain

### AEFIs

An adverse event following immunisation (AEFI) is any untoward medical occurrence which follows immunisation. AEFIs are not necessarily caused by the vaccine - they can be related to the vaccine itself, to the vaccination process (stress related reactions) or can occur independently from vaccination (coincidental). The datasets include cases reported through both the NPRA Reporting System and MySejahtera.

_Disclaimers:_

- _The data are unverified (i.e. self-declared) reports of adverse events, both minor and serious, that occur after immunisation._
- _The number of reports alone cannot used to reach conclusions about the existence, severity, frequency, or rates of AEFIs associated with vaccines._
- _Reported events are not always proven to have a causal relationship with the vaccine. Establishing causality requires additional investigation. Serious AEFI reports are always followed-up and investigated thoroughly for better understanding of the circumstances. However, our public data does not generally change based on information obtained from the investigation process (i.e. we do not reduce AEFI counts after the fact)._
- _The NPRA and MOH always consider the complexities mentioned above, in addition to various other factors, when analysing and monitoring vaccine safety._
