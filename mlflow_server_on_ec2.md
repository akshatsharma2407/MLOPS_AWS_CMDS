Run the following command on EC2 machine

sudo apt update

sudo apt install python3-pip

sudo apt install pipx

sudo pipx ensurepath

pipxinstall pipenv

export PATH=$PATH:/home/ubuntu/.local/bin

echo 'export PATH=$PATH:/home/ubuntu/.local/bin' >> ~/.bashrc

source ~/.bashrc

mkdir mlflow

cd mlflow

pipenv shell

pipenv install setuptools

pipenv install mlflow

pipenv install awscli

pipenv install boto3

## Then set aws credentials (IAM USER access key and secret key)
aws configure


#Finally (this code will ensure that mlflow server is running on ec2, even if you disconnect to ec2 console)
nohup mlflow server \
    --host 0.0.0.0 \
    --port 5000 \
    --default-artifact-root s3://BUCKETNAME \
    --allowed-hosts '*' \
    --cors-allowed-origins '*' > mlflow.log 2>&1 &

# after this add a port on 5000 in inbound security rules with 0.0.0.0/0 and your mlflow server will be up and running
