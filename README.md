# Data_manipulations
data manipulation in python progaramming
#creating a dataframe with given attributes
import pandas as pd
from datetime import datetime, date
df = pd.DataFrame({
    'Name': ['Elavarasan','Surya','sri','dinesh',
         'naveen','raj','gokul','guru','Srinithi','Arun'],
    'Father_name':['Ramesh','palanisamy','murugan','vadivel',
          'ganapathi','kannan','murugan','balan','sekar','raj'],
    'DOB':['05/06/2000','16/11/2001','29/01/2001','12/10/2008',
        '12/10/2010','12/11/2012','23/02/2000','15/7/2000','23/4/2000','7/6/2000']
     })            
def Age_cal(born):
    born=datetime.strptime(born,"%d/%m/%Y").date()
    today = date.today()
    Age = today.year - born.year - ((today.month,today.day) < (born.month,born.day))
    return Age
df['Age']=df['DOB'].apply(Age_cal) 
df['Father_Age']=df['Age']*2
df['Status']=df['Age'].apply(lambda x: 'Major' if x > 17 else 'Minor')
print("DATAFRAME")
df

#selectig a column with specific datatype
print("FATHER AGE")
df["Father_Age"]

#slicing the dataframe
df.loc[(df["Status"]=="Major"),["Name","Father_name","Age"]]

#Grouping by age
df.groupby(["Age"]).mean()

#Maping the dataframe column "Name" with  new column(Education)  
Education= {'Elavarasan': "PG", 'Surya':'UG',"Sri":'UG',"Dinesh":9,"naveen":8,"raj":7,"gokul":'PG',"guru":12,'srinithi':"PG","Arun":"MCA"}
df["Education"]=df["Name"].map(Education)
df

#Renaming the column names
df.rename(columns={"Education":"Qualification"},inplace=True)
df

#droping the row
df.drop([8],axis=0,inplace=True)
df

#droping the column
df.drop(["Status"], axis=1,inplace=True)
df

from google.colab import drive
drive.mount('/content/drive')

#converting to csv
df.to_csv("/content/drive/MyDrive/Python/elaa.csv")
