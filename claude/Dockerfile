FROM python:3.12-alpine
RUN pip install mkdocs --no-cache-dir
WORKDIR /docs
EXPOSE 8000
CMD ["mkdocs", "serve", "--dev-addr=0.0.0.0:8000"]
