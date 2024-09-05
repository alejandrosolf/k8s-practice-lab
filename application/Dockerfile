FROM python:3.9.7

WORKDIR /app

COPY . /app

RUN pip3 install --no-cache-dir --requirement requirements.txt

EXPOSE 5000

ENTRYPOINT ["python3", "-m" , "flask", "run", "--host=0.0.0.0"]