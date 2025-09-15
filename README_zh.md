# Parkinson震颤识别（PD）数据集

我们整理了多个帕金森病（PD）震颤数据集，每个数据集都使用了 IMU 传感器。震颤程度在这些数据集中被划分为 0-3 的标签，其中 0 表示无震颤，1-3 分别表示震颤程度递增（数字越大震颤越严重）。

## 1. TIM-Tremor 数据集（Technology in Motion Tremor，TI）[1]

该数据集使用粘贴在患者手背上的加速计传感器收集了 55 位患者的姿势性震颤和静止性震颤数据，同时配合视频录像。由于帕金森病患者并非在任何时间段都会发生震颤，因此在医师指导下，患者使用一只手依次做数数、轻敲、弹钢琴等动作“刺激”震颤发生，同时另一只手保持静止，传感器收集加速计数据。本文使用了该数据集中的加速计数据，采样频率为 1000Hz，线性映射（`label_new = label/2`）。

## 2. PdAssist 数据集（Objective and Quantified Symptom Assessment of Parkinson’s Disease via Smartphone，PA）[2]

该数据集通过手机助手收集数百名病患的帕金森震颤数据。患者按照医师指导完成动作，包括直立状态下左右手垂臂测试、单腿站立稳定性测试、步态测试、左右手姿势性震颤测试以及左右手持静止性震颤测试。本文使用左右手持静止性震颤测试的加速计数据，采样频率为 50Hz。

## 3. IMU-Wild 数据集（IMU Data Captured Unobtrusively in-the-wild by Parkinson’s Disease Patients and Healthy Controls，IW）[3]

该数据集在户外条件下收集了 45 位被试者在震颤发生时的加速计和陀螺仪数据，其中包括 31 名患者和 14 名健康人。本文使用被试者在“打电话”动作下的震颤加速计数据，采样频率为 50Hz。

## 4. PD-BioStamp 数据集（Parkinson Disease Accelerometry Dataset from Five Wearable Sensor Study，BI）[4]

该数据集使用放置于胸口和四肢的 5 个传感器收集 34 名帕金森病患者在药物“开/关”期间的震颤数据（“开”表示药物生效，震颤减小；“关”表示药物未生效或过期，震颤加剧）。本文使用上肢两个传感器收集的加速计数据，采样频率为 50Hz。

## 数据组织形式

对于所有数据集，仅使用记录的加速计数据。每个用户的数据由多个 **Raw Segments** 组成，每个 Raw Segment 包含多个样本。数据以 `<X.npy, Y.npy>` 的形式组织，每个 Raw Segment 对应一对文件：

- `X.npy`：存储加速计记录数据，形状为 `[num_samples, 128, 3]`  
- `Y.npy`：存储对应标签，形状为 `[num_samples]`  

例如，一个 Raw Segment 的 `X.npy` 形状为 `[5,128,3]`，`Y.npy` 形状为 `[5]`，表示该 Raw Segment 被切分为 5 个样本。

## 数据预处理

在实验前，通过线性插值将所有数据集的采样频率统一为 50Hz。使用步长为 128（2.56 秒）的滑动窗口将不同长度的 Raw Segment 切分为样本，样本之间无重叠。

处理后的数据统计如下：

| 数据集      | 用户数量 | 原始数据段数量 | 样本数量 | 分类别样本数量 (0-3)  |
| ----------- | -------- | -------------- | -------- | --------------------- |
| TIM-Tremor  | 55       | 340            | 3092     | 1180, 761, 696, 455   |
| PdAssist    | 121      | 1171           | 6504     | 5939, 270, 257, 38    |
| IMU-Wild    | 55       | 1944           | 12517    | 8916, 2215, 1145, 241 |
| PD-BioStamp | 68       | 399            | 1947     | 1791, 47, 87, 22      |

---

## 推荐引用

如果您使用这些数据集，请引用以下工作，作者会很高兴这些数据能为其他研究提供帮助：

- Wen S, Chen Y, Ma Y, et al. *Time series adaptation network for sensor-based cross domain human activity recognition* [C]//2023 International Joint Conference on Neural Networks (IJCNN). IEEE, 2023: 1-8.  
- Wen S, Chen Y, Guo S, et al. *Discriminative domain adaptation network for fine-grained disease severity classification* [C]//2023 International Joint Conference on Neural Networks (IJCNN). IEEE, 2023: 1-8.

---

## 参考文献

1. Paulina B, Jian Z, Silvia O, Pintea A, et al. *Technology in motion tremor dataset: TIM-Tremor* [EB/OL].  
2. Chen Y, Yang X, Chen B, et al. *PdAssist: Objective and quantified symptom assessment of Parkinson’s disease via smartphone* [C]//2017 IEEE International Conference on Bioinformatics and Biomedicine (BIBM). IEEE, 2017: 939-945.  
3. Papadopoulos A, Kyritsis K, Klingelhoefer L, et al. *Detecting parkinsonian tremor from IMU data collected in-the-wild using deep multiple-instance learning* [J]. IEEE Journal of Biomedical and Health Informatics, 2019, 24(9): 2559-2569.  
4. Adams J, Dinesh K, Snyder C, et al. *PD-BioStampRC21: Parkinson’s disease accelerometry dataset from five wearable sensor study* [J]. IEEE Dataport.