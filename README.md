# Ex-09-Data-Visualization-

## AIM
_To Perform Data Visualization on a complex dataset and save the data to a file._

# Explanation
_**Data visualization** is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data._

# ALGORITHM
- **_STEP 1_**: Read the given Data
- **_STEP 2_**: Clean the Data Set using Data Cleaning Process
- **_STEP 3_**: Apply Feature generation and selection techniques to all the features of the data set
- **_STEP 4_**: Apply data visualization techniques to identify the patterns of the data.



- **_DATASET_**
```python
import seaborn as sns
import pandas as pd
import matplotlib.pyplot as plt
df=sns.load_dataset("tips")
print(df)
```
<img width="230" src="https://github.com/Adhithyaram29D/ODD2023-Datascience-Ex-09/assets/119393540/a9ed2d62-327d-4a7e-a17c-3c8ed222d41c">

<br>

- **_NULL VALUES_**
```python
df.isnull().sum()
```
<img width="150" src="https://github.com/Adhithyaram29D/ODD2023-Datascience-Ex-09/assets/119393540/fe9a1b6e-f023-4b81-98c0-55cd3d65d103">

- **_OUTLIERS_**
```PYTHON
plt.figure(figsize=(5,5))
plt.title("Data with Outliners")
df.boxplot()
plt.show()
```
<img width="218" alt="280584089-bff556d9-b4fe-4858-a01b-321486dfde3d" src="https://github.com/Adhithyaram29D/ODD2023-Datascience-Ex-09/assets/119393540/4195182a-75fb-4b8e-8c9f-5a1e753e5e47">

- **_AFTER REMOVING THE OUTLIERS_**
```python
plt.figure(figsize=(5,5))
cols=["size","tip","total_bill"]
q1=df[cols].quantile(0.25)
q3=df[cols].quantile(0.75)
iqr=q3-q1
df=df[~((df[cols]<(q1-1.5*iqr))|(df[cols]>(q3+1.5*iqr))).any(axis=1)]
plt.title("dataset after removing outliners")
df.boxplot()
plt.show()
```
<img width="218" alt="280584089-bff556d9-b4fe-4858-a01b-321486dfde3d" src="https://github.com/Adhithyaram29D/ODD2023-Datascience-Ex-09/assets/119393540/b0cc2898-5ec1-40f0-8649-27c0a89290eb">

- **_HIGHEST TOTAL BILL AMOUNT BY DAY OF THE WEEK_**
```python
sns.barplot(x=df["day"],y=df["total_bill"],hue=df["day"])
plt.legend(loc="center")
plt.title("highest total bill amount by day of the week")
```
<img width="283" alt="280585224-936109b5-b9e1-4999-9141-c9efe1392fb1" src="https://github.com/Adhithyaram29D/ODD2023-Datascience-Ex-09/assets/119393540/d694a729-7447-4800-8934-d48ce84b29af">

- **_AVERAGE TIP AMOUNT GIVEN BY SMOKERS AND NON - SMOKERS_**
```python
sns.boxplot(x=df["smoker"],y=df["tip"],hue=df["smoker"])
plt.title("average tip amount given by smokers and non-smokers")
```
<img width="280" alt="280585652-bfd1968b-ae05-4021-85c1-6f4b5de61b44" src="https://github.com/Adhithyaram29D/ODD2023-Datascience-Ex-09/assets/119393540/7424422a-cfb6-44bb-8d2d-c9a128c3434a">

- **_TIP PERCENTAGE BY DINING PARTY SIZE_**
```PYTHON
df["tip_percent"]=df["tip"] / df["total_bill"]
sns.scatterplot(x=df['size'], y=df['tip_percent'],data=df)
plt.title("Tip Percentage by Dining Party Size")
```
<img width="289" alt="280585759-b1c54cf2-01fd-46a4-821e-d1d2c073b5d4" src="https://github.com/Adhithyaram29D/ODD2023-Datascience-Ex-09/assets/119393540/3cb783b5-f5dd-4328-b5f0-5d0a11d49232">

- **_TIPS BASED ON GENDER_**
```PYTHON
sns.boxplot(x=df["sex"],y=df["tip"],hue=df["sex"])
plt.title("tips based on gender")
```
<img width="279" alt="280585813-149a4c35-19c5-4277-9ada-4d29368c33d1" src="https://github.com/Adhithyaram29D/ODD2023-Datascience-Ex-09/assets/119393540/a3b344c5-a1d0-4f00-9753-2c02f5d8715d">

- **_TOTAL BILL AMOUNT BY DAY OF THE WEEK_**
```PYTHON
sns.scatterplot(x=df["day"],y=df["total_bill"],hue=df["day"])
plt.legend(loc="best")
plt.title("total bill amount by day of te week")
```
<img width="293" alt="280586070-78260705-ff35-4243-9a6a-10e2684c19e4" src="https://github.com/Adhithyaram29D/ODD2023-Datascience-Ex-09/assets/119393540/f0f8a720-96aa-4d65-83a5-5de58c2792ee">


- **_DISTRIBUTION OF TOTAL AMOUNTS BY TIME OF DAY_**
```PYTHON
sns.histplot(data=df, x="total_bill", hue="time", element="step", stat="density")
plt.title("Distribution of Total Bill Amounts by Time of Day")
plt.show()
```
<img width="293" alt="280586338-ce0246bb-47ed-43c1-820f-8375cb19a59d" src="https://github.com/Adhithyaram29D/ODD2023-Datascience-Ex-09/assets/119393540/346a628e-6ccb-4c0d-bb87-93405205fd34">

- **_AVERAGE TOTAL BILL AMOUNT BY DINNING PARTY SIZE_**
```PYTHON
sns.barplot(x=df["size"],y=df["total_bill"],hue=df["size"])
plt.title("average total bill amount by dinning party size")
```
<img width="286" alt="280586459-ac743628-bc52-4210-b118-39874bb7c618" src="https://github.com/Adhithyaram29D/ODD2023-Datascience-Ex-09/assets/119393540/8dfe8f2e-0a74-4037-8b05-c765a62d5eab">

- **_TIP AMOUNT BY DAY OF WEEK_**
```PYTHON
sns.boxplot(x="day", y="tip", data=df)
plt.title("Tip Amount by Day of Week")
plt.show()
```
<img width="278" alt="280586561-0da84310-abad-4130-a3c8-4a00aa546eb4" src="https://github.com/Adhithyaram29D/ODD2023-Datascience-Ex-09/assets/119393540/ff16f8b0-67f7-481e-9f66-c0578902d24e">

- **_TIP AMOUNT TIME OF DAY_**
```PYTHON
sns.violinplot(x="time",y="tip",data=df)
plt.title("tip amount time of day")
```
<img width="284" alt="280586764-429d50b8-c667-4568-8077-4df99aba54aa" src="https://github.com/Adhithyaram29D/ODD2023-Datascience-Ex-09/assets/119393540/2de581ab-b7e4-4996-8e9a-c369a6e7adf2">

- **_CORRELATION BETWEEN TIP AMOUNT AND TOTAL BILL AMOUNT_**
```PYTHON
sns.scatterplot(x="total_bill",y="tip",data=df)
plt.title("Correlation between Tip Amount and Total Bill Amount")
plt.show()
```

<img width="280" alt="280586794-ef1864f3-454f-4a41-81c0-9e39b9907e08" src="https://github.com/Adhithyaram29D/ODD2023-Datascience-Ex-09/assets/119393540/5c25207c-95de-421b-bdb3-7e30f6aff55f">

# RESULT:
_Thus, Data Visualization on a complex dataset and save the data to a file has been performed successfully._