# **EXP No.6 – AI-Assisted Programming and Debugging**

## **🎯 Aim**

> **“To write and implement Python code using multiple AI tools to automate API interaction, compare AI-generated outputs, identify and fix programming errors, optimize code, explain computational complexity, generate unit tests, and evaluate the effectiveness of AI-assisted programming compared with manual coding.”**

---

# **🤖 AI Tools Required**

- **ChatGPT** 
- **Google Gemini** 
- **Claude** 
- **Python** 
- **Jupyter Notebook / Google Colab** 
- **VS Code** 

---

# **📌 Application Selected**

## **Intelligent User Behaviour Anomaly Detector**

> **“The selected application is an Intelligent User Behaviour Anomaly Detection System. The system analyzes employee behavioural data such as login time, login location, file access frequency, USB usage, email activity, and device information to identify unusual or suspicious behaviour.”**

---

# **👨‍💻 Persona Pattern**

### **Persona**

> **“Act as an experienced Python programmer and machine learning engineer specializing in cybersecurity and anomaly detection. Write clean, efficient, readable, and modular Python code for detecting anomalous employee behaviour. Follow Python best practices, handle errors properly, explain the computational complexity, and generate appropriate unit tests.”**

---

# **1️⃣ Python Code Generation Using AI**

### **Prompt Given to AI Tools**

> **“Act as an experienced Python programmer. Write a Python program for an employee behaviour anomaly detection system. The program should accept employee activity data containing login time, login location, file access frequency, USB usage, email activity, and device information. Preprocess the data and use Isolation Forest to identify anomalous behaviour. Display the detected anomalies clearly.”**

---

## **🤖 ChatGPT Output**

```
import pandas as pd


from sklearn.preprocessing import LabelEncoder

from sklearn.ensemble import IsolationForest

\# Load dataset

data = pd.read\_csv("employee\_activity.csv")

\# Encode categorical columns

encoder = LabelEncoder()

data["login\_location"] = encoder.fit\_transform(

data["login\_location"]

)

data["device\_used"] = encoder.fit\_transform(

data["device\_used"]

)

\# Select features

features = [

"login\_time",

"login\_location",

"file\_access\_frequency",

"usb\_usage",

"email\_activity",

"device\_used"

]

X = data[features]

\# Train Isolation Forest

model = IsolationForest(

contamination=0.1,

random\_state=42

)

data["anomaly"] = model.fit\_predict(X)

\# Convert prediction into readable labels

data["status"] = data["anomaly"].map({

1: "Normal",

-1: "Anomalous"

})

print(data[["status"]])
```
---

# **2️⃣ Google Gemini Output**

### **Prompt**

> **“Generate Python code for detecting anomalous employee behaviour using Isolation Forest. Include preprocessing, categorical encoding, model training, prediction, and display of anomalous records.”**

### **Generated Approach**

> **“Gemini generated a similar Isolation Forest-based solution but included additional data validation and a separate function for preprocessing the dataset.”**

Example structure:

```
def preprocess_data(data):


data = data.copy()

data["login\_location"] = (

data["login\_location"].astype("category").cat.codes

    )

data["device\_used"] = (

data["device\_used"].astype("category").cat.codes

    )

return data



def detect\_anomalies(data):

features = [

"login\_time",

"login\_location",

"file\_access\_frequency",

"usb\_usage",

"email\_activity",

"device\_used"

    ]

model = IsolationForest(

contamination=0.1,

random\_state=42

    )

data["prediction"] = model.fit\_predict(

data[features]

    )

return data
```
---

# **3️⃣ Claude Output**

### **Prompt**

> **“Generate clean and modular Python code for employee behaviour anomaly detection using Isolation Forest. Separate data preprocessing and anomaly detection into functions and include error handling.”**

### **Generated Approach**

```
import pandas as pd


from sklearn.ensemble import IsolationForest



def load\_data(filename):

try:

return pd.read\_csv(filename)

except FileNotFoundError:

print("Dataset not found.")

return None



def detect\_anomalies(data):

features = [

"login\_time",

"login\_location",

"file\_access\_frequency",

"usb\_usage",

"email\_activity",

"device\_used"

    ]

model = IsolationForest(

contamination=0.1,

random\_state=42

    )

data["prediction"] = model.fit\_predict(

data[features]

    )

return data



data = load\_data("employee\_activity.csv")

if data is not None:

result = detect\_anomalies(data)

print(

result[result["prediction"] == -1]

    )
```
---

