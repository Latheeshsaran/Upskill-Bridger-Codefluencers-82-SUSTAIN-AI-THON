# Upskill-Recommendation
<!DOCTYPE html>
<html>
<head>
    <title>Skill Gap Bridging Platform</title>
</head>
<body>
    <h1 align="center">Skill Gap Bridging Platform</h1>
    <p align="center">
        <em>An AI-powered solution to match skills with industry needs.</em>
    </p>
    <hr>

    <h2>🔍 Brief Introduction</h2>
    <p>
        This project is designed to bridge the skill gap in the workforce by leveraging machine learning to predict the core skills and company-specific skills required for various job roles. It aims to align personal development with business requirements, creating a workforce equipped for future challenges.
    </p>

    <h2>📊 Workflow Diagram</h2>
    <p align="center">
        <img src="workflow_diagram.png" alt="Workflow Diagram" width="600">
    </p>
    <p>
        The workflow begins with dataset preprocessing, followed by model training and evaluation. Finally, it allows real-time skill predictions based on user inputs.
    </p>

    <h2>🧠 Concept Map</h2>
    <p align="center">
        <img src="concept_map.png" alt="Concept Map" width="600">
    </p>
    <p>
        The concept revolves around aligning individual learning paths with industry demands while promoting career growth and workforce retention.
    </p>

    <h2>⚙️ Tech Stack</h2>
    <ul>
        <li>Python (Pandas, scikit-learn)</li>
        <li>KNN Classifier with MultiOutputClassifier</li>
        <li>Machine Learning for multi-output prediction</li>
        <li>GitHub for version control and collaboration</li>
    </ul>

    <h2>🌟 Novelty</h2>
    <ul>
        <li><b>Industry-Centric Focus:</b> Tailored learning paths based on industry-specific requirements.</li>
        <li><b>Two-Way Alignment:</b> Matches job seekers with roles while creating a workforce for industries.</li>
        <li><b>Ongoing Career Growth:</b> Promotes continuous skill enhancement for evolving technologies.</li>
        <li><b>Workforce Retention:</b> Focuses on improving performance and retention of current employees.</li>
    </ul>

    <h2>🚀 Solution</h2>
    <p>
        The platform processes job titles, company names, and industries to predict core and company-specific skills. It uses a multi-output KNN classifier trained on a structured dataset to ensure accurate predictions.
    </p>

    <h2>📂 Others</h2>
    <p>
        <b>Dataset:</b> The project uses a custom dataset containing job-related data.<br>
        <b>Future Scope:</b> Integration with real-time job platforms and personalized recommendations for upskilling.<br>
        <b>Team:</b> Developed by CODEFLUENCERS at the Chennai Institute of Technology.
    </p>

    <h2>💻 Code</h2>
    <pre>
<code>
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import OneHotEncoder, MultiLabelBinarizer
from sklearn.neighbors import KNeighborsClassifier
from sklearn.multioutput import MultiOutputClassifier
from sklearn.metrics import classification_report

# Load the dataset
data = pd.read_csv('upskilling_dataset.csv')

# Preprocessing
categorical_features = ['Job Title', 'Company', 'Industry']
encoder = OneHotEncoder(sparse_output=False)
categorical_encoded = encoder.fit_transform(data[categorical_features])

data['Core Skills'] = data['Core Skills'].str.split(', ').apply(set)
data['Company-Specific Skills'] = data['Company-Specific Skills'].str.split(', ').apply(set)

mlb_core = MultiLabelBinarizer()
mlb_company = MultiLabelBinarizer()

y_core = mlb_core.fit_transform(data['Core Skills'])
y_company = mlb_company.fit_transform(data['Company-Specific Skills'])

y = pd.concat([pd.DataFrame(y_core), pd.DataFrame(y_company)], axis=1)
X = pd.DataFrame(categorical_encoded)

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

knn_model = KNeighborsClassifier()
multioutput_knn_model = MultiOutputClassifier(knn_model)
multioutput_knn_model.fit(X_train, y_train)

y_pred = multioutput_knn_model.predict(X_test)
print("Core Skills Classification Report:")
print(classification_report(y_test.iloc[:, :len(mlb_core.classes_)], y_pred[:, :len(mlb_core.classes_)], target_names=mlb_core.classes_))

print("Company-Specific Skills Classification Report:")
print(classification_report(y_test.iloc[:, len(mlb_core.classes_):], y_pred[:, len(mlb_core.classes_):], target_names=mlb_company.classes_))
</code>
    </pre>
</body>
</html>
