import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# -----------------------------
# CAGR Calculation
# -----------------------------
def calculate_cagr(start_value, end_value, periods):
    return (end_value / start_value) ** (1 / periods) - 1

# Sample data (2011 to 2019) - PFCE (Private Final Consumption Expenditure) in INR/person
df=pd.read_csv("food_analysis.csv")

# -----------------------------
# Calculate CAGR for each category
# -----------------------------
years = len(df['Year']) - 1
cagr_results = {
    category: calculate_cagr(df[category].iloc[0], df[category].iloc[-1], years)
    for category in ['Food', 'Fruits', 'Vegetables', 'MMP', 'MFE']
}

print("CAGR (2011–2019):")
for k, v in cagr_results.items():
    print(f"{k}: {v:.2%}")

# -----------------------------
# Caloric Intake Comparison (Simplified)
# -----------------------------
caloric_data = {
    'Category': ['Cereals', 'Pulses', 'Dairy', 'Fruits/Vegetables', 'MFE', 'Processed'],
    'Actual Intake (kcal)': [1300, 150, 250, 100, 200, 500],
    'LANCET Recommended (kcal)': [800, 100, 250, 204, 300, 50]
}
cal_df = pd.DataFrame(caloric_data)

# Plotting comparison
cal_df.plot(x='Category', kind='bar', stacked=False, figsize=(10, 6))
plt.title("Calorie Intake: Actual vs. LANCET Recommended")
plt.ylabel("Calories (kcal)")
plt.xticks(rotation=45)
plt.tight_layout()
plt.grid(True)
plt.show()

# -----------------------------
# Environmental Impact (GWP) Comparison
# -----------------------------
diets = ['Rural', 'Urban', 'NIN Vegetarian', 'NIN Non-Veg', 'LANCET']
gwp_values = [0.9, 1.0, 1.1, 1.2, 1.3]  # Relative scale

plt.figure(figsize=(8, 5))
plt.bar(diets, gwp_values, color='seagreen')
plt.title("Global Warming Potential (Relative GHG Emissions)")
plt.ylabel("Relative Emissions (CO2 eq.)")
plt.grid(axis='y')
plt.tight_layout()
plt.show()