# **📊 AI Code Comparison**

| **Feature**                    |     ChatGPT                |   Gemini                   |   Claude                   |
| ------------------------------ | -------------------------- | -------------------------- | -------------------------- |
| **Basic Code Generation**      | ✅                         | ✅                          | ✅                       |
| **Data Preprocessing**         | ✅                         | ✅                          | ✅                       |
| **Isolation Forest**           | ✅                         | ✅                          | ✅                       |
| **Modular Functions**          | ⚠️                         | ✅                          | ✅                       |
| **Error Handling**             | ⚠️                         | ⚠️                         | ✅                        |
| **Code Readability**           | High                       | High                       | Very High                  |
| **Beginner Friendly**          | Very High                  | High                       | High                       |
| **Optimization**               | Medium                     | High                       | High                       |
| **Unit Testing**               | Requires additional prompt | Requires additional prompt | Requires additional prompt |

---

# **🐛 Bug Identification**

### **Prompt**

> **“Review the generated Python code as a senior programmer. Identify syntax errors, logical errors, data preprocessing problems, possible runtime errors, and machine learning issues. Explain how each issue can be fixed.”**

### **Potential Bugs Identified**

| **Bug / Issue**              |     Cause                                | Solution                           |
| ---------------------------- | ---------------------------------------- | ---------------------------------- |
| Missing dataset              | Incorrect file path                      | Verify dataset path                |
| Missing values               | Dataset contains null values             | Apply missing-value handling       |
| Invalid categorical values   | ML model requires numerical values       | Encode categorical features        |
| Feature mismatch             | Expected columns are missing             | Validate required columns          |
| Incorrect contamination      | Poor anomaly proportion assumption       | Tune contamination parameter       |
| Data leakage                 | Using inappropriate data during training | Separate training and testing data |

---

# **🔧 Code Optimization**

### **Prompt**

> **“Optimize the generated Python anomaly detection code for readability, efficiency, maintainability, and scalability. Avoid unnecessary operations and use reusable functions.”**

### **Optimized Structure**

```
Employee Activity Dataset
```

          ↓

Data Validation

          ↓

Data Preprocessing

          ↓

Feature Selection

          ↓

Isolation Forest

          ↓

Anomaly Prediction

          ↓

Normal / Anomalous

          ↓

Security Alert

---

# **⚡ Optimized Python Code**

```
import pandas as pd


from sklearn.ensemble import IsolationForest



FEATURES = [

"login\_time",

"login\_location",

"file\_access\_frequency",

"usb\_usage",

"email\_activity",

"device\_used"

]



def preprocess\_data(data):

data = data.copy()

for column in ["login\_location", "device\_used"]:

data[column] = data[column].astype("category").cat.codes

return data[FEATURES]



def detect\_anomalies(data):

model = IsolationForest(

contamination=0.1,

random\_state=42,

n\_jobs=-1

    )

predictions = model.fit\_predict(data)

return predictions



df = pd.read\_csv("employee\_activity.csv")

X = preprocess\_data(df)

df["status"] = detect\_anomalies(X)

df["status"] = df["status"].map({

1: "Normal",

-1: "Anomalous"

})

print(df)
```
---

# **🧮 Complexity Analysis**

### **Prompt**

> **“Explain the time and space complexity of the employee behaviour anomaly detection code.”**

### **Analysis**

Let:

- **n = number of employee records** 
- **m = number of features** 

### **Time Complexity**

> **“Data preprocessing requires approximately O(n × m) time because each record and feature may need to be processed.”**

> **“Isolation Forest training and prediction depend on the number of samples and trees. In practical implementations, the computational cost is approximately O(t × n log n), where t represents the number of trees.”**

### **Space Complexity**

> **“The dataset requires approximately O(n × m) memory, while the Isolation Forest model requires additional memory for storing the decision trees.”**

---

# **🧪 Unit Test Generation**

### **Prompt**

> **“Generate Python unit tests for the employee behaviour anomaly detection functions. Test normal input, missing values, invalid input, and anomaly detection output.”**

### **Unit Test Example**

```
import pandas as pd


import pytest

from anomaly\_detector import preprocess\_data



def test\_preprocess\_data():

data = pd.DataFrame({

"login\_time": [10, 11],

"login\_location": ["Office", "Office"],

"file\_access\_frequency": [5, 6],

"usb\_usage": [0, 1],

"email\_activity": [3, 4],

"device\_used": ["Laptop", "Laptop"]

    })

result = preprocess\_data(data)

assert result.shape == (2, 6)



def test\_required\_columns():

data = pd.DataFrame({

"login\_time": [10]

    })

with pytest.raises(KeyError):

preprocess\_data(data)
```
---

