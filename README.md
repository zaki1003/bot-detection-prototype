# Bot Detection Prototype: A Comparative Analysis

This project provides a comprehensive analysis and comparison of four distinct bot detection methodologies using a real-world web server access log dataset. The goal is to identify the most effective and efficient algorithm for detecting automated traffic in a production-like environment.

The analysis evaluates a traditional **Rule-Based System** against three advanced, unsupervised anomaly detection algorithms: **Isolation Forest**, **XStream**, and a feature-based prototype of **Streaming Sequence-Aware Graph Anomaly Detection (SSGAD)**.

## 🚀 Key Features

*   **Log Parsing & EDA:** In-depth parsing of web server logs and exploratory data analysis to identify initial traffic patterns.
*   **Advanced Feature Engineering:** Creation of **behavioral features** for each IP, categorized into "Basic" (8 features) and "Advanced" (25 features) sets to test model sensitivity.
*   **Four-Algorithm Implementation:**
    1.  **Rule-Based Detector:** A heuristic system to establish an interpretable "ground truth."
    2.  **Isolation Forest:** A standard tree-based anomaly detection model.
    3.  **[XStream](https://cmuxstream.github.io/):** A streaming-focused outlier detection algorithm based on the KDD '18 research paper.
    4.  **SSGAD:** A prototype of a graph-based anomaly detection concept.
*   **Comparative Performance Analysis:** Rigorous evaluation of all algorithms using F1-score, Precision, and Recall.
*   **Data Visualization:** Clear and insightful visualizations to support the analytical findings.

## 📊 Dataset Overview

The analysis is performed on a publicly available **Web Server Access Log** dataset, representing a realistic snapshot of traffic to an e-commerce website.

| Metric              | Value                                         |
| :------------------ | :-------------------------------------------- |
| **Source**          | Kaggle: [Web Server Access Logs](https://www.kaggle.com/datasets/eliasdabbas/web-server-access-logs) |
| **Key Characteristic** | Contains a clear mix of human traffic and known web crawlers (Googlebot, Bingbot, etc.). |

Since the dataset is unlabeled, the Rule-Based System's classifications are used as the ground truth for evaluating the performance of the unsupervised models.

## ⚙️ Methodology

The project follows a systematic, four-step approach:

1.  **Log Parsing & EDA:** The raw log file is parsed to extract structured data. Initial analysis reveals a significant presence of bot traffic (~34% from known crawlers) and high traffic concentration from a few IPs.

2.  **Feature Engineering:** Two feature sets (**Basic** and **Advanced**) are engineered to capture IP behavior, including request velocity, error rates, timing patterns, and user agent diversity.

3.  **Ground Truth Establishment:** A **Rule-Based System** is implemented to provide clear, interpretable bot labels. This system flags 14 IPs (4.2%) as malicious-like bots, which serves as the benchmark for the other models.

4.  **Model Implementation & Evaluation:** The three unsupervised models (Isolation Forest, XStream, SSGAD) are trained and evaluated against the rule-based ground truth. Their performance is measured using standard classification metrics.

## 🏆 Results & Analysis

The comparative analysis produced a clear and decisive ranking of the bot detection algorithms.

### Final Algorithm Performance Ranking

The models were ranked by their **F1-score**, which provides the best measure of overall effectiveness by balancing precision and recall. **XStream with basic features was the clear champion**, significantly outperforming all other configurations.

| Rank      | Algorithm          | Features/Mode    | F1-Score | Recall | Precision |
| :-------- | :----------------- | :--------------- | :------- | :----- | :-------- |
| 🥇 **1st** | **XStream**        | **Basic**        | **0.7778** | 1.0000 | 0.6364    |
| 🥈 **2nd** | **SSGAD**          | **Feature (Basic)** | 0.6829   | 1.0000 | 0.5185    |
| 🥉 **3rd** | **Isolation Forest** | **Basic**        | 0.6512   | 1.0000 | 0.4828    |
| 4th       | SSGAD              | Graph            | 0.6222   | 1.0000 | 0.4516    |
| 5th       | SSGAD              | Feature (Advanced) | 0.6000   | 0.8571 | 0.4615    |
| 6th       | Isolation Forest   | Advanced         | 0.5217   | 0.8571 | 0.3750    |
| 7th       | XStream            | Advanced         | 0.0805   | 1.0000 | 0.0419    |

### Key Findings

1.  **XStream's Superiority:** With a curated set of basic features, XStream achieved the best performance with a **perfect 100% recall** and the **highest precision (64%)**, making it both highly effective and efficient.

2.  **The "Less is More" Principle:** The most critical insight was that the **basic feature set consistently outperformed the advanced set** for all top models. This was especially true for XStream, whose performance catastrophically failed with more features, highlighting the importance of feature quality over quantity.

3.  **Perfect Recall is Achievable:** The top three models all achieved **100% recall** with basic features, proving they are highly capable of identifying the full scope of bot activity in this dataset. The main differentiator was their precision.

### Visualizations

The visualizations from the rule-based analysis clearly distinguish bot behavior from human traffic, validating the heuristics used. Bots exhibit significantly higher request rates and error rates.

<img width="4471" height="2970" alt="Image" src="https://github.com/user-attachments/assets/06139060-c684-464e-bb16-ba53b6df1c3d" />

## 🏁 Conclusion & Recommendations

This analysis demonstrates that **XStream**, when paired with a simple, well-chosen feature set, is an exceptionally powerful tool for bot detection, outperforming other common anomaly detection methods.

**Production Recommendations:**

*   **Primary System:** Implement **XStream with a curated set of basic features** for optimal performance and efficiency.
*   **High-Security Scenarios:** For critical assets where catching every threat is paramount, **SSGAD (Graph Mode)** is an excellent choice due to its perfect recall.
*   **Avoid Complexity:** Avoid using large, uncurated feature sets, as they were shown to degrade the performance of every algorithm tested.

This project provides a robust framework for evaluating and deploying a bot detection system, proving that advanced algorithms combined with thoughtful feature engineering can deliver superior results.

## 🛠️ How to Run

### 🚀 View on Kaggle (Recommended)

The easiest way to explore this project is to view the interactive notebook directly on Kaggle. This requires no local setup.

**[➡️ View the Notebook on Kaggle](https://www.kaggle.com/code/your-username/your-notebook-name)**


### 💻 Local Setup

Alternatively, to run the project locally, follow these steps:

**1. Prerequisites:**
*   Python 3.8+
*   Jupyter Notebook or JupyterLab

**2. Installation:**
Clone the repository and install the required libraries. It is recommended to use a virtual environment.
```bash
git clone https://github.com/zaki1003/bot-detection-prototype.git
cd bot-detection-prototype
pip install -r requirements.txt
```
*(You will need to create a `requirements.txt` file with the libraries listed in the notebook, such as pandas, scikit-learn, mmh3, matplotlib, seaborn, etc.)*

**3. Dataset:**
Download the dataset from [Kaggle](https://www.kaggle.com/datasets/eliasdabbas/web-server-access-logs) and place the `access.log` file in the root directory. Rename it to `access_10000.log` or update the file path in the notebook.

**4. Execution:**
Launch Jupyter and run the cells in the `bot-detection-prototype-notebook.ipynb` notebook.
```bash
jupyter notebook bot-detection-prototype-notebook.ipynb
```
