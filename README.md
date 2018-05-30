import psycopg2
from flask import Flask,send_from_directory
from flask_cors import CORS
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
import os
import pickle
path = os.getcwd()
print(path)
port = int(os.getenv("PORT", 3030))
upload_folder = path
ALLOWED_EXTENSIONS = set(['pkl','txt','csv'])
app = Flask(__name__)
CORS(app)
app.config['UPLOAD_FOLDER'] = upload_folder

def fetchData():
    try:
        conn = psycopg2.connect(database="postgres", user="postgres", password="root", host="localhost", port="5432")
        print("Opened database successfully")
        sql = "SELECT \"Size\", \"Bedrooms\", \"Age\", \"Bathrooms\", \"Price\" from public.\"PredictData\""
        df_sql = pd.read_sql(sql, conn)
        print("df_sql\n",df_sql)
        print("Fetch done successfully")
        print("Calling fft.....\n")
        df = numpy.fft.fft(df_sql,n=None, axis=-1, norm=None)
        print("df after fft\n",df)
    except Exception as e:
        print(e)

if __name__ == '__main__':
    fetchData()
    app.run(debug=True, port=port)