# **🧪 Unit Testing Results**

| **Test Case**                      |      Expected                     |Result   |
| ---------------------------------- | --------------------------------- | ------  |
| Valid employee data                | Data successfully processed       | ✅ PASS |
| Categorical values                 | Converted to numerical values     | ✅ PASS |
| Missing required column            | Error raised                      | ✅ PASS |
| Anomaly prediction                 | Normal/Anomalous output generated | ✅ PASS |

---

# **🔄 Manual Coding vs AI-Assisted Coding**

| **Parameter**                                |    Manual Coding              |    AI-Assisted Coding          |
| -------------------------------------------- | ----------------------------- | ------------------------------ |
| **Development Speed**                        | Medium                        | Very High                      |
| **Code Generation**                          | Requires manual effort        | Very Fast                      |
| **Debugging**                                | Manual                        | AI-assisted                    |
| **Optimization**                             | Developer dependent           | AI suggestions available       |
| **Learning**                                 | Strong understanding required | Explanations available         |
| **Errors**                                   | Can occur                     | Can also occur                 |
| **Testing**                                  | Manual test creation          | Automated test generation      |
| **Code Quality**                             | Depends on developer          | Depends on prompt + validation |
| **Maintainability**                          | Developer controlled          | Requires review                |
| **Final Reliability**                        | Requires testing              | Requires testing               |

---

# **📈 Code Quality Analysis**

| **Quality FactorAI-Assisted Coding **       |  Result         |
| ------------------------------------------- | ----------------|
| **Readability**                             | ⭐⭐⭐⭐⭐    |
| **Efficiency**                              | ⭐⭐⭐⭐☆     |
| **Maintainability**                         | ⭐⭐⭐⭐☆     |
| **Error Handling**                          | ⭐⭐⭐⭐☆     |
| **Modularity**                              | ⭐⭐⭐⭐⭐    |
| **Testing**                                 | ⭐⭐⭐⭐☆     |
| **Documentation**                           | ⭐⭐⭐⭐☆     |
| **Overall Quality**                         | **⭐⭐⭐⭐☆** |

---

# **💡 Analysis and Discussion**

> **“AI-assisted programming significantly reduced the time required to generate the initial Python implementation. Multiple AI tools were able to produce functional approaches for employee behaviour anomaly detection using Isolation Forest.”**

> **“However, the generated code cannot be accepted without verification. Some outputs may contain incorrect assumptions, missing error handling, unsuitable preprocessing, or inefficient implementation.”**

> **“ChatGPT provided a simple and beginner-friendly implementation, Gemini provided a structured approach, while Claude produced more modular code with better error handling.”**

> **“The experiment demonstrates that AI tools are highly useful for code generation, debugging, optimization, complexity analysis, and test generation, but human validation remains necessary to ensure correctness and reliability.”**

---

# **🏆 Best AI-Assisted Approach**

> **“Among the tested approaches, the combination of AI-generated code, manual verification, debugging, optimization, and unit testing provided the most reliable solution.”**

### **Recommended Workflow**

```
Problem Definition
```

       ↓

Persona Prompt

       ↓

Generate Code

       ↓

Compare AI Outputs

       ↓

Identify Bugs

       ↓

Fix Bugs

       ↓

Optimize Code

       ↓

Analyze Complexity

       ↓

Generate Unit Tests

       ↓

Manual Validation

       ↓

Final Code

---

# **✅ Conclusion**

> **“This experiment demonstrated the effectiveness of AI-assisted programming and debugging using multiple AI tools. ChatGPT, Gemini, and Claude were used to generate Python code for an employee behaviour anomaly detection application.”**

> **“The generated programs were compared based on code quality, readability, modularity, efficiency, error handling, and testing support. AI tools significantly reduced development time and provided useful assistance in debugging, optimization, complexity analysis, and unit-test generation.”**

> **“However, AI-generated code may contain logical errors, incorrect assumptions, or security issues. Therefore, human review, testing, and engineering validation are essential before using AI-generated code in real-world applications.”**

### **Final Finding**

> **“AI-assisted programming is most effective when AI-generated code is combined with human expertise, testing, debugging, and validation rather than being used without verification.”**

## **Result** 
The corresponding Prompt is executed successfully.
