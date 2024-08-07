# Mixed Effects Analysis <span id="Chap:data:mixed_effects" label="Chap:data:mixed_effects"></span>

## Introduction

This chapter describes Mixed Effects (MFX) analysis of fMRI data. The
algorithm on which this is based is described fully in (Friston et al.
2005).

Before doing an MFX analysis you will need to have previously
implemented a within-subject analysis for each subject. See, for
example, chapter <a href="#Chap:data:faces" data-reference-type="ref"
data-reference="Chap:data:faces">[Chap:data:faces]</a> for how to do
this. If you have 12 subjects you should have 12 separate within-subject
SPM analyses.

The results of these within-subject analyses can then be used in a
summary statistic approach to random effects inference. This entails
using contrasts from the group of subjects as data in a 'second-level'
design as described in the previous chapter.

Alternatively you can implemented a Mixed Effects (MFX) analysis. There
are five steps to a MFX analysis.

1.  **Specify FFX** This step will create a Fixed Effects model with
    data from all subjects, and a single design matrix comprising
    partitions for each subject. In the SPM batch editor (press the
    Batch button in the SPM top left (command) window) go to *SPM,
    Stats, Mixed Effects Analysis, FFX Specification*. Select the
    directory where you want the FFX model to be saved - we will refer
    to this as DIR. Then select the SPM.mat files that contain the
    analyses for each individual subject. If you have 12 subjects you
    should select 12 SPM.mat files.

    It is essential that the design matrices contained in the SPM.mat
    files have the same number of columns. More specifically it is
    required that, over subjects, there be the same number of sessions,
    conditions per session, and columns per condition (eg
    parametric/time modulators if any). This information is written out
    to the command window so, in the event of an error, you can see
    which subjects are the odd ones out.

2.  **Estimate FFX** This is a very simple step. Press the Estimate
    button in the top-left (command) SPM window, select the DIR/SPM.mat
    file created in the previous step, and then press the green play
    button. SPM will now estimate the group FFX model.

3.  **Specify MFX** In the SPM batch editor go to *SPM, Stats, Mixed
    Effects Analysis, MFX Specification*. Select the DIR/SPM.mat file
    that was estimated in the previous step, and then press the green
    play button.

    SPM will now specify a second level model that is equivalent to a
    two-level hierarchical model. This equivalence is derived in
    equation four of (Friston et al. 2005). The second level model
    comprises (a) a second level design matrix, (b) data, which are the
    regression coefficient images from the estimated FFX model and (c)
    an error covariance matrix, whose variance components are computed
    using the Restricted Maximum Likelihood (ReML) algorithm.

    It is the structure of this covariance matrix that makes an MFX
    analysis different from the alternative summary statistic
    implementation of RFX. The difference is that the MFX error
    covariance structure also contains a contribution from
    within-subject errors from the first level that have been projected
    through (the pseudo-inverse of) the first level design matrix.

    SPM will create a subdirectory DIR/mfx and place an SPM.mat file
    there. This is the MFX model.

4.  **Estimate MFX** This is a very simple step. Press the Estimate
    button in the top-left SPM window, select the DIR/mfx/SPM.mat file
    created in the previous step, and then press the green play button.
    SPM will now estimate the MFX model.

5.  **Results** The estimated MFX model can be interrogated in the usual
    way. Press the Results button in the SPM command window. This will
    bring up the SPM contrasts manager, where you can specify effects to
    test as described in previous chapters.

<div id="refs" class="references csl-bib-body hanging-indent">

<div id="ref-karl_mixed" class="csl-entry">

Friston, K. J., K. E. Stephan, T. E. Lund, A. Morcom, and S. J. Kiebel.
2005. "Mixed-Effects and fMRI Studies." *NeuroImage* 24: 244--52.

</div>

</div>
