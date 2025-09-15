# Parkinson’s Disease (PD) Tremor Datasets

We compiled multiple Parkinson’s disease (PD) tremor datasets, each collected using IMU sensors. Tremor severity in these datasets is labeled on a scale from 0 to 3, where 0 indicates no tremor, and 1–3 represent increasing levels of tremor severity. Further details can be found in the paper [Time Series Adaptation Network for Sensor-based Human Activity Recognition](#ref4).

## 1. TIM-Tremor Dataset (Technology in Motion Tremor, TI) [1]

This dataset collected postural and resting tremor data from 55 patients using accelerometer sensors attached to the back of the hand, along with video recordings. Since tremor does not occur continuously in PD patients, under physician guidance, patients performed actions such as counting, tapping, and piano playing with one hand to “trigger” tremor, while the other hand remained still for data collection. We used only the accelerometer data in our experiments. The sampling frequency is 1000 Hz, and labels are linearly mapped (`label_new = label/2`).

## 2. PdAssist Dataset (Objective and Quantified Symptom Assessment of Parkinson’s Disease via Smartphone, PA) [2]

This dataset was collected using a smartphone assistant app. Patients performed guided tasks including arm hanging tests, single-leg balance tests, gait tests, postural tremor tests, and resting tremor tests. We used accelerometer data from the resting tremor tests of both hands. The dataset contains data from hundreds of patients, sampled at 50 Hz.

## 3. IMU-Wild Dataset (IMU Data Captured Unobtrusively in-the-wild by Parkinson’s Disease Patients and Healthy Controls, IW) [3]

Data were collected outdoors from 45 subjects (31 PD patients and 14 healthy controls) during tremor episodes using accelerometer and gyroscope sensors. We used tremor data recorded during “phone-calling” tasks. The sampling frequency is 50 Hz.

## 4. PD-BioStamp Dataset (Parkinson Disease Accelerometry Dataset from Five Wearable Sensor Study, BI) [4]

This dataset used five sensors placed on the chest and limbs to collect tremor data from 34 PD patients during medication “on/off” periods (“on”: medication effective, tremor reduced; “off”: medication ineffective or expired, tremor increased). We used accelerometer data from two upper-limb sensors. Sampling frequency is 50 Hz.

## Data Organization

For all datasets, only the recorded accelerometer data are used. Each user’s data consist of multiple **Raw Segments**, and each Raw Segment contains multiple samples. Data are organized as `<X.npy, Y.npy>` pairs per Raw Segment:

- `X.npy`: stores sensor measurements, with shape `[num_samples, 128, 3]`  
- `Y.npy`: stores corresponding labels, with shape `[num_samples]`  

For example, `X.npy` with shape `[5,128,3]` and `Y.npy` with shape `[5]` indicates that this Raw Segment contains 5 samples after segmentation.

## Data Preprocessing

Before experiments, the sampling frequency of all datasets was unified to 50 Hz using linear interpolation. A sliding window of length 128 (2.56 seconds) was applied to divide variable-length Raw Segments into samples, without overlap between samples.

Processed data statistics:

| Dataset     | Number of Users | Number of Raw Segments | Number of Samples | Samples per Label (0-3) |
| ----------- | --------------- | ---------------------- | ----------------- | ----------------------- |
| TIM-Tremor  | 55              | 340                    | 3092              | 1180, 761, 696, 455     |
| PdAssist    | 121             | 1171                   | 6504              | 5939, 270, 257, 38      |
| IMU-Wild    | 55              | 1944                   | 12517             | 8916, 2215, 1145, 241   |
| PD-BioStamp | 68              | 399                    | 1947              | 1791, 47, 87, 22        |

---

## Recommended Citations

If you use these datasets, please cite the following works:

- Wen S, Chen Y, Ma Y, et al. *Time series adaptation network for sensor-based cross domain human activity recognition* [C]//2023 International Joint Conference on Neural Networks (IJCNN). IEEE, 2023: 1-8.  
- Wen S, Chen Y, Guo S, et al. *Discriminative domain adaptation network for fine-grained disease severity classification* [C]//2023 International Joint Conference on Neural Networks (IJCNN). IEEE, 2023: 1-8.

---

## References

1. Paulina B, Jian Z, Silvia O, Pintea A, et al. *Technology in motion tremor dataset: TIM-Tremor* [EB/OL].  
2. Chen Y, Yang X, Chen B, et al. *PdAssist: Objective and quantified symptom assessment of Parkinson’s disease via smartphone* [C]//2017 IEEE International Conference on Bioinformatics and Biomedicine (BIBM). IEEE, 2017: 939-945.  
3. Papadopoulos A, Kyritsis K, Klingelhoefer L, et al. *Detecting parkinsonian tremor from IMU data collected in-the-wild using deep multiple-instance learning* [J]. IEEE Journal of Biomedical and Health Informatics, 2019, 24(9): 2559-2569.  
4. Adams J, Dinesh K, Snyder C, et al. *PD-BioStampRC21: Parkinson’s disease accelerometry dataset from five wearable sensor study* [J]. IEEE Dataport.