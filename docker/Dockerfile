FROM python:3.7

# Set the working directory (workdir) to /app
RUN mkdir /app
WORKDIR /app

# Install dependencies
RUN apt update 

COPY flask_app/requirements.txt .
RUN pip install -r requirements.txt

# Set application environment variables
ENV FLASK_APP=main.py
ENV FLASK_RUN_HOST=0.0.0.0

# Expose port 5000
EXPOSE 5000

# Copy the app files to workdir
COPY flask_app .

# Default command when start a container
CMD ["bash", "-c", "flask run"]