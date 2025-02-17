# Container dasar
FROM python:3.9.1

# Perintah container untuk install pandas
RUN apt-get install wget
RUN pip install pandas sqlalchemy psycopg2

# spesifikan work directorynya
WORKDIR /app

# menyalin script ke container 
COPY pipeline.py pipeline.py 

# mendefinisikan apa yang dilakukan pertama kali ketika container berjalan
ENTRYPOINT [ "python", "pipeline.py" ]