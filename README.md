# data-engineering-zoomcamp

### 1. Membuat Data Ingestion sederhana 🗃️
1. Buat file pipeline.py file ini berisi script sederhana untuk menerima argumen dari command line untuk menjalan proses berdasarkan tanggal tertentu
`import sys
import pandas as ps

#fungsi menampilkan argumen
print(sys.argv)
day = sys.argv[1]

print(f'job finish successfully for day {day}')`

2. Buat file Dockerfile yang berisikan konfigurasi untuk membuat docker image

`# Container dasar
FROM python:3.9.1
# Perintah container untuk install pandas
RUN apt-get install wget
RUN pip install pandas sqlalchemy psycopg2
# spesifikan work directorynya
WORKDIR /app
# menyalin script ke container 
COPY pipeline.py pipeline.py 
# mendefinisikan apa yang dilakukan pertama kali ketika container berjalan
ENTRYPOINT [ "python", "pipeline.py" ]`

3. Jalankan docker desktop
4. Masukan command ini membuat image `docker build -t test:pandas .`
5. Masukan command ini untuk menjalankan container dan menambahkan tanggal (2025-02-14) serta argumen (proses-1) `docker run -it test:pandas 2025-02-14 proses-1` 
