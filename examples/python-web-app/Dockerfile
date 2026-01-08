# -------------------------------
# Stage 1: Builder
# -------------------------------
FROM ubuntu AS builder
 
WORKDIR /app
 
# Install system dependencies
RUN apt-get update && \
    apt-get install -y python3 python3-pip python3-venv && \
    rm -rf /var/lib/apt/lists/*
 
# Copy requirements and source
COPY requirements.txt .
COPY devops .
 
# Create virtual environment and install dependencies
RUN python3 -m venv venv1 && \
    . venv1/bin/activate && \
    pip install --no-cache-dir -r requirements.txt
 
 
# -------------------------------
# Stage 2: Runtime
# -------------------------------
FROM ubuntu
 
WORKDIR /app
 
# Install only runtime dependencies
RUN apt-get update && \
    apt-get install -y python3 && \
    rm -rf /var/lib/apt/lists/*
 
# Copy app code and virtual environment from builder
COPY --from=builder /app /app
 
EXPOSE 8000
 
CMD ["/bin/bash", "-c", "source venv1/bin/activate && python3 manage.py runserver 0.0.0.0:8000"]

 
 
