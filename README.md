#  Marketing Mix Modeling (MMM) – Methodology & Insights

This project applies time-series modeling with XGBoost to understand the impact of different marketing channels on revenue.

1. Data Preparation

	-	sine/cosine transformations were used to capture weekly & monthly cycles.
	-	tree-based model like XGBoost
	-	added lag features
	-	used 4-week moving averages
	-	applied log1p transformation (log(1+x)) to spend & revenue data.
	-	handles zeros safely and reduces the impact of extreme spikes in marketing spend
	-	used RobustScaler instead of StandardScaler

2. Modeling Approach

	-	Model Choice: XGBoost
	-	Powerful on tabular data.
	-	Handles non-linear interactions 
	-	Hyperparameters
	-	n_estimators = 300
	-	learning_rate = 0.05
	-	Regularization
	-	Data split chronologically (80% train, 20% test).

3. Causal Framing with a Mediator Model

The model explicitly considers Google Spend as a mediator influenced by other channels.
	-	Mediator Hypothesis
	-	Channels like TikTok & Facebook drive brand awareness, which increases Google search activity → boosting Google spend.
	-	Google Spend, in turn, has a direct impact on revenue.
	-	Two-Stage Setup
	-	Stage 1: Predict Google Spend (scaled_log1p_Google_Spend) from other channels.
	-	Stage 2: Predict Revenue using
	-	Predicted Google Spend (pred_google_spend_cv)

4. Diagnostics & Model Performance
	-	R² ≈ 0.93 → explains 93% of revenue variance on unseen data.
	-	RMSE & MAE show low prediction error in dollar terms.
	-	TimeSeriesSplit confirmed consistent relationships across periods.

# Project Structure
1. MMM_Assessment.ipynb: The main Jupyter Notebook containing all the code.
2. dataset.csv: The raw weekly data used for the model.
3. requirements.txt
4. README.md: This file! Your guide to the project.

# SETUP INSTRUCTIONS
python -m venv venv
source venv/bin/activate 
pip install -r requirements.txt
