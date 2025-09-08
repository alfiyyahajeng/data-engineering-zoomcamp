# Simple Data Ingestion

### 1. Membuat Data Ingestion sederhana 🗃️
1. Buat file pipeline.py file ini berisi script sederhana untuk menerima argumen dari command line untuk menjalan proses berdasarkan tanggal tertentu
```python
import sys
import pandas as ps
print(sys.argv)
day = sys.argv[1]
print(f'job finish successfully for day {day}')
```

2. Buat file Dockerfile yang berisikan konfigurasi untuk membuat docker image
```python
FROM python:3.9.1
RUN apt-get install wget
RUN pip install pandas sqlalchemy psycopg2
WORKDIR /app
COPY pipeline.py pipeline.py 
ENTRYPOINT [ "python", "pipeline.py" ]
```
3. Jalankan docker desktop
4. Masukan command ini membuat image `docker build -t test:pandas .`
5. Masukan command ini untuk menjalankan container dan menambahkan tanggal (2025-02-14) serta argumen (proses-1) `docker run -it test:pandas 2025-02-14 proses-1` 
