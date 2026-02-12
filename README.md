# IntTravel: A Real-World Dataset and Generative Framework for Integrated Multi-Task Travel Recommendation

<div align="center">
Huimin Yan¹, Longfei Xu¹†, Junjie Sun, Zheng Liu, Wei Luo, Kaikui Liu, Xiangxiang Chu

<br>
<br>
AMAP, Alibaba Group

<br>

¹Equal contribution &nbsp;&nbsp;&nbsp; †Corresponding author and project lead.

[![Data Set](https://img.shields.io/badge/Data-Set-green)](https://huggingface.co/datasets/GD-ML/IntTravel_dataset/tree/main)

</div>

## 📖 Overview
We introduce **IntTravel**, the first large-scale public dataset for **integrated travel recommendation**, including **4.1 billion interactions from 163 million users with 7.3 million POIs**. Built upon this dataset, we introduce an end-to-end, **decoder-only generative framework for multi-task recommendation**. It incorporates information preservation, selection, and factorization to balance task collaboration with specialized differentiation, yielding substantial performance gains. IntTravel has been successfully deployed on Amap serving hundreds of millions of users.

## 📊 IntTravel: Dataset

All data are collected from a leading provider of digital map, navigation and real-time traffic information in China. Here is a simple dataset in `data_process/raw_data` and a more comprehensive dataset in [Hugging Face](https://huggingface.co/datasets/GD-ML/IntTravel_dataset/tree/main). The code in `data_process` demonstrates how to construct the input sequence of the model and the labels for all tasks based on the original data.

### Information of POIs

The IntTravel dataset contains **7,291,872** POIs (Point of Interests) distributed across several major cities in China. Each POI is described by the following fields:

| Field | Description |
|:---|:---|
| POI ID | A unique identifier for each Point of Interest. |
| Normalized score | A 0-1 score reflecting the overall popularity of the POI. |
| Geographic ID | Identifier for the POI's geographic block. Same GIDs indicate geographical proximity. |
| Category ID | A numerical identifier for the Point of Interest's category. |
| Administrative Region ID | The identifier for the administrative region of the POI. |
| Coordinates | The spatial coordinates of the POI on a 2D plane. |

### User Profiles
The IntTravel dataset contains **162,815,861** users, each described by the following fields:

| Field | Description |
|:---|:---|
| User ID | A unique identifier assigned to each user. |
| Profile Feature 1 | The first profile feature. |
| ... | ... |
| Profile Feature 6 | The sixth profile feature. |


### User Interactions
The IntTravel dataset includes **4,129,827,011** user interaction events. Each event is characterized by the following fields:

| Field | Description |
|:---|:---|
| User ID | A unique identifier for the user who performed the interaction. |
| Timestamp | The time of the user interaction, recorded in milliseconds. |
| Action Type | A numerical ID representing the type of user behavior (e.g., click). |
| POI ID | The identifier of the Point of Interest involved in the interaction. |
| Geographic ID | The geographic block ID where the user was during the interaction. |
| Administrative Region ID | The administrative region ID where the user was during the interaction. |
| Weather | A numerical ID representing the weather condition during the interaction. |
| Travel Mode | A numerical ID for the user's chosen travel mode. |
| Via POI ID | The identifier for a way-point POI added by the user. |


## 💡 IntTravel: Multi-Task Framework

<img width="5275" height="2122" alt="IntTravel_multi_task_framework" src="https://github.com/user-attachments/assets/5ddf5382-299f-41ed-aeac-2b475883cb7a" />

IntTravel is **the first multi-task solution for generative recommendation**. We propose a bottom-up multi-task method to handle multiple tasks within a single generative model. The approach comprises three modules:

*   **Task-Guided Information Persistence (TIP)** ensures maximum propagation of task-relevant information in the decoder.
*   **Task-Specific Selective Gating (TSG)** enables each task to filter useful information from the decoder's output.
*   **Task-Aware Scenario Factorization (TSF)** empowers each task to factorize its output based on specific scenarios.


## ✨ Scaling Laws
<p align="center">
<img width="432" height="332" alt="scaling" src="https://github.com/user-attachments/assets/b05403bd-b7b7-495a-a3d5-056d45ec4b57" />
</p>

The results of scaling experiments reveal a **strong and consistent scaling trend**. As the model depth increases from 1 to 80 layers, performance on all metrics steadily improves (task accuracy increases outward while loss decreases outward). There is no sign of performance decrease even at very deep configurations like **80 layers**, which is often a challenge for complex models. This demonstrates the excellent scaling capability of proposed architecture.


