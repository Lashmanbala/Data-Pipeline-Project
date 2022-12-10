# Data-Pipeline-Project
Data Pipeline Project using Pandas, AWS Lambda, s3, RDS.

# Reading Data

There are 3 csv files with data regarding Game of Thrones. The data was downloaded from Kaggle.

I read the data using Pandas in Jupyter notebook

# Data Cleaning

There are some columns with lot of NaN values. Those columns barely has data. So I removed those columns using pandas.

The attacker column has the battle outcome details in binary fomat(0 and 1). I mapped it with 'win' and 'loss'.

attacker_size and defender_size columns has some NaN values. I replaced those values with the mean values of the respective columns.

And I converted the dataframes into csv files in order to put it in the s3 bucket.

# Creating the components of the pipeline

I created s3 client using boto3 package. though which I created a s3 bucket.

I created a Mysql server in AWS RDS. And I connected with the server using Sqlalchemy package. And I created database in order to put table thorough Lambda function.

I created a Lambda function with a trigger of s3 bucket which I have created. If any input of a csv file will trigger the function.
In the code part of I connected with the s3 and Mysql. But here I needed to create a lambda layer to import the Sqlalchemy and Pandas packages which are not available in Lambda.

# Working of The Pipeline

Once I put a csv file which i've created from the cleaned dataframe, It'll trigger the Lambda function. Then the Lambda function access the particular s3 bucket and read the csv file in it. And using Pandas it'll create a dataframe out of the csv file. Using pandas to_sql() method it'll put the dataframe as table in the AWS RDS.
