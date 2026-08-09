<div align="center">

<h1>CAFM-PW</h1>

<h3>Mechanics-Informed Tabular Foundation Model for Plastic Hinge Length in Reinforced Concrete Structural Walls with Calibrated Uncertainty</h3>

<p><i>Back-calculation of plastic hinge length with campaign level calibration</i></p>

<p>
<a href="https://twakjira.github.io/CAFM-PW/"><img src="https://img.shields.io/badge/%F0%9F%8C%90%20Project%20page-4A90D9?style=for-the-badge" alt="Project page"></a>
<a href="#availability"><img src="https://img.shields.io/badge/Paper-under%20review-94A3B8?style=for-the-badge" alt="Paper"></a>
<a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-2AA876?style=for-the-badge" alt="License"></a>
</p>

</div>

---

## Overview

The plastic hinge length controls the plastic rotation and drift capacity assigned to reinforced concrete structural walls in concentrated plasticity models. However, the plastic hinge length listed in experimental databases is a derived quantity. Each testing program obtains the value from the measured plastic curvature and displacement through an adopted idealization. Moreover, specimens of one experimental campaign share design ranges and data reduction procedures. Consequently, random partitions of individual specimens can overstate the accuracy expected for a new campaign.

CAFM-PW couples an inverted compatibility relation with a pretrained tabular foundation model for the post-test identification of the plastic hinge length. Prediction intervals are calibrated with one conformity score per experimental campaign.

## Method

| Component | Role |
| :-- | :-- |
| **Mechanics-based reference value** | A compatibility relation between plastic displacement, plastic curvature, and hinge length is inverted in closed form to provide a physically grounded reference value for each test |
| **Residual and direct formulations** | A pretrained tabular foundation model predicts the residual with respect to the reference value in one formulation and the logarithm of the hinge length in a second formulation, and the predictive quantiles of the two formulations are averaged with no gradient update |
| **Campaign level calibration** | Conformalized quantile regression uses one conformity score per experimental campaign excluded from model fitting |
| **Prediction updating** | Appending a few tested walls from the target campaign to the context improves accuracy and sharpens intervals without changing any parameter |

## Results

The evaluation covers 234 tests from 58 experimental campaigns. Complete campaigns are withheld from training, calibration, and testing, and every comparison is tested at the campaign level.

| Metric | CAFM-PW | Best benchmark model |
| :-- | --: | --: |
| Median absolute percentage error | **2.19%** | 2.66% |
| Coefficient of determination | **0.990** | 0.981 |
| Logarithmic coefficient of determination | **0.983** | 0.961 |
| Predictions within 20% of the reported value | **95.3%** | 87.7% |
| Empirical coverage at 90% nominal coverage | **0.920** | 0.832 |
| Normalized interval width at 90% nominal coverage | **0.180** | 0.438 |

Appending five tested walls from the target campaign to the context lowers the median error by 71% and the normalized interval width by 47%, with no parameter update.

## Availability

The full implementation, the processed database, the trained configurations, and the reproduction scripts will be released here upon acceptance of the associated article.

## License

Released under the [MIT License](LICENSE).
