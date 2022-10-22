# zomato_analysis

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv('zomato.csv')
df.head()
df.columns
df.dtypes
df.shape
df.isnull().sum()
feature_na=[feature for feature in df.columns if df[feature].isnull().sum()>0]
feature_na
for feature in feature_na:
    print('{} has {} missing values'.format(feature,np.round(df[feature].isnull().sum()/len(df)*100,4)))
df['rate'].unique()
df.dropna(axis='index',subset=['rate'],inplace=True)
df.shape
def split(x):
    return x.split('/')[0]
df['rate']=df['rate'].apply(split)
df.head()
df['rate'].unique()
df.replace('NEW',0, inplace=True)
df.replace('-',0, inplace=True)
df['rate']=df['rate'].astype(float)
df.head()
df_rate=df.groupby('name')['rate'].mean().to_frame().reset_index()
df_rate
df_rate.columns=['restaurants','avg_rating']
df_rate.head(20)
sns.histplot(df_rate['avg_rating'])
cuisines=df['cuisines'].value_counts()[0:10]
cuisines
df.columns
df['approx_cost(for two people)'].isna().sum()
df.dropna(axis='index',subset=['approx_cost(for two people)'],inplace=True)
df['approx_cost(for two people)'].isna().sum()
df['approx_cost(for two people)'].unique()
sns.histplot(df['approx_cost(for two people)'])
sns.scatterplot(x='rate',y='approx_cost(for two people)',data=df)
sns.scatterplot(x='rate',y='approx_cost(for two people)',hue='online_order',data=df)
sns.boxplot(x='online_order',y='votes',data=df)
