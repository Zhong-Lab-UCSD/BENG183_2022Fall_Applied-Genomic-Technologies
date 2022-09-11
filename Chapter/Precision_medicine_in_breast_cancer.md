# Precision medicine in breast cancer


## 1. A breast cancer story
Definition of Precision Medicine (by Dr. Su-In Lee): Tailoring of medical treatment to the individual characteristics of each patient, especially by using genetic or molecular profiling.

In other words, precision medicine should account for personal variations in genomic sequence and environmental exposure.

> Here is a story of how scientists used precision medicine to treat breast cancer.

In the old paradigm, cancer types are usually distinguished by the origin of tumors. For example, lung cancer, liver cancer, breast cancer.

However, tumors with the same origin may be different in appearance and behavior, aggressiveness, and vulnerability. Thus we need to treat each kind of tumor differently.

The early treatment of breast cancer in the 1970s:
- All patients underwent removal of ovaries: The assumption was, no estrogen, no growth of tumor.
- It only helped around 70% of patients with ER+ tumor.
- But how tumor cells are built matters: For example, markers on tumor cell surface and growth circuits can lead to different tumor progression.

Then a discovery in 1970 found that:
- 70% of breast cancer are ER (estrogen-receptor) positive.
- These patients can be treated with anti-estrogen agent to block cancer growth.
> A much better treatment, but what about the remaining 30% of the patients?
 
1984 discovery:
- 20% of breast cancers have abnormal HER-2 gene expression.
- A new drug, Herceptin, was developed to inhibit the function of this protein.

Mid-1990s findings:
- 5% of breast cancers have inherited defect in gene BRCA1 or BRCA2.
- No preventive treatment, but can screen for such inborn defect and watch for tumor formation closely.

Fortunately, the treatments using anti-estrogen agent or Herceptin can be effective for around 85% of the breast cancer patients. This improvement in cancer therapy is largely contributed to the effort to split the patients into different subgroups, then treat each subgroup on its own based on its distinct characteristics. That is the core of precision medicine. We will see how scientists implement this "splitting" in the next section as well.

Note that the 5% of breast cancer with inherited defect in gene BRCA1 or BRCA2, are categoried as Triple Negative Breast Cancer (TNBC). This type of breast cancer does not express the genes for estrogen receptor (ER), progesterone receptor (PR) and HER2. And it is still in need of an effective treatment.

In order to develop personalized treatment and advance the field of precision medicine, current genomics and machine learning researchers need to address:
- identifying genetic or molecular markers for clinical phenotypes
- discovering disease subtypes from genetic and/or molecular data
- building prediction models for clinical events based on electronic medical record (EMR) data

## 2\. The history of breast cancer treatment （by Kelsey Dang, Katy Zou, Diego Quintero）


![timeline](https://github.com/kelseydang/BENG183_Project/blob/master/BENG183_Project/timeline%20precision%20medicine.png)

**1882:** William Halsted performed the first radical mastectomy, a
procedure that surgically removes the breast, underlying chest muscle
(including pectoralis major and pectoralis minor), and lymph nodes of
the axilla.3 This surgery remained the standard breast cancer treatment
well into the 20th century.<sup>2</sup>

**1895:** The first X-ray was taken. Emil Herman Grubbe used X-rays to
treat a breast cancer patient.<sup>4</sup>

**1898:** Marie and Pierre Curie discovered the radioactive elements
radium and polonium. Radium was used for radiation therapy on patients
but its penetrating abilities were not well understood.<sup>2</sup>

**1932:** A new, less invasive mastectomy approach was
developed.<sup>2</sup>

**1937:** Radiation therapy is used in conjunction with surgery in order
to preserve the breast. The tumor is removed and needles laced with
radium are inserted near the breast and lymph nodes.<sup>2</sup>

**1978:** The anti-estrogen drug tamoxifen is approved by the Food and
Drug Administration (FDA) for use in breast cancer treatment. Tamoxifen
is part of a new class of drugs called selective estrogen receptor
modulators (SERMs) used against cancer. Each cell types’ unique receptor
composition allows for selective growth inhibition.5 This is a huge
breakthrough in understanding gene and protein interaction pathways.

**1984:** Researchers discovered the human equivalent gene HER2 in rats.
HER2 was aggressive when overexpressed and nonresponsive to treatments,
posing a serious dilemma for researchers.<sup>2</sup>

**1986:** Scientists clone the HER2 gene.

**1995:** Using cloning technology, scientists can now clone the tumor
suppressor genes BRCA1 and BRCA2. Inherited mutations in these two genes
predict an increased risk of breast cancer.

**1996:** The FDA approves anastrozole as an anti-estrogen treatment for
breast cancer.

**1998:** Tamoxifen, another SERM, is found to decrease the risk of
developing breast cancer in at-risk men and women by 50%. It is now the
most commonly prescribed preventative therapy for
“hormone-receptor-positive, early-stage breast cancer after surgery”.6
Trastuzumab, better known as Herceptin, is approved by the FDA. It is
used to target patients with HER2 receptor positive breast
cancer.<sup>7</sup>

**April 2003:** Human Genome Project is completed. This allowed the
possibility of precision medicine to be widely accepted.

**2006:** The drug raloxifene was found to reduce breast cancer risk for
postmenopausal women who have higher risk.

**2015:** All of US initiated was founded under the Obama administration
in efforts to expand the database for precision medicine focused
research.<sup>1</sup>

## 3\.Genomic biomarkers and companion tests

In the first of the charts below, the most widely prescribed breast
cancer drugs are listed along with the specific patient type targeted.
The second chart lists important biomarkers associated with breast
cancer, a description of what the biomarker is, the patient type it
affects, and the modern treatment prescribed.

![drug table](https://github.com/kelseydang/BENG183_Project/blob/master/BENG183_Project/drug%20table.png)

![biomarker table](https://github.com/kelseydang/BENG183_Project/blob/master/BENG183_Project/biomarker%20table.png)

Genomics is a branch of biology that focuses on understanding genomes
and comprises of the central core of precision medicine.<sup>24</sup>
Given the knowledge that every individual’s genetic makeup differs,
biomarkers are used in order to identify commonalities between carriers
of diseases. In this section, we will focus on genomic biomarkers that
identify breast cancer patient types, specifically delving into
HER2-positive patients who have an overexpression of the HER2 gene.  

The discovery of the HER2 gene pathway and its importance in breast
cancer growth led to the development of the drug trastuzumab and various
other targeted treatments, improving the survival rate of breast cancer
patients. The HER2 gene produces proteins that when overexpressed leads
to uncontrolled proliferation of epidermal tissue. The two NCI-funded
research teams led separately by Dennis Slamon, M.D. and Stuart
Aaronson, M.D. were able to discover the “groundbreaking hypothesis that
If HER2 could be blocked, the growth of HER2-positive breast cancer
might be slowed.”<sup>25</sup> This was done by showing that high levels
of HER2 protein correlate with faster breast cancer growth. A solution
they found was to inhibit the actions of the HER2 proteins with special,
laboratory produced monoclonal antibodies. So thus, the drug trastuzumab
or Herceptin was created.

