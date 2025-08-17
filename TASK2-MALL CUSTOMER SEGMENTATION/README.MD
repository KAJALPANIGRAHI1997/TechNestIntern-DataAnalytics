
# Mall Customer Segmentation

This project performs **customer segmentation** using the Mall Customers dataset.  
We apply **K-Means Clustering** to group customers based on their **Annual Income** and **Spending Score**, and visualize the results.

## 📂 Project Contents
- `Mall_Customers.csv` → Dataset used for clustering.
- `MALL CUSTOMER SEGMENT.ipynb` → Jupyter Notebook with complete analysis and code.
- `clustering_bivariate.png` → Visualization of customer segments.
- `Clustering.csv` → Output file with assigned cluster labels.

## 🛠️ Technologies Used
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn

## 📊 Methodology
1. **Load Data** – Import the dataset.
2. **Data Exploration** – Understand the distribution of features.
3. **K-Means Clustering** – Identify optimal number of clusters using Elbow Method.
4. **Visualization** – Scatter plot of clusters based on spending score & income.

## 📷 Output Example
![Customer Segmentation](clustering_bivariate.png)
## 📂 Project Structure
mall-customer-segmentation/
│
├── data/                     # Raw and processed data
│   ├── Mall_Customers.csv
│   └── Clustering.csv
│
├── notebooks/                # Jupyter notebooks
│   └── MALL CUSTOMER SEGMENT.ipynb
│
├── images/                   # Visualizations and plots
│   └── clustering_bivariate.png
│
├── requirements.txt          # Dependencies
├── README.md                 # Project documentation
└── LICENSE                   # Optional - license info

## 🚀 How to Run
1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/mall-customer-segmentation.git
````

2. Navigate into the project folder:

   ```bash
   cd mall-customer-segmentation
   ```
3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```
4. Open the notebook:

   ```bash
   jupyter notebook "MALL CUSTOMER SEGMENT.ipynb"
   ```

## 📜 License

This project is licensed under the MIT License.

