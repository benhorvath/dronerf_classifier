# Classifying drone RF signals with statistical learning and a small data set

RPubs document: [https://rpubs.com/benhorvath/dronerf_classifier](https://rpubs.com/benhorvath/dronerf_classifier)

This brief note puts together a couple (non-deep learning) algorithms to classify RF signals using a small open-source data set. This work agrees with Medaiyese, et al. (2021) that large labeled data sets and complicated deep learning may not be essential for classifying drone RF signals.

The data is available for download at: [`DroneRF` dataset: A dataset of drones for RF-based detection, classification, and identification](https://data.mendeley.com/datasets/f4c2b4n755/1). Uncompressed, it is 43 gigabytes in size. It is summarized in Allahham, et al. (2019):

> ... the `DroneRF` dataset: a radio frequency (RF) based dataset of drones functioning in different modes, including off, on and connected, hovering, flying, and video recording. The dataset contains recordings of RF activities, composed of 227 recorded segments collected from 3 different drones, as well as recordings of background RF activities with no drones. The data has been collected by RF receivers that intercepts the drone's communications with the flight control module. The receivers are connected to two laptops, via PCIe cables, that runs a program responsible for fetching, processing and storing the sensed RF data in a database. 

Three models are developed and tested on a reserved hold-out set:

* $M_0$: Binary task, binomial GLM with ElasticNet regularization (R library: `glmnet`); hold-out performance:
  - precision: 0.89
  - recall: 1.0
  - F-score: 0.94
  - balanced accuracy: 0.99
* $M_1$: Binary task, Random Forest (R library: `ranger`); hold-out performance:
  - precision: 0.94
  - recall: 1.0
  - F-score: 0.97
  - balanced accuracy: 0.99
* $M_2$: Multiclass task, Random Forest; hold-out performance:
  - mean balanced accuracy: 0.91
  - mean sensitivity: 0.88
  - mean specificity: 0.94

Model performance could easily be improved with slightly more powerful hardware, which would allow spectograms to encode more information, i.e., larger than $122 x 122$ pixels.


## References

* Allahham, MHD Saria, Mohammad F. Al-Sa'd, Abdulla Al-Ali, Amr Mohamed, Tamer Khattab, and Aiman Erbad. 2019. '`DroneRF` dataset: A dataset of drones for RF-based detection, classification and identification.' _Data in Brief_ 26: 104313.

* Friedman, Jerome, Trevor Hastie, and Rob Tibshirani. 2010. 'Regularization paths for generalized linear models via coordinate descent.' _Journal of Statistical Software_ 33, no. 1: 1.

* Medaiyese, Olusiji O., Abbas Syed, and Adrian P. Lauf. 2021. 'Machine learning framework for RF-based drone detection and identification system.' _2021 2nd International Conference on Smart Cities, Automation \& Intelligent Computing Systems_. IEEE.

* Zou, Hui, and Trevor Hastie. 2005. 'Regularization and variable selection via the elastic net.' _Journal of the Royal Statistical Society: Series B (Statistical Methodology)_ 67, no. 2: 301--20.
